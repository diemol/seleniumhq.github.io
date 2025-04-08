---
title: Servidor de controlador IE
linkTitle: Servidor de controlador IE
weight: 8
description: |
  El controlador de Internet Explorer es un servidor independiente que implementa la especificación WebDriver.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/InternetExplorerDriver-Internals)

El `InternetExplorerDriver` es un servidor independiente que implementa el protocolo wire de WebDriver.
Este controlador ha sido probado con IE 11, y en Windows 10. Puede funcionar con versiones anteriores
de IE y Windows, pero esto no es compatible.

El controlador soporta versiones de 32-bit y 64-bit del navegador. La elección de cómo
determinar qué "bit-ness" usar al ejecutar el navegador depende de qué versión del
IEDriverServer.exe es lanzada. Si la versión de 32 bits de `IEDriverServer.exe` es lanzada,
la versión de 32 bits de IE será lanzada. De la misma manera, si se lanza la versión de 64 bits de
IEDriverServer.exe, se lanzará la versión de 64 bits de IE.

## Instalando

No necesita ejecutar un instalador antes de usar el `InternetExplorerDriver`, aunque se requiere alguna configuración
. El ejecutable del servidor independiente debe descargarse desde
la página [Downloads](https://www.selenium.dev/downloads/) y colocarse en tu
[PATH](http://en.wikipedia.org/wiki/PATH_\(variable\)).

## Pros

- Ejecuta en un navegador real y soporta JavaScript

## Contra

- Obviamente, el InternetExplorerDriver sólo funcionará en Windows!
- Comparativamente lento (aunque todavía bastante snappy :)

## Cambios de línea de comandos

Como un ejecutable independiente, el comportamiento del controlador IE puede ser modificado a través de varios argumentos
en la línea de comandos. To set the value of these command-line arguments, you should
consult the documentation for the language binding you are using. Los interruptores
de línea de comandos soportados se describen en la tabla de abajo. Todos -`<switch>`, --`<switch>`
y /`<switch>` son compatibles.

| Cambiar                         | Comenzando                                                                                                                                                                                                                                           |
| :------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| --port=`<portNumber>`           | Especifica el puerto en el que el servidor HTTP del controlador IE escuchará comandos de enlaces de idioma. Por defecto es 5555.                                                                                     |
| --host=`<hostAdapterIPAddress>` | Especifica la dirección IP del adaptador de host en el que el servidor HTTP del controlador IE escuchará comandos desde enlaces de idioma. Por defecto es 127.0.0.1. |
| --log-level=`<logLevel>`        | Especifica el nivel en el que los mensajes de registro son salidos. Los valores válidos son FATAL, ERROR, WARN, INFO, DEBUG y TRACE. Por defecto es FATAL.                                           |
| --log-file=`<logFile>`          | Especifica la ruta completa y el nombre del archivo de registro. Defaults to stdout.                                                                                                                                 |
| --extract-path=`<path>`         | Especifica la ruta completa al directorio utilizado para extraer los archivos utilizados por el servidor. Por defecto es el directorio TEMP si no se especifica.                                                     |
| --silencioso                    | Suprime la salida de diagnóstico cuando se inicia el servidor.                                                                                                                                                                       |

## Propiedades del sistema importantes

Las siguientes propiedades del sistema (lea usando `System.getProperty()` y establezca usando
`System. etProperty()` en código Java o la bandera de línea de comandos "`-DpropertyName=value`)
son usadas por el `InternetExplorerDriver`:

| **Propiedad**                     | **Lo que significa**                                                                                                                                                                                       |
| :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `webdriver.ie.driver`             | La ubicación del binario del conductor IE.                                                                                                                                                 |
| `webdriver.ie.driver.host`        | Especifica la dirección IP del adaptador de host en el que el controlador IE escuchará.                                                                                                    |
| `webdriver.ie.driver.loglevel`    | Especifica el nivel en el que los mensajes de registro son salidos. Los valores válidos son FATAL, ERROR, WARN, INFO, DEBUG y TRACE. Por defecto es FATAL. |
| `webdriver.ie.driver.logfile`     | Especifica la ruta completa y el nombre del archivo de registro.                                                                                                                           |
| `webdriver.ie.driver.silent`      | Suprime la salida de diagnóstico cuando se inicia el controlador IE.                                                                                                                       |
| `webdriver.ie.driver.extractpath` | Especifica la ruta completa al directorio utilizado para extraer los archivos utilizados por el servidor. Por defecto es el directorio TEMP si no se especifica.           |

## Configuración requerida

- El ejecutable `IEDriverServer` debe ser [downloaded](https://www.selenium.dev/downloads/) y colocarse en tu [PATH](http://en.wikipedia.org/wiki/PATH_\(variable\)).
- En IE 7 o superior en Windows Vista, Windows 7 o Windows 10, debe configurar los ajustes del Modo Protegido para que cada zona sea el mismo valor. El valor puede estar encendido o apagado, siempre y cuando sea el mismo para cada zona. Para configurar la configuración del Modo Protegido, seleccione "Opciones de Internet..." en el menú Herramientas y haga clic en la pestaña Seguridad. Para cada zona, habrá una casilla de verificación en la parte inferior de la pestaña "Activar modo protegido".
- Además, el "Modo Protegido Mejorado" debe estar desactivado para IE 10 o superior. Esta opción se encuentra en la pestaña Avanzada del diálogo Opciones de Internet.
- El nivel de zoom del navegador debe ajustarse al 100% para que los eventos nativos del ratón puedan ajustarse a las coordenadas correctas.
- Para Windows 10, también necesita configurar "Cambiar el tamaño de texto, aplicaciones y otros elementos" al 100% en la configuración de la pantalla.
- Para IE 11 _only_, necesitará establecer una entrada de registro en el equipo de destino para que el controlador pueda mantener una conexión a la instancia de Internet Explorer que crea. Para instalaciones Windows de 32 bits, la clave que debe examinar en el editor de registro es `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer\Main\FeatureControl\FEATURE_BFCACHE`. Para instalaciones Windows de 64 bits, la clave es `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Internet Explorer\Main\FeatureControl\FEATURE_BFCACHE`. Tenga en cuenta que la subclave `FEATURE_BFCACHE` puede o no estar presente, y debe ser creada si no está presente. **Importante:** Dentro de esta clave, crea un valor DWORD llamado `iexplore.exe` con el valor de 0.

## Eventos nativos e Internet Explorer

Como el `InternetExplorerDriver` es sólo para Windows, intenta usar los eventos llamados "nativos", o de nivel de SO
para realizar operaciones de ratón y teclado en el navegador. This is in contrast to using
simulated JavaScript events for the same operations. The advantage of using native events is that
it does not rely on the JavaScript sandbox, and it ensures proper JavaScript event propagation
within the browser. Sin embargo, actualmente hay algunos problemas con los eventos del ratón cuando la ventana del navegador IE
no tiene enfoque, y al intentar pasar el cursor sobre los elementos.

### Enfoque del navegador

El reto es que el propio IE parece no respetar totalmente los mensajes de Windows que enviamos a la ventana del navegador
IE (`WM\_MOUSEDOWN` y `WM\_MOUSEUP`) si la ventana no tiene el foco.
Específicamente, el elemento en el que se hace clic recibirá una ventana de enfoque a su alrededor, pero el elemento no procesará el clic
. Posiblemente, no deberíamos enviar mensajes; Más bien,
deberíamos estar usando la API `SendInput()`, pero esa API requiere explícitamente que la ventana tenga el foco
. Tenemos dos objetivos contradictorios con el proyecto WebDriver .

En primer lugar, nos esforzamos por emular al usuario lo más cerca posible. Esto significa usar eventos nativos
en lugar de simular los eventos usando JavaScript.

En segundo lugar, queremos no requerir que el foco de la ventana del navegador sea automatizado. Esto significa que
solo forzar la ventana del navegador al primer plano es subóptimo.

Una consideración adicional es la posibilidad de múltiples instancias de IE ejecutándose bajo múltiples instancias de WebDriver
, lo que significa que cualquier solución "traer la ventana al primer plano" tendrá que envolver
en algún tipo de construcción sincronizadora (mutex?) dentro del código
C++ del controlador IE. Aún así, este código seguirá estando sujeto a condiciones de carrera si, por ejemplo, el usuario
trae otra ventana al primer plano entre el controlador trayendo IE al primer plano
y ejecutando el evento nativo.

The discussion around the requirements of the driver and how to prioritize these two
conflicting goals is ongoing. La sabiduría predominante es dar prioridad a la primera sobre
la segunda, y documenta que su máquina no estará disponible para otras tareas cuando utilice
el controlador IE. Sin embargo, esa decisión dista mucho de estar ultimada, y el código para implementarla es
probable que sea bastante complicado.

### Pasando por encima de elementos

Cuando intentas pasar el cursor sobre los elementos, y el cursor físico del ratón está dentro de los límites
de la ventana del navegador IE, el ratón no funcionará. Más específicamente, aparecerá
para trabajar durante una fracción de segundo, y luego el elemento volverá a su estado
anterior. La teoría predominante por qué ocurre esto es que IE está haciendo pruebas de impacto de algún tipo
durante su bucle de eventos, lo cual hace que responda a la posición física del ratón cuando el cursor físico
está dentro de los límites de la ventana. El equipo de desarrollo de WebDriver no ha podido descubrir
una solución para este comportamiento de IE.

### Haciendo clic en `<option>` Elementos o Enviando Formularios y `alert()`

Hay dos lugares donde el conductor de IE no interactúa con elementos utilizando eventos nativos.
Esto está haciendo clic en `<option>` elementos dentro de un elemento `<select>. Bajo circunstancias normales, 
el controlador IE calcula dónde hacer clic en base a la posición y tamaño del elemento, típicamente 
como es devuelto por el método de JavaScript `getBoundingClientRect()`. Sin embargo, para ` elementos<option>`, 
`getBoundingClientRect()`devuelve un rectángulo con posición cero y tamaño cero. El controlador IE 
gestiona este escenario usando el Atomo de Automatización`click()`, que esencialmente establece 
el `. elegido`propiedad del elemento y simula el evento`onChange`en JavaScript. 
Sin embargo, esto significa que si el evento`onChange`del elemento`<select>`contiene el código JavaScript 
que llama a`alert()`, `confirm()`o`prompt()`, llamando al método `click()\` de WebElement
colgará hasta que el diálogo modal sea manualmente descartado. No hay ninguna solución alternativa conocida para este comportamiento
usando solo el código WebDriver

Del mismo modo, hay algunos escenarios al enviar un formulario HTML a través del método `submit()`
de WebElement puede tener el mismo efecto. Esto puede suceder si el controlador llama a la función JavaScript `submit()`
en el formulario, y hay un controlador de eventos onSubmit que llama a las funciones de JavaScript `alert()`,
`confirm()`, o `prompt()`.

Esta restricción se presenta como el número 3508 (en Google Code).

## Múltiples instancias de `InternetExplorerDriver`

Con la creación del `IEDriverServer.exe`, debería ser posible crear y utilizar múltiples instancias
simultáneas del `InternetExplorerDriver`. Sin embargo, esta funcionalidad está en gran medida
no probada, y puede haber problemas con las cookies, el enfoque de la ventana y cosas por el estilo. Si intentas
usar múltiples instancias del controlador IE, y chocar con estos problemas, considera usar el `RemoteWebDriver`
y máquinas virtuales.

Hay dos soluciones para problemas con las cookies (y otros elementos de sesión) compartidos entre
múltiples instancias de InternetExplorer.

La primera es iniciar InternetExplorer en modo privado. Después de eso, InternetExplorer comenzará
con datos de sesión limpios y no guardará los datos de sesión cambiados al salir. To do so you
need to pass 2 specific capabilities to driver: `ie.forceCreateProcessApi` with `true` value
and `ie.browserCommandLineSwitches` with `-private` value. Ten en cuenta que solo funcionará
para InternetExplorer 8 y posterior, y el Registro de Windows
`HKLM_CURRENT_USER\\Software\\Microsoft\\Internet Explorer\\Main` ruta debe contener la clave
`TabProc.` con valor `0`.

La segunda es limpiar la sesión durante el inicio de InternetExplorer. For this you need to pass
specific `ie.ensureCleanSession` capability with `true` value to driver. Esto elimina la caché
para todas las instancias en ejecución de InternetExplorer, incluyendo las iniciadas manualmente.

## Ejecutando `IEDriverServer.exe` remotamente

The HTTP server started by the `IEDriverServer.exe` sets an access control list to only accept
connections from the local machine, and disallows incoming connections from remote machines.
En la actualidad, esto no se puede cambiar sin modificar el código fuente al `IEDriverServer.exe`.
Para ejecutar el controlador Internet Explorer en una máquina remota, usar el servidor remoto independiente Java
en conexión con el equivalente de su enlace de idioma de `RemoteWebDriver`.

## Ejecutar `IEDriverServer.exe` bajo un Servicio de Windows

Intentar utilizar IEDriverServer.exe como parte de una aplicación de Servicio de Windows es expresamente
no compatible. Los procesos de servicio, y los procesos generados por ellos, tienen unos requisitos
muy diferentes que los que se ejecutan en un contexto de usuario regular. `IEDriverServer. xe` no está probado explícitamente en
ese entorno, e incluye llamadas API de Windows que están documentadas para ser prohibidas para ser utilizadas
en procesos de servicio. While it may be possible to get the IE driver to work while running under
a service process, users encountering problems in that environment will need to seek out their
own solutions.
