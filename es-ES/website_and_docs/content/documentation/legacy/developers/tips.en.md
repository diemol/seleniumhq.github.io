---
title: Consejos de Desarrollador
linkTitle: Consejos
weight: 10
description: |
  Detalles sobre cómo ejecutar Selenium Test Suite con Crazy Fun.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Developer-Tips)

## Ejecutando una prueba individual

Al desarrollar WebDriver, es común querer ejecutar una sola prueba en lugar de toda la suite de pruebas para un controlador en particular.

Puede ejecutar todas las pruebas en una clase de prueba dada de esta manera:

```
./go test_firefox onlyRun=CombinedInputActionsTest
```

También puede ejecutar una sola prueba directamente desde la línea de comandos escribiendo:

```
./go método test_firefox=foo
```

## No hay alboroto en errores o fallos

La suite de pruebas se detendrá por defecto en errores y fallos.  Puedes desactivar este comportamiento estableciendo las variables de entorno `haltonerror` o `haltonfailure` a `0`.

## Revisando los registros de las pruebas

Cuando ejecuta las pruebas, los resultados de las pruebas no aparecen en la pantalla. Están escritos en la carpeta \`./build/test\_logs'. Un par de archivos están escritos. Sus nombres son relativamente consistentes e incluyen los detalles de las pruebas ejecutadas. El par comprende un archivo txt y un archivo xml. El archivo xml contiene más información sobre el entorno de ejecución como la ruta, la versión Ant, etc. Estos archivos se sobrescriben la próxima vez que se ejecute el mismo objetivo de prueba, por lo que puede querer archivar los resultados si son importantes para usted.

## Usando Rake

Rake es muy similar a usar otras herramientas de compilación como "make" o "ant". Puede especificar un "objetivo" a ejecutar añadiéndolo como parámetro, y puede añadir más de un objetivo a la vez. Tenga en cuenta que dado que WebDriver no se basa en la instalación de ruby y utiliza JRuby, rake **no** debe involucrarse directamente - utilice el script _go_ en su lugar. Por ejemplo, para limpiar la compilación y luego construir y ejecutar las pruebas HtmlUnitDriver:

```
./go limpia test_htmlunit
```

El objetivo por defecto que se utiliza compilará el código y ejecutará todas las pruebas. Objetivos más interesantes son:

| **Target**                             | **Descripción**                                                                                                                                                                                                                     |
| :------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| limpiar                                | Eliminar el contenido del directorio de compilación, eliminando todos los artefactos compilados                                                                                                                                     |
| prueba                                 | Compilar las dependencias y ejecutar todas las pruebas para el HtmlUnitDriver, FirefoxDriver, InternetExplorerDriver así como las pruebas de la biblioteca de soporte                                                               |
| firefox                                | Compilar FirefoxDriver                                                                                                                                                                                                              |
| htmlunit                               | Compilar el HtmlUnitDriver                                                                                                                                                                                                          |
| es                                     | Compila el InternetExplorerDriver. Esto no compilará el C++ en un sistema que no sea Windows, pero siempre compilará el Java, sin importar qué sistema operativo esté usando                                        |
| soporte                                | Adivina lo que hace esto :)                                                                                                                                                                                         |
| prueba\_htmlunit | Compila las dependencias y luego ejecute las pruebas para el HtmlUnitDriver. Se puede seguir el mismo patrón "test\_x" para todos los objetivos de compilación en esta tabla. |

### Ejecutar un depurador remoto con pruebas Java

Puede ejecutar las pruebas en modo de depuración y esperar a un detector java remoto (que se configuraría en eclipse o intellij).

```
./go debug=true suspend=true test_firefox
```

## Depurando el Firefox Driver

### Obteniendo salida del propio proceso de Firefox

Esto suele ser útil para depurar problemas al iniciar Firefox. La propiedad del sistema Java `webdriver.firefox.logfile` indicará al FirefoxDriver que redireccione la salida a un archivo:

```
java -Dwebdriver.firefox.logfile=/dev/stdout -cp selenium-2.jar <sometest>
```

### Salida a la consola de errores

Una técnica común usada para depurar la extensión del controlador Firefox son las sentencias de depuración. Los dos siguientes métodos se pueden utilizar desde casi cualquier código Javascript dentro de la extensión:

- `Logger.dumpn()` - Registra una cadena en consola (y convierte argumentos en cadenas). Por ejemplo: `Logger.dumpn("Found element: " + node)`.
- `Logger.dump()` - Obtiene un solo argumento, un objeto, y vuelca todo su contenido: interfaces implementadas, campos de datos, métodos, etc.

### Obteniendo salida de la consola de error a un archivo

Para ver la salida generada usando la utilidad `Logger`, se tiene que abrir la consola de error de Firefox, difícil o simplemente imposible en máquinas remotas. Afortunadamente, hay una forma de obtener el contenido de la salida volcada a un archivo:

```
FirefoxProfile p = new FirefoxProfile();
p.setPreference("webdriver.log.file", "/tmp/firefox_console");
controlador WebDriver = new FirefoxDriver(p);
...
```

La preferencia `webdriver.log.file` indicará al `Logger` volcar todos los contenidos de la consola al archivo especificado.
archivo webdriver.log.file

### Obteniendo aún más salida a la línea de comandos

Al sospechar que el registro adicional desde Firefox podría ser beneficioso, se puede crank el nivel de depuración hasta el momento:

```
exportar NSPR_LOG_MODULES=all:3
```

Configurar esta variable de entorno hará que Firefox registre mensajes adicionales en la consola. Utilice esta variable de entorno junto con `webdriver.firefox.logfile` para mantener la salida de Firefox en la consola.

## Depurar el controlador de Internet Explorer

Para obtener información detallada de IEDriverServer. xe puede ejecutar pruebas con la opción devMode=true, esta opción establecerá el nivel de registro a DEBUG y redirigirá la salida de registro al archivo iedriver.log

```
./go test_ie devMode=true
```

## Agregando una prueba

La mayoría de los casos de prueba de WebDriver viven bajo java/client/test/org/openqa/selenium. Por ejemplo, para demostrar un problema haciendo clic en los elementos, se debe añadir un caso de prueba a ClickTest. Los casos de prueba ya tienen una instancia del controlador - no es necesario crear uno.
La prueba utiliza páginas que son servidas por un servidor en proceso, servidas desde common/src/web. Sus URLs son proporcionadas por la clase Pages, así que al añadir una página y añadirla a la clase Pages también.

## Interactuando manualmente con `RemoteWebDriverServer`

Podemos utilizar un navegador web o herramientas como telnet para interactuar con un RemoteWebDriverServer, por ejemplo, para depurar el protocolo JSON. Aquí hay un simple ejemplo de comprobación del estado de un servidor instalado en la máquina local

En un navegador web

```
http://localhost:8080/wd/hub/status/

```

En telnet

```
telnet localhost 8080

GET /wd/hub/status/ HTTP/1.0

```

En Macs y Unix en general intente `curl`

```
curl  http://localhost:8080/wd/hub/status
```

Y en linux `wget`

```
wget http://localhost:8080/wd/hub/status
```

En todos estos casos, el RemoteWebDriverServer debe responder con

```

{status:0} 

```
