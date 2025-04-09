---
title: Implementación continua de la integración de Selenium
linkTitle: CI Tool
weight: 6
description: |
  Solíamos tener una herramienta de CI de Jenkins que ejecutaba pruebas unitarias y ejecutaba pruebas de integración en Sauce Labs. Hemos movido todas las pruebas a Travis, y ahora ejecutamos todo con Github Actions.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Continuous-Integration)

## Arquitectura general

Tenemos una serie de máquinas virtuales de Google Computer Engine ejecutando Ubuntu, actualmente alojadas en {0..29}.ci.seleniumhq. rg - tienen DNS públicamente direccionable configurado para el punto [ab](ab.md).{0..29}. i.seleniumhq.org también los señala, para que las pruebas de cookies puedan hacer búsquedas de subdominios.

Una de estas máquinas, ci.seleniumhq.org, está ejecutando jenkins. Si quieres un login en jenkins, ponte en contacto con juangj.  El Build All Java job encuesta SCM para cambios, y hace lo siguiente:

- Hace una construcción limpia del objetivo 'lanzamiento', cualquier prueba que se vaya a ejecutar, y cualquier artefacto (e. . el ejecutable de IEDriverServer) que será requerido para ejecutar esas pruebas
- Muestra todo el directorio de trabajo construido y lo publica en http://ci.seleniumhq.org/selenium-trunk-r${REVISION}.tgz - esto es usado más tarde por ejecuciones de prueba
- Publica el jarro selenium-server-standalone en http://ci.seleniumhq.org/selenium-server-standalone-r${REVISION}.tgz - esto es copiado directamente por [SauceLabs](http://saucelabs.com) al ejecutar pruebas.
- Publica el IEDriverServer y lo publica en http://ci.seleniumhq.org/IEDriverServer-Win32-r${REVISION}. ip - esto es copiado directamente por [SauceLabs](http://saucelabs.com) para ejecutar pruebas IE
  Esta máquina está respaldada por un disco persistente de 1TB, que pueden contener muchos artefactos de construcción, pero deben ser eliminados ocasionalmente (especialmente cuando se mueven el disco entre zonas).

Cuando esta compilación tiene éxito, activa las compilaciones de aguas abajo para cada combinación de OS/navegador/prueba que nos importa.  También activa una construcción limpia para asegurar que nuestros paneles de laberinto sigan en orden ("construcción de Maven").

Aparte de "Maven build" que se ejecuta en el mismo nodo de compilación (un carpintero, Máquina de 8-CPU con 32GB RAM), todas las versiones de downstream se ejecutan en nodos de construcción independientes.

Las versiones de aguas abajo se configuran usando variables de entorno, según la clase [SauceDriver](https://github.com/SeleniumHQ/selenium/blob/master/java/client/test/org/openqa/selenium/testing/drivers/SauceDriver.java).  Las versiones posteriores descargan el tar selenium-trunk del maestro de construcción, y luego ejecute las pruebas (que ya deberían haber sido compiladas por la regla Build All Java).  Dos de estas versiones anteriores son especiales; "HtmlUnit Java Tests" y "Pequeñas Pruebas" sólo ejecutan localmente sin headless.  Los otros usan [SauceLabs](http://saucelabs.com).

Una nota acerca de la red: Los nodos de construcción están configurados en una red interna 10.1.0/24, por lo que la comunicación de red entre ellos es increíblemente rápida y gratuita.

Cuando se está ejecutando una prueba de navegador sin encabezamiento, el servlet de test-file aloja los archivos de prueba en puertos determinados por una variable de entorno (231${EXECUTOR\_NUMBER} y 241${EXECUTOR\_NUMBER} - EXECUTOR\_NUMBER es actualmente siempre igual a 0).  El nombre de host utilizado por las pruebas es establecido por una variable de entorno ([ab](ab.md).${NODE\_NAME}.ci.seleniumhq.org donde NODE\_NAME en {0..29}).  Se solicita un navegador a [SauceLabs](http://saucelabs.com) usando nuestras credenciales (almacenadas en variables de entorno de todo jenkins, configuradas en la página de configuración del sistema).  Jenkins está configurado actualmente para ejecutar tres clases de test-classes a la vez en paralelo, por ejecución de prueba, de nuevo en la página Configuración del sistema.

Las pruebas se ejecutan y los resultados son notificados al IRC.

Gracias a [SauceLabs](http://saucelabs.com) y [Google](http://cloud.google.com/products/compute-engine.html) por donar la infraestructura para ejecutar todas estas pruebas.

## FAQ

### Quiero ejecutar mis pruebas en Sauce como lo hace Jenkins (mis pruebas fallan en CI, pero funcionan bien en mi máquina!)

Ver la página [SauceDriver](Sauce.md)

### Quiero añadir un nuevo navegador (¡Firefox ha lanzado una nueva versión!)

Jenkins no tiene un gran concepto de plantillas.  I (dawagner) tengo algunos scripts de selenium que automatizan la interfaz de usuario de Jenkins, para crear nuevos trabajos usando los ajustes enlatados.  Si quieres hacerlo manualmente, aquí están aproximadamente los pasos a seguir:

- Encuentra las configuraciones más similares que quieras copiar.  Si es una nueva versión de Firefox, encuentre la última versión de firefox (que debería tener aproximadamente 6 compilaciones asociadas con él: Javascript + Java {Windows,Linux} \*\*{Native,Synthesized}
- Para cada una de estas compilaciones, crea un nuevo Job (menú en el lado izquierdo de la página de inicio, al iniciar sesión)
- Nombra el trabajo al estilo de los demás.  Selecciona "Copiar trabajo existente" e introduce el trabajo que estás copiando.
- Desplácese por el trabajo que está prepoblado.  Reemplace los números de versión, el nombre del navegador y cualquier otro detalle que necesite reemplazar.  Para actualizaciones de firefox, actualmente hay tres lugares en los que deberías estar reemplazando el número (el campo "browser\_version" y dos en la consola de ejecución de construcción)
- Guardar
- Ve a la tarea Build All Java, configúrela, añade tu nueva construcción al campo "Proyectos para construir" donde hay muchos otros listados.\*\*

Si se trata de una actualización de firefox, probablemente también quiera eliminar una versión existente.
