---
title: Añadiendo nuevos conductores al código de Selenium 2
linkTitle: Conductores
weight: 4
description: |
  Instrucciones para cómo crear pruebas para nuevos controladores para Selenium 2.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Writing-New-Drivers) \

## Introducción

WebDriver tiene un conjunto completo de pruebas que describen el comportamiento esperado de una nueva implementación. Supondremos que está implementando el controlador en Java en aras de la simplicidad, pero puede echar un vistazo a cualquiera de las implementaciones existentes para ver cómo manejamos compilaciones más complejas u otros lenguajes una vez que haya leído esto.

## Escribir una nueva implementación de WebDriver

### Crear nuevos directorios de nivel

Crea una nueva carpeta de nivel superior, paralela a "común" y "firefox", con el nombre de tu navegador. En esto, crea un directorio "src/java" y un directorio "test/java". Debería ser obvio lo que va a dónde.

### Configurar una Suite de Prueba

Copie una de las suites de prueba existentes a su árbol de pruebas, y modifíquela para su nuevo navegador. Esto probablemente hará que modifiques la "Ignora". ava", que es de esperar, y añadir una clase holding para su implementación en el árbol fuente. **debes** incluir el directorio "común" para poder recoger todas las pruebas. Por ahora, mientras nada cause un colapso fatal, deje las pruebas tal como están.

Una vez que hayas añadido la suite de pruebas, añade un archivo CrazyFunBuild "build.desc" en el nivel superior de tu proyecto. Modelo después del que está en el directorio "htmlunit". Deberías poder ejecutar tus pruebas desde la línea de comandos usando el script "go".

En este punto, esperamos un fracaso total y tópico cuando se lleven a cabo las pruebas.

### Empezar a implementar

Si tu navegador se queda sin proceso, se recomienda encarecidamente_ hacer uso del JsonWireProtocol. Esto hará que el lado del cliente (las APIs que los usuarios usan) sean relativamente baratas para implementar, y significa que usted obtiene Java, C#, Ruby y Python soportan un esfuerzo significativamente menor ya que puedes extender el cliente remoto.

## Consejos de implementación

### Donde empezar

Como se ha mencionado, tiene un conjunto de pruebas. El orden sugerido para hacer este pase es ásperamente:

1. ElementFindingTest --- necesario porque la ubicación del elemento es clave
2. Páginas de carga
3. ChildrenFindingTest --- más elementos de búsqueda
4. FormHandlingTest
5. FrameSwitchingTest
6. Ejecutando prueba de Javascript
7. JavascriptActivedDriverTest

Llegados a este punto, tendrá un conductor de trabajo razonablemente completo. Después de eso, probablemente sea mejor obtener las interacciones del usuario correctamente:

1. Prueba Correcta
2. TypingTest

Antes de girar en el borde del corte:

1. AlertsTest

No es necesario hacer que cada prueba funcione en una clase antes de continuar. Suelo ir lo más abajo posible de una clase y luego cambie a la siguiente clase de la lista cuando la marcha se haga más dura. Esto le permite mantener una velocidad razonable y aún así cubrir lo básico.

### Ejecutar una sola prueba

Está lejos de ser ideal, pero el método que utilizamos es modificar la clase SingleTestSuite en el proyecto común, y luego modificar el módulo desde el que se ejecuta a través de la interfaz de usuario de IDE (es decir, simplemente vaya a la configuración de inicio (en IDEA) y modifique el módulo utilizado: ¡no muevas el archivo!) Esta clase debe ser autoexplicativa.

### Ignorando Pruebas

En algún momento querrá dejar de ejecutar pruebas de forma ad hoc y hacer uso de un producto de construcción continua para asegurarse de que no está introduciendo regresiones. En este punto, el proceso es ejecutar las pruebas desde la línea de comandos. Esto generará una lista de pruebas fallidas. Vaya a través de cada una de estas pruebas y añada o modifique el "@Ignore" asociado con la prueba. Vuelva a ejecutar las pruebas. Puede tomar algunas iteraciones, pero tu construcción terminará siendo verde. Niza.

La construcción hace uso de ant detrás de las escenas y almacena los registros en "build/build\_log.xml" y los registros de pruebas en "build/test\_logs"
