---
title: Herramienta de construcción loca
linkTitle: Diversión loca
weight: 2
description: |
  La herramienta original de construcción de Selenium que creció de nada hasta ser extremadamente inmanejable, lo que hace que trabaje de forma loca y "divertida".
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Crazy-Fun-Build)

WebDriver es un gran proyecto: si tratamos de empujar todo en un único archivo de construcción monolítica, eventualmente se vuelve inmanejable. Lo sabemos. Lo hemos probado. Así que rompimos el único Rakefile en una serie de archivos `build.desc`. Cada uno de ellos describe una parte de la construcción.

Echemos un vistazo a un archivo build.desc. Esto es parte del [test principal build.desc](https://github.com/SeleniumHQ/selenium/blob/master/java/client/test/org/openqa/selenium/build.desc):

```
java_test(name = "single",
  srcs = [
    "SingleTestSuite. ava",
  ],
  deps = [
    ":tests",
    "//java/server/src/org/openqa/selenium/server",
    "//java/client/test/org/openqa/selenium/v1:selenium-backed-webdriver-test",
    "//java/client/test/org/openqa/selenium/firefox:test",
  ] ])

```

## Objetivos

Esto pone de relieve la mayoría de los conceptos clave. En primer lugar, declara **objetivo**, en este caso hay un único objetivo `java_test`.
Cada objetivo tiene un atributo `name`.

### Target Names

La combinación de la ubicación del archivo "build.desc" y el nombre se utilizan para derivar las tareas de rake que se generan. Todos los nombres de tareas tienen el prefijo "//" seguido de la ruta al directorio que contiene la "compilación". esc" en relación al archivo `Rakefile`, seguido de un ":" y luego el nombre del objetivo dentro del "build.desc". Un ejemplo hace esto mucho más claro :)

La tarea de rake generada por este ejemplo es `//java/client/test/org/openqa/selenium:single`

### Nombres de objetivo corto

Como un acceso directo, si un destino recibe el nombre del directorio que contiene la "compilación". archivo esc", puede omitir la parte del nombre de la tarea rastrera después de los dos puntos. En nuestro ejemplo: `//java/server/src/org/openqa/selenium/server` es el mismo que `//java/server/src/org/openqa/selenium/server:server`.

### Objetivos implícitos

Algunas reglas de construcción proveen objetivos implícitos y proporcionan extensiones relacionadas a un objetivo de construcción normal. Ejemplos incluyen generar archivos de código fuente o ejecutar pruebas. Estos se declaran añadiendo dos puntos y el nombre del objetivo implícito al nombre completo de una regla de construcción. En nuestro ejemplo, puedes ejecutar las pruebas usando "///java/client/test/org/openqa/selenium:single:run"

Cada una de las reglas descritas a continuación tiene una lista de objetivos implícitos que están asociados con ellos.

### Outputs

Cada objetivo especificado en un archivo "build.desc" produce una única salida. Esto es importante. Téngalo en mente. Generalmente, todos los archivos de salida se colocan en el directorio "build", en relación al nombre de la tarea Rake. En nuestro ejemplo, la salida de "//java/org/openqa/selenium/server" se encontraría en "build/java/org/openqa/selenium/server.jar". Las reglas de compilación deben mostrar los nombres y ubicaciones de cualquier archivo que generen.

### Dependencias

Eche un vistazo a la sección "deps" del objetivo "single" anterior. El `":tests"` es una referencia a un objetivo en el archivo actual "build.desc", en este caso, es un objetivo "java\_library" inmediatamente arriba. También verá que hay una referencia a varios caminos completos. Por ejemplo `"//java/server/src/org/openqa/selenium/server"` Esto se refiere a otro objetivo definido en un archivo build.desc divertido crazy.

### Browsers

Las reglas py\_test y js\_test tienen un manejo especial para ejecutar las mismas pruebas en varios navegadores.  Los meta-datos relevantes específicos del navegador se mantienen en rake-tasks/browsers.rb.  La forma general de usar esto es añadir `_`browsername al nombre de destino; sin el sufijo `_`browsername las pruebas se ejecutarán para todos los navegadores.

Por ejemplo, si teníamos una regla js\_test //foo/bar, ejecutaríamos sus pruebas en firefox ejecutando el objetivo //foo/bar\_ff:run o ejecutaríamos todos los navegadores disponibles ejecutando el objetivo //foo/bar:run

## Construir objetivos

Puedes listar todos los objetivos de construcción usando la opción `-T`. ej.

```
./go -T
```

Ser una breve descripción de los objetivos disponibles que usted puede utilizar.

### Atributos comunes

Se requieren los siguientes atributos para todos los objetivos de construcción:

| **Nombre de Atributo** | **Type** | **Extensión**                                                                                                  |
| :--------------------- | :------- | :------------------------------------------------------------------------------------------------------------- |
| nombre                 | cadena   | Utilizado para derivar el destino del rastrillo y (a menudo) el nombre del binario generado |

Los siguientes atributos se utilizan comúnmente:

| **Nombre de Atributo** | **Type** | **Extensión**                             |
| :--------------------- | :------- | :---------------------------------------- |
| srcs                   | matriz   | La fuente sin procesar para este objetivo |
| deps                   | matriz   | Prerrequisitos de este objetivo           |

### librería\_java

- **Salida:** archivo JAR con el nombre del atributo "nombre" si el atributo "srcs" está establecido.
- **Objetivos implícitos:** ejecutar (si especifica el atributo "principal"), proyecto, project-srcs, uber, zip
- **Atributos requeridos:** "nombre" y al menos uno de "srcs" o "deps".

| **Nombre de Atributo** | **Type** | **Extensión**                                                                                           |
| :--------------------- | :------- | :------------------------------------------------------------------------------------------------------ |
| deps                   | matriz   | Como arriba                                                                                             |
| srcs                   | matriz   | Como arriba                                                                                             |
| recursos               | matriz   | Cualquier recurso que debería ser copiado en el archivo jar .                           |
| principal              | cadena   | El nombre completo de la clase principal del jar (usado para crear jars ejecutables) |

### java\_test

- **Salida:** archivo JAR con el nombre del atributo "nombre" si el atributo "srcs" está establecido.
- **Objetivos implícitos:** ejecución, proyecto, project-srcs, uber, zip
- **Atributos requeridos:** "nombre" y al menos uno de "srcs" o "deps".

| **Nombre de Atributo** | **Type** | **Extensión**                                                                    |
| :--------------------- | :------- | :------------------------------------------------------------------------------- |
| deps                   | matriz   | Como arriba.                                                     |
| srcs                   | matriz   | Como arriba.                                                     |
| recursos               | matriz   | Cualquier recurso que debería ser copiado en el archivo jar .    |
| principal              | cadena   | La clase alternativa a usar para ejecutar estas pruebas.         |
| args                   | cadena   | La línea de argumento a pasar a la clase principal                               |
| propiedades            | matriz   | Una matriz de mapas que contienen propiedades del sistema que deben establecerse |

### js\_deps

- **Salida:** Archivo marcador para indicar que la tarea está actualizada.
- **Objetivos implícitos:** Ninguno
- **Atributos requeridos:** "nombre" y "srcs"

| **Nombre de Atributo** | **Type** | **Extensión** |
| :--------------------- | :------- | :------------ |
| nombre                 | cadena   | Como arriba   |
| srcs                   | matriz   | Como arriba   |
| deps                   | matriz   | Como arriba   |

### js\_binario

- **Salida:** Un archivo JS monolítico que contiene todas las dependencias y fuentes compiladas usando el compilador de cierre sin optimizaciones.
- **Objetivos implícitos:** Ninguno
- **Atributos requeridos:** Al menos uno de srcs o deps.

| **Nombre de Atributo** | **Type** | **Extensión** |
| :--------------------- | :------- | :------------ |
| nombre                 | cadena   | Como arriba   |
| srcs                   | matriz   | Como arriba   |
| deps                   | matriz   | Como arriba   |

### js\_fragment

- **Salida:** Fuente de una función anónima que representa la función exportada, compilada por el compilador de cierre con todas las optimizaciones encendidas.
- **Objetivos implícitos:** Ninguno
- **Atributos requeridos:** nombre, módulo, función, deps

| **Nombre de Atributo** | **Type** | **Extensión**                                |
| :--------------------- | :------- | :------------------------------------------- |
| nombre                 | cadena   | Como arriba                                  |
| módulo                 | cadena   | El nombre del módulo que contiene la función |
| función                | cadena   | El nombre completo de la función a exportar  |
| deps                   | matriz   | Como arriba                                  |

### js\_fragment\_header

- **Salida:** Un archivo de cabecera C con todas las dependencias js\_fragment declaradas como constantes.
- **Objetivos implícitos:** Ninguno
- **Atributos requeridos:** nombre, deps

| **Nombre de Atributo** | **Type** | **Extensión** |
| :--------------------- | :------- | :------------ |
| nombre                 | cadena   | Como arriba   |
| srcs                   | matriz   | Como arriba   |
| deps                   | matriz   | Como arriba   |

### js\_test

- **Salida:**
- **Objetivos implícitos:** `_`BROWSER:run, ejecutar
- **Atributos requeridos:** Ninguno.

| **Nombre de Atributo** | **Type** | **Extensión**                                                                                                                                                                                                                                                                                                                                    |
| :--------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| deps                   | matriz   | Como arriba.                                                                                                                                                                                                                                                                                                                     |
| srcs                   | matriz   | Como arriba.                                                                                                                                                                                                                                                                                                                     |
| ruta                   | cadena   | La ruta en la que esperar que los archivos de prueba se alojen en el servidor de pruebas.                                                                                                                                                                                                                                        |
| browsers               | matriz   | Lista de navegadores, desde rake\_tasks/browsers.rb, para ejecutar las pruebas.  Sólo intentará ejecutar pruebas en aquellos navegadores que estén disponibles en el sistema.  Si no es así, el valor predeterminado de todos los navegadores del sistema. |

Suponiendo que los navegadores = ['ff', 'chrome'], para el objetivo //foo, se generarán los objetivos implícitos: //foo\_ff:run y /foo\_chrome:run, que ejecutan las pruebas en cada uno de esos navegadores, y se generará el objetivo implícito //foo:run, que ejecuta las pruebas tanto en ff como en chrome.

### py\_test

- **Salida:** Crea la estructura de directorios requerida para ejecutar las pruebas de python listadas.
- **Objetivos implícitos:** `_`BROWSER:run, ejecutar
- **Atributos requeridos:** nombre.

| **Nombre de Atributo**                                               | **Type** | **Extensión**                                                                                                                                                                                                                                                                                                                                    |
| :------------------------------------------------------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| deps                                                                 | matriz   | Otras reglas de py\_test, cuyas pruebas también deben ser ejecutadas.                                                                                                                                                                                                                                      |
| pruebas comunes                                                      | matriz   | Probar archivo(s) para ejecutarse en todos los navegadores.  Estas pruebas se pasarán a través de una plantilla, con sustitutos específicos del navegador, para que estén correctamente listados para cada navegador en el árbol de archivos de salida de python.                             |
| BROWSER\_specific\_tests | matriz   | Probar archivo(s) para ejecutarse sólo en BROWSER.                                                                                                                                                                                                                                                            |
| recursos                                                             | matriz   | Recursos que deben ser copiados a la estructura de directorios de python.                                                                                                                                                                                                                                                        |
| browsers                                                             | matriz   | Lista de navegadores, desde rake\_tasks/browsers.rb, para ejecutar las pruebas.  Sólo intentará ejecutar pruebas en aquellos navegadores que estén disponibles en el sistema.  Si no es así, el valor predeterminado de todos los navegadores del sistema. |

Nota: Cada invocación de py\_test se realiza en un nuevo virtualenv.

### rake\_task

- **Salida:** Una regla de construcción divertida que puede ser referida a "golpear el escape" y usar blancos de rastrillo ordinarios.
- **Objetivos implícitos:** Ninguno
- **Atributos requeridos:** nombre, tarea\_name, out.

| **Nombre de Atributo**            | **Type** | **Extensión**                                  |
| :-------------------------------- | :------- | :--------------------------------------------- |
| nombre                            | cadena   | Como arriba                                    |
| tarea\_name | cadena   | El objetivo de rastrillo ordinario a llamar    |
| fuera                             | cadena   | El archivo que se genera, relativo al Rakefile |

### gcc\_librería

- **Salida:** Archivo de librería compartido con el nombre del atributo "nombre" si el atributo "srcs" está establecido.
- **Objetivos implícitos:** Ninguno.
- **Atributos requeridos:** "nombre" y "srcs".

| **Nombre de Atributo**           | **Type** | **Extensión**                                                                                |
| :------------------------------- | :------- | :------------------------------------------------------------------------------------------- |
| srcs                             | matriz   | Como arriba                                                                                  |
| arco                             | cadena   | "amd64" para compilaciones de 64 bits, "i386" para compilaciones de 32 bits. |
| args                             | cadena   | Argumentos al compilador (-I banderas, por ejemplo).      |
| link\_args | cadena   | Argumentos al enlazador (banderas -l, por ejemplo)                        |

Nota: Cuando se construye una nueva biblioteca por primera vez, la compilación tendrá éxito, pero la copia precompilada fallará con un mensaje similar:

```
cp build/cpp/amd64/libimetesthandler64.so 
abortado!
no puede convertir nil en String
```

Solución: Copie la librería justt-built a la carpeta precompilada apropiada (cpp/prebuilt/arch/).
