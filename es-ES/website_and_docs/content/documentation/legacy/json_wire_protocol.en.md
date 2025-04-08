---
title: Especificación del protocolo JSON Wire
linkTitle: JSON Wire Protocol
weight: 10
description: |
  Los endpoints y cargas útiles para el protocolo de código abierto ahora obsoleto que era el precursor de la [especificación W3C](https://w3c.github.io/webdriver/).
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol)

Todas las implementaciones de WebDriver que se comuniquen con el navegador, o un servidor RemoteWebDriver usarán un protocolo de cable común. Este protocolo de cable define un [RESTful web service](http://www.google.com?q=RESTful+web+service) usando [JSON](http://www.json.org) sobre HTTP.

El protocolo asumirá que la API de WebDriver ha sido "aplanada", pero hay una expectativa de que las implementaciones de clientes tomen un enfoque más orientado a objetos, como se demuestra en la API de Java existente. El protocolo wire está implementado en los pares de peticiones/respuesta de "comandos" y "respuestas".

## Términos y conceptos

### Cliente

La máquina en la que se está utilizando la API de WebDriver.<br><br>

### Sesión

La máquina ejecutando el RemoteWebDriver. Este término también puede referirse a un navegador específico que implementa directamente el protocolo de cable, como el FirefoxDriver o IPhoneDriver.<br><br>

El servidor debe mantener un navegador por sesión. Los comandos enviados a una sesión serán redireccionados al navegador correspondiente.<br><br>

### Elemento web

Un objeto en la API de WebDriver que representa un elemento DOM en la página.<br><br>

### Objeto JSON WebElement

La representación JSON de un WebElement para la transmisión a través del cable. Este objeto tendrá las siguientes propiedades:<br><br>

| **Clave** | **Type** | **Descripción**                                                                                                                                                               |
| --------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ELEMENCIA | cadena   | El ID opaco asignado al elemento por el servidor. Este ID debe ser utilizado en todos los comandos subsiguientes emitidos contra el elemento. |

### Capacidades JSON objeto

No todas las implementaciones del servidor soportarán todas las funciones de WebDriver . Por lo tanto, el cliente y el servidor deben usar objetos JSON con las propiedades listadas a continuación al describir qué características soporta una sesión. <br><br>

<table><thead><tr><th><b>Tecla</b> </th><th><b>Tipo</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> nombre del navegador </td><td> cadena      </td><td> El nombre del navegador que se está usando; debe ser uno de <code> {android, chrome, firefox, htmlunit, explorador de Internet, iPhone, iPad, opera, safari}</code>. </td></tr>
<tr><td> versión    </td><td> cadena      </td><td> La versión del navegador, o la cadena vacía si se desconoce. </td></tr>
<tr><td> plataforma   </td><td> cadena      </td><td> Una clave especificando en qué plataforma se está ejecutando el navegador. Este valor debe ser uno de <code>{WINDOWS|XP|VISTA|MAC|LINUX|UNIX}</code>. Al solicitar una sesión nueva, el cliente puede especificar <code>TOY</code> para indicar que se puede utilizar cualquier plataforma disponible. </td></tr>
<tr><td> javascriptActivado </td><td> boolean     </td><td> Si la sesión soporta la ejecución de JavaScript suministrado por el usuario en el contexto de la página actual. </td></tr>
<tr><td> capturas de pantalla </td><td> boolean     </td><td> Si la sesión soporta la toma de capturas de pantalla de la página actual. </td></tr>
<tr><td> alertas de handles </td><td> boolean     </td><td> Si la sesión puede interactuar con ventanas emergentes modales, como <code>window.alert</code> y <code>window.confirm</code>. </td></tr>
<tr><td> base de datos habilitada </td><td> boolean     </td><td> Si la sesión puede interactuar con el almacenamiento de la base de datos. </td></tr>
<tr><td> ubicaciónContexto activado </td><td> boolean     </td><td> Si la sesión puede establecer y consultar el contexto de ubicación del navegador. </td></tr>
<tr><td> aplicaciónCacheActivada </td><td> boolean     </td><td> Si la sesión puede interactuar con la caché de la aplicación. </td></tr>
<tr><td> navegador conectado </td><td> boolean     </td><td> Si la sesión puede consultar la conectividad del navegador y desactivarla si lo desea. </td></tr>
<tr><td> cssSelectores habilitados </td><td> boolean     </td><td> Si la sesión soporta selectores CSS al buscar elementos. </td></tr>
<tr><td> web Almacenamiento Activado </td><td> boolean     </td><td> Si la sesión soporta interacciones con <a href='http://www.w3.org/TR/2009/WD-webstorage-20091029/'>objetos de almacenamiento</a>. </td></tr>
<tr><td> rotable  </td><td> boolean     </td><td> Si la sesión puede girar la disposición actual de la página entre las orientaciones de retrato y paisaje (sólo se aplica a las plataformas móviles). </td></tr>
<tr><td> aceptar Certs </td><td> boolean     </td><td> Si la sesión debe aceptar todos los certificados SSL por defecto. </td></tr>
<tr><td> eventos nativos </td><td> boolean     </td><td> Si la sesión es capaz de generar eventos nativos al simular la entrada del usuario. </td></tr>
<tr><td> proxy      </td><td> objeto proxy </td><td> Detalles de cualquier proxy a utilizar. Si no se especifica ningún proxy, sea cual sea el estado actual o predeterminado del sistema. El formato se especifica bajo Objeto JSON Proxy. </td></tr>
<tr><td> Alerta inesperada </td><td> cadena     </td><td> Qué debería hacer el navegador con una alerta no controlada antes de lanzar la UnhandledAlertException. Los valores posibles son "aceptar", "descartar" e "ignorar" </td></tr>
<tr><td> elementScrollBehavior      </td><td> entero </td><td> Permite al usuario especificar si los elementos se desplazan a la vista para que la interacción se alinee con la parte superior (0) o la parte inferior (1) de la ventana. El valor por defecto es alinearse con la parte superior de la ventana gráfica. Soportado en IE y Firefox (desde 2.36) </td></tr></tbody></table>

### Capacidades deseadas

Un objeto JSON de Capacidades enviado por el cliente describiendo las capacidades que debería poseer una nueva sesión creada por el servidor. Cualquier clave omitida indica implícitamente que la capacidad correspondiente es irrelevante. Más en <a href='DesiredCapabilities.md'>DesiredCapabilidades</a>. <br><br>

### Capacidades reales

Un objeto JSON de Capacidades devuelto por el servidor describiendo qué características realmente soporta una sesión.
Cualquier clave omitida indica implícitamente que la capacidad correspondiente no está soportada. <br><br>

### Cookie objeto JSON

Un objeto JSON que describe una Cookie.<br><br>

<table><thead><tr><th><b>Tecla</b> </th><th><b>Tipo</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> nombre       </td><td> cadena      </td><td> El nombre de la cookie. </td></tr>
<tr><td> valor      </td><td> cadena      </td><td> Valor de la cookie.  </td></tr>
<tr><td> ruta       </td><td> cadena      </td><td> (Opcional) La ruta de las cookies.<sup>1</sup> </td></tr>
<tr><td> dominio     </td><td> cadena      </td><td> (Opcional) El dominio al que la cookie es visible.<sup>1</sup> </td></tr>
<tr><td> seguro     </td><td> boolean     </td><td> (Opcional) Si la cookie es una cookie segura.<sup>1</sup> </td></tr>
<tr><td> Sólo http   </td><td> boolean     </td><td> (Opcional) Si la cookie es una cookie httpOnly.<sup>1</sup> </td></tr>
<tr><td> expiry     </td><td> número      </td><td> (Opcional) Cuando la cookie caduque, se especifica en segundos desde medianoche, el 1 de enero de 1970 UTC.<sup>1</sup> </td></tr></tbody></table>

<sup>1</sup> When returning Cookie objects, the server should only omit an optional field if it is incapable of providing the information. <br><br>

### Registro entrada JSON Objeto

Un objeto JSON que describe una entrada de registro. <br><br>

<table><thead><tr><th><b>Tecla</b> </th><th><b>Tipo</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> fecha  </td><td> número      </td><td> La marca de tiempo de la entrada. </td></tr>
<tr><td> nivel      </td><td> cadena      </td><td> El nivel de registro de la entrada, por ejemplo, "INFO" (ver <a href='#Log_Levels.md'>niveles de registro</a>). </td></tr>
<tr><td> mensaje    </td><td> cadena      </td><td> El mensaje de registro.   </td></tr>
</tbody></table>

### Niveles de Log

Registra los niveles en orden, con el nivel más alto y más grueso en la parte inferior. <br><br>

<table><thead><tr><th><b>Nivel</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> TODO          </td><td> Todos los mensajes de registro. Utilizado para la obtención de registros y la configuración del registro. </td></tr>
<tr><td> DEBUG        </td><td> Mensajes para depuración. </td></tr>
<tr><td> INFO         </td><td> Mensajes con información de usuario. </td></tr>
<tr><td> ATENCIÓN      </td><td> Mensajes correspondientes a problemas no críticos. </td></tr>
<tr><td> AVISO       </td><td> Mensajes correspondientes a errores críticos. </td></tr>
<tr><td> DESACTIVADO          </td><td> No hay mensajes de registro. Utilizado para la configuración del registro. </td></tr>
</tbody></table>

### Tipo de Log

La siguiente tabla muestra los tipos de registro comunes. Otros tipos de registro, por ejemplo, para el registro de rendimiento también pueden estar disponibles. <br><br>

<table><thead><tr><th><b>Tipo de Log</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> cliente          </td><td> Registros del cliente. </td></tr>
<tr><td> conductor          </td><td> Registros del webdriver. </td></tr>
<tr><td> navegador         </td><td> Registros desde el navegador. </td></tr>
<tr><td> servidor          </td><td> Registros del servidor. </td></tr>
</tbody></table>

### Objeto JSON del proxy

Un objeto JSON que describe una configuración de proxy. <br><br>

<table><thead><tr><th><b>Tecla</b> </th><th><b>Tipo</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> proxyType  </td><td> cadena      </td><td> (Requerido) El tipo de proxy que se está usando. Los valores posibles son: <b>directo</b> - Una conexión directa - no hay proxy en uso <b>manual</b> - Configuración manual del proxy configurada, p.ej. establecer un proxy para HTTP, un proxy para FTP, etc, <b>pac</b> - Configuración automática del proxy desde una URL, <b>autodetectar</b> - Detección automática del proxy, probablemente con WPAD, <b>sistema</b> - Usar ajustes del sistema </td></tr>
<tr><td> proxyAutoconfigUrl </td><td> cadena      </td><td> (Requerida si proxyType == <b>pac</b>, Ignorada de otra manera) Especifica la URL que se utilizará para la configuración automática del proxy. Ejemplo de formato esperado: <a href='http://hostname.com:1234/pacfile'>http://hostname.com:1234/pacfile</a> </td></tr>
<tr><td> ftpProxy, httpProxy, sslProxy, socksProxy </td><td> cadena      </td><td> (Opcional, Ignorado si proxyType != <b>manual</b>) Especifica los proxies que se usarán para las solicitudes FTP, HTTP, HTTPS y SOCKS respectivamente. El comportamiento no está definido si se hace una solicitud, donde el proxy del protocolo en particular no está definido, si proxyType es <b>manual</b>. Ejemplo de formato esperado: hostname.com:1234 </td></tr>
<tr><td> socksUsername </td><td> cadena      </td><td> (Opcional, ignorado si proxyType != <b>manual</b> y socksProxy no está definido) Especifica el nombre de usuario del proxy SOCKS. </td></tr>
<tr><td> socksPassword </td><td> cadena      </td><td> (Opcional, ignorado si proxyType != <b>manual</b> y socksProxy no está definido) Especifica la contraseña del proxy SOCKS. </td></tr>
<tr><td> noProxy    </td><td> cadena      </td><td> (Opcional, ignorado si proxyType != <b>manual</b>) Especifica direcciones de bypass proxy. El formato es específico del controlador. </td></tr></tbody></table>

## Mensajes

### Comandos

Los mensajes de comando de WebDriver deben cumplir con la [especificación de solicitud HTTP/1.1](http://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html#sec5). Aunque el servidor puede ser extendido para responder a otros tipos de contenido, el protocolo de cable dicta que todos los comandos aceptan un tipo de contenido de `application/json;charset=UTF-8`. Del mismo modo, los cuerpos del mensaje para la solicitud POST y PUT deben usar un tipo de contenido `application/json;charset=UTF-8`.

Cada comando en el servicio WebDriver se asignará a un método HTTP en una ruta específica. Los segmentos de ruta con dos puntos (:) indican que el segmento es una variable usada para identificar aún más el recurso subyacente. Por ejemplo, considere un recurso arbitrario mapeado como:

```
Obtener /favorito/color/:name
```

Dado este mapeo, el servidor debe responder a las peticiones GET enviadas a "/favorite/color/Jack" y "/favorite/color/Jill", con la variable `:name` establecida a "Jack" y "Jill", respectivamente.

### Respuestas

Las respuestas de comando se enviarán como [mensajes de respuesta HTTP/1.1](http://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html#sec6). Si el servidor remoto debe devolver una respuesta 4xx, el cuerpo de respuesta tendrá un Tipo de Contenido de texto/plano y el cuerpo del mensaje será un mensaje descriptivo de la mala petición. Para todos los demás casos, si una respuesta incluye un cuerpo de mensajes, debe tener un tipo de contenido de aplicación/json; harset=UTF-8 y será un objeto JSON con las siguientes propiedades:

| **Clave**    | **Type** | **Descripción**                                                                                                                                |                                                                                                                                                                                                                                                                               |
| :----------- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Id de sesión | cadena   | nulo                                                                                                                                           | Un manejador opaco usado por el servidor para determinar dónde enrutar comandos específicos de sesión. Este ID debe incluirse en todos los comandos de sesión futuros en lugar de la variable de segmento de ruta :sessionId. |
| estado       | número   | Un código de estado que resume el resultado del comando. Un valor distinto a cero indica que el comando falló. |                                                                                                                                                                                                                                                                               |
| valor        | `*`      | El valor de respuesta JSON.                                                                                                    |                                                                                                                                                                                                                                                                               |

#### Respuesta de códigos de estado

El protocolo de cable heredará sus códigos de estado de los utilizados por el InternetExplorerDriver:

| **Código** | **Summary**                       | **Detalles**                                                                                                                                                                                   |
| :--------- | :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0          | `Éxito`                           | El comando se ha ejecutado correctamente.                                                                                                                                      |
| 6          | `NoSuchDriver`                    | Una sesión se ha terminado o no se ha iniciado                                                                                                                                                 |
| 7          | `No SuchElement`                  | Un elemento no pudo ser localizado en la página usando los parámetros de búsqueda dados.                                                                                       |
| 8          | `NoSuchFrame`                     | Una solicitud para cambiar a un marco no pudo ser satisfecha porque el marco no pudo ser encontrado.                                                                           |
| 9          | `Comando desconocido`             | El recurso solicitado no pudo ser encontrado, o una solicitud fue recibida usando un método HTTP que no es soportado por el recurso mapeado.                                   |
| 10         | `StaleElementReference`           | Un comando de elemento falló porque el elemento referenciado ya no está conectado al DOM.                                                                                      |
| 11         | `ElementoNoVisible`               | No se ha podido completar un comando de elemento porque el elemento no es visible en la página.                                                                                |
| 12         | `InvalidElementState`             | No se pudo completar un comando de elemento porque el elemento está en un estado inválido (por ejemplo, al intentar hacer clic en un elemento desactivado). |
| 13         | `Error desconocido`               | Se ha producido un error desconocido del lado del servidor mientras se procesaba el comando.                                                                                   |
| 15         | `ElementIsNotSelectable`          | Se ha intentado seleccionar un elemento que no puede ser seleccionado.                                                                                                         |
| 17         | `JavaScriptError`                 | Ocurrió un error mientras se ejecutaba el usuario proporcionaba JavaScript.                                                                                                    |
| 19         | `XPathLookupError`                | Se ha producido un error al buscar un elemento por XPath.                                                                                                                      |
| 21         | `Tiempo de espera`                | Una operación no se completó antes de que expirara el tiempo de espera.                                                                                                        |
| 23         | `NoSuchWindow`                    | Una solicitud para cambiar a una ventana diferente no pudo ser satisfecha porque no se pudo encontrar la ventana.                                                              |
| 24         | `Inválida CookieDomain`           | Se hizo un intento ilegal de establecer una cookie bajo un dominio diferente a la página actual.                                                                               |
| 25         | `UnableToSetCookie`               | Una solicitud para establecer el valor de una cookie no pudo ser satisfecha.                                                                                                   |
| 26         | `UnexpectedAlertOpen`             | Se abrió un diálogo modal, bloqueando esta operación                                                                                                                                           |
| 27         | `NoAlertOpenError`                | Se intentó operar en un diálogo modal cuando uno no estaba abierto.                                                                                                            |
| 28         | `ScriptTimeout`                   | Un script no se completó antes de que caducara su tiempo de espera.                                                                                                            |
| 29         | `ElementCoordinates Inválidos`    | Las coordenadas proporcionadas a una operación de interacción no son válidas.                                                                                                  |
| 30         | `IMENotAvailable`                 | IME no estaba disponible.                                                                                                                                                      |
| 31         | `IMEEngineActivationFailed`       | No se pudo iniciar un motor IME.                                                                                                                                               |
| 32         | `Selector Inválido`               | El argumento no era un selector válido (por ejemplo, XPath/CSS).                                                                                            |
| 33         | `Sesión no creada Excepción`      | No se pudo crear una nueva sesión.                                                                                                                                             |
| 34         | `Mover objetivo fuera de límites` | El objetivo proporcionado para una acción de movimiento está fuera de límites.                                                                                                 |

El cliente debe interpretar una respuesta 404 No encontrada del servidor como una respuesta de "comando desconocido". Todas las otras respuestas 4xx y 5xx del servidor que no definen un campo de estado deben interpretarse como respuestas de "Error desconocido".

### Manejo de errores

Hay dos niveles de manejo de errores especificados por el protocolo wire: peticiones inválidas y comandos fallidos.

#### Solicitudes inválidas

Todas las peticiones no válidas deben resultar en que el servidor devuelva una respuesta HTTP 4xx. El Tipo de Contenido de Respuesta debe establecerse en texto/plano y el cuerpo del mensaje debe ser un mensaje de error descriptivo. Las categorías de solicitudes no válidas son las siguientes:

<dl>
<dt><b>Unknown Commands</b></dt>
<dd>If the server receives a command request whose path is not mapped to a resource in the REST service, it should respond with a <code>404 Not Found</code> message.<br>
<br>
</dd>
<dt><b>Unimplemented Commands</b></dt>
<dd>Cada servidor que implementa el protocolo de cable WebDriver debe responder a cada comando definido. Si un comando individual no ha sido implementado en el servidor, el servidor debe responder con un mensaje de error <code>501 no implementado</code>. Tenga en cuenta que este es el único error en la categoría Solicitud inválida que no devuelve un código de estado <code>4xx</code> .<br>
<br>
</dd>
<dt><b>Recurso Variable No encontrado</b></dt>
<dd>Si una petición de ruta mapea un recurso variable, pero ese recurso no existe, entonces el servidor debería responder con un <code>404 no encontrado</code>. Por ejemplo, si el ID <code>my-session</code> no es un ID de sesión válido en el servidor, y se envía un comando a <code>GET /session/my-session HTTP/1.</code>, entonces el servidor debería devolver con elegancia un <code>404</code>.<br>
<br>
</dd>
<dt><b>Invalid Command Method</b></dt>
<dd>Si una petición de ruta mapea un recurso válido, pero ese recurso no responde al método de solicitud, el servidor debe responder con un método <code>405 no permitido</code>. La respuesta debe incluir un encabezado Permitir con una lista de los métodos permitidos para el recurso solicitado.<br>
<br>
</dd>
<dt><b>Faltan parámetros de comando</b></dt>
<dd>Si un comando POST/PUT mapea un recurso que espera un conjunto de parámetros JSON, y el cuerpo de respuesta no incluye uno de esos parámetros, el servidor debe responder con una <code>400 Solicitud Mala</code>. El cuerpo de respuesta debe listar los parámetros faltantes.<br>
<br>
</dd>
</dl>

#### Comandos fallidos

Si una solicitud se mapea a un comando válido y contiene todos los parámetros esperados en el cuerpo de la solicitud, pero falla al ejecutar con éxito, entonces el servidor debe enviar un error de servidor interno 500. Esta respuesta debe tener un Tipo de Contenido de `application/json;charset=UTF-8` y el cuerpo de respuesta debe ser un objeto de respuesta JSON bien formado.

El estado de respuesta debe ser uno de los códigos de estado definidos y el valor de respuesta debe ser otro objeto JSON con información detallada para el comando fallido:

| Clave      | Tipo   | Descripción                                                                                                                                                                                                                                                                   |
| :--------- | :----- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| mensaje    | cadena | Un mensaje descriptivo para el fallo del comando.                                                                                                                                                                                                             |
| pantalla   | cadena | (Opcional) Si está incluido, una captura de pantalla de la página actual como una cadena codificada en base64.                                                                                                                             |
| clase      | cadena | (Opcional) Si se incluye, especifica el nombre de la clase completamente calificada para la excepción que se arrojó cuando el comando falló.                                                                                               |
| stackTrace | matriz | (Opcional) Si se incluye, especifica un array de objetos JSON que describen el stack trace para la excepción que se arrojó cuando el comando falló. El elemento cero de la matriz representa la parte superior de la pila. |

Cada objeto JSON en la matriz stackTrace debe contener las siguientes propiedades:

| **Clave**         | **Type** | **Descripción**                                                                                                                                                                                                                                                                              |
| :---------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| nombre de archivo | cadena   | El nombre del archivo de origen que contiene la línea representada por este fotograma.                                                                                                                                                                                       |
| claseNombre       | cadena   | El nombre de clase completo para la clase activa en este fotograma. Si el nombre de la clase no se puede determinar, o no es aplicable para el idioma en el que está implementado el servidor, entonces esta propiedad debe establecerse en la cadena vacía. |
| métodoNombre      | cadena   | El nombre del método activo en este fotograma, o la cadena vacía si es desconocido/no aplicable.                                                                                                                                                                             |
| número de línea   | número   | El número de línea en el archivo original de origen para el cuadro, o 0 si se desconoce.                                                                                                                                                                                     |

## Mapeo de recursos

Los recursos en el servicio WebDriver REST se asignan a patrones individuales de URL. Cada recurso puede responder a uno o más métodos de petición HTTP. Si un recurso responde a una solicitud GET, entonces también debería responder a peticiones HEAD. Todos los recursos deben responder a peticiones OPTIONS con un campo de cabecera `Permitir`, cuyo valor es una lista de todos los métodos a los que responde el recurso.

Si un recurso es mapeado a una URL que contiene un nombre de segmento de ruta variable, ese segmento de ruta debe ser usado para continuar la petición. Los segmentos de ruta variable se indican en el mapeo de recursos por un prefijo de dos puntos. Por ejemplo, consideremos lo siguiente:

```
/favorito/color/:person
```

Un recurso asignado a esta URL debería analizar el valor del segmento de ruta `:person` para determinar aún más cómo responder a la solicitud. Si este recurso recibió una solicitud para `/favorite/color/Jack`, entonces debería devolver el color favorito de Jack. Del mismo modo, el servidor debería devolver el color favorito de Jill para cualquier solicitud a `/favorite/color/Jill`.

Dos recursos sólo pueden ser mapeados al mismo patrón de URL si uno de esos recursos contiene segmentos de ruta variables, y el otro no. En estos casos, el servidor siempre debe enrutar las peticiones al recurso cuya ruta sea la mejor coincidencia para la petición. Considere las siguientes dos rutas de recursos:

1. `/session/:sessionId/element/active`
2. `/session/:sessionId/element/:id`

Dados estos mapeos, el servidor siempre debe enrutar peticiones cuyo segmento de ruta final está activo en el primer recurso. Todas las demás peticiones deben ser enrutadas en segundo.

## Referencia de comandos

### Resumen del Comando

| **Método HTTP** | **Ruta**                                                                                                                                                                     | **Summary**                                                                                                                                                           |                |                                            |
| :-------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------------------ |
| RECOGER         | [/status](#status)                                                                                                                                                           | Consultar el estado actual del servidor.                                                                                                              |                |                                            |
| POST            | [/session](#session)                                                                                                                                                         | Crear una nueva sesión.                                                                                                                               |                |                                            |
| RECOGER         | [/sessions](#sessions)                                                                                                                                                       | Devuelve una lista de las sesiones activas actualmente.                                                                                               |                |                                            |
| RECOGER         | [/session/:sessionId](#sessionsessionid)                                                                                                                     | Recuperar las capacidades de la sesión especificada.                                                                                                  |                |                                            |
| BORRAR          | [/session/:sessionId](#sessionsessionid)                                                                                                                     | Eliminar la sesión.                                                                                                                                   |                |                                            |
| POST            | [/session/:sessionId/timeouts](#sessionsessionidtimeouts)                                                                                                    | Configurar la cantidad de tiempo que un tipo de operación en particular puede ejecutar antes de que se aborten y un                                                   | Tiempo agotado | se ha devuelto al cliente. |
| POST            | [/session/:sessionId/timeouts/async\_script](#sessionsessionidtimeoutsasync_script)                                                    | Establece el tiempo en milisegundos, que los scripts asíncronos ejecutados por `/session/:sessionId/execute_async` pueden ejecutarse antes de que sean abortados y un | Tiempo agotado | se ha devuelto al cliente. |
| POST            | [/session/:sessionId/timeouts/implicit\_wait](#sessionsessionidtimeoutsimplicit_wait)                                                  | Establecer la cantidad de tiempo que el controlador debe esperar al buscar elementos.                                                                 |                |                                            |
| RECOGER         | [/session/:sessionId/window\_handle](#sessionsessionidwindow_handle)                                                                   | Recuperar el manejador de ventana actual.                                                                                                             |                |                                            |
| RECOGER         | [/session/:sessionId/window\_handles](#sessionsessionidwindow_handles)                                                                 | Recuperar la lista de todos los manejadores de ventanas disponibles para la sesión.                                                                   |                |                                            |
| RECOGER         | [/session/:sessionId/url](#sessionsessionidurl)                                                                                                              | Recuperar la URL de la página actual.                                                                                                                 |                |                                            |
| POST            | [/session/:sessionId/url](#sessionsessionidurl)                                                                                                              | Navega a una nueva URL.                                                                                                                               |                |                                            |
| POST            | [/session/:sessionId/forward](#sessionsessionidforward)                                                                                                      | Navegar hacia adelante en el historial del navegador, si es posible.                                                                                  |                |                                            |
| POST            | [/session/:sessionId/back](#sessionsessionidback)                                                                                                            | Navegar hacia atrás en el historial del navegador, si es posible.                                                                                     |                |                                            |
| POST            | [/session/:sessionId/refresh](#sessionsessionidrefresh)                                                                                                      | Actualizar la página actual.                                                                                                                          |                |                                            |
| POST            | [/session/:sessionId/execute](#sessionsessionidexecute)                                                                                                      | Inyectar un fragmento de JavaScript en la página para su ejecución en el contexto del fotograma seleccionado actualmente.                             |                |                                            |
| POST            | [/session/:sessionId/execute\_async](#sessionsessionidexecute_async)                                                                   | Inyectar un fragmento de JavaScript en la página para su ejecución en el contexto del fotograma seleccionado actualmente.                             |                |                                            |
| RECOGER         | [/session/:sessionId/screenshot](#sessionsessionidscreenshot)                                                                                                | Tomar una captura de pantalla de la página actual.                                                                                                    |                |                                            |
| RECOGER         | [/session/:sessionId/ime/available\_engines](#sessionsessionidimeavailable_engines)                                                    | Listar todos los motores disponibles en la máquina.                                                                                                   |                |                                            |
| RECOGER         | [/session/:sessionId/ime/active\_engine](#sessionsessionidimeactive_engine)                                                            | Obtener el nombre del motor IME activo.                                                                                                               |                |                                            |
| RECOGER         | [/session/:sessionId/ime/activated](#sessionsessionidimeactivated)                                                                                           | Indica si la entrada IME está activa en este momento (no si está disponible.                                                       |                |                                            |
| POST            | [/session/:sessionId/ime/deactivate](#sessionsessionidimedeactivate)                                                                                         | Desactiva el motor IME actualmente activo.                                                                                                            |                |                                            |
| POST            | [/session/:sessionId/ime/activate](#sessionsessionidimeactivate)                                                                                             | Hacer activos un motor que esté disponible (aparece en la lista devuelta por getAvailable Engines).                                |                |                                            |
| POST            | [/session/:sessionId/frame](#sessionsessionidframe)                                                                                                          | Cambia el enfoque a otro fotograma de la página.                                                                                                      |                |                                            |
| POST            | [/session/:sessionId/frame/parent](#sessionsessionidframeparent)                                                                                             | Cambie el enfoque al contexto padre.                                                                                                                  |                |                                            |
| POST            | [/session/:sessionId/window](#sessionsessionidwindow)                                                                                                        | Cambia el enfoque a otra ventana.                                                                                                                     |                |                                            |
| BORRAR          | [/session/:sessionId/window](#sessionsessionidwindow)                                                                                                        | Cerrar la ventana actual.                                                                                                                             |                |                                            |
| POST            | [/session/:sessionId/window/:windowHandle/size](#sessionsessionidwindowwindowhandlesize)                                                     | Cambia el tamaño de la ventana especificada.                                                                                                          |                |                                            |
| RECOGER         | [/session/:sessionId/window/:windowHandle/size](#sessionsessionidwindowwindowhandlesize)                                                     | Obtener el tamaño de la ventana especificada.                                                                                                         |                |                                            |
| POST            | [/session/:sessionId/window/:windowHandle/position](#sessionsessionidwindowwindowhandleposition)                                             | Cambia la posición de la ventana especificada.                                                                                                        |                |                                            |
| RECOGER         | [/session/:sessionId/window/:windowHandle/position](#sessionsessionidwindowwindowhandleposition)                                             | Obtiene la posición de la ventana especificada.                                                                                                       |                |                                            |
| POST            | [/session/:sessionId/window/:windowHandle/maximize](#sessionsessionidwindowwindowhandlemaximize)                                             | Maximice la ventana especificada si no está maximizada.                                                                                               |                |                                            |
| RECOGER         | [/session/:sessionId/cookie](#sessionsessionidcookie)                                                                                                        | Recuperar todas las cookies visibles en la página actual.                                                                                             |                |                                            |
| POST            | [/session/:sessionId/cookie](#sessionsessionidcookie)                                                                                                        | Establecer una cookie.                                                                                                                                |                |                                            |
| BORRAR          | [/session/:sessionId/cookie](#sessionsessionidcookie)                                                                                                        | Borrar todas las cookies visibles en la página actual.                                                                                                |                |                                            |
| BORRAR          | [/session/:sessionId/cookie/:name](#sessionsessionidcookiename)                                                                              | Elimina la cookie con el nombre dado.                                                                                                                 |                |                                            |
| RECOGER         | [/session/:sessionId/source](#sessionsessionidsource)                                                                                                        | Obtener la fuente de la página actual.                                                                                                                |                |                                            |
| RECOGER         | [/session/:sessionId/title](#sessionsessionidtitle)                                                                                                          | Obtener el título de la página actual.                                                                                                                |                |                                            |
| POST            | [/session/:sessionId/element](#sessionsessionidelement)                                                                                                      | Buscar un elemento en la página, comenzando por la raíz del documento.                                                                                |                |                                            |
| POST            | [/session/:sessionId/elements](#sessionsessionidelements)                                                                                                    | Buscar múltiples elementos en la página, comenzando desde la raíz del documento.                                                                      |                |                                            |
| POST            | [/session/:sessionId/element/activo](#sessionsessionidelementactive)                                                                                         | Obtener el elemento en la página que actualmente se ha centrado.                                                                                      |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id](#sessionsessionidelementid)                                                                                | Describa el elemento identificado.                                                                                                                    |                |                                            |
| POST            | [/session/:sessionId/element/:id/element](#sessionsessionidelementidelement)                                                                 | Buscar un elemento en la página, comenzando por el elemento identificado.                                                                             |                |                                            |
| POST            | [/session/:sessionId/element/:id/elements](#sessionsessionidelementidelements)                                                               | Buscar múltiples elementos en la página, comenzando por el elemento identificado.                                                                     |                |                                            |
| POST            | [/session/:sessionId/element/:id/click](#sessionsessionidelementidclick)                                                                     | Haga clic en un elemento.                                                                                                                             |                |                                            |
| POST            | [/session/:sessionId/element/:id/submit](#sessionsessionidelementidsubmit)                                                                   | Enviar un elemento `FORM`.                                                                                                                            |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/text](#sessionsessionidelementidtext)                                                                       | Devuelve el texto visible para el elemento.                                                                                                           |                |                                            |
| POST            | [/session/:sessionId/element/:id/valor](#sessionsessionidelementidvalue)                                                                     | Enviar una secuencia de trazos clave a un elemento.                                                                                                   |                |                                            |
| POST            | [/session/:sessionId/keys](#sessionsessionidkeys)                                                                                                            | Envía una secuencia de teclas al elemento activo.                                                                                                     |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/name](#sessionsessionidelementidname)                                                                       | Consulta para el nombre de la etiqueta de un elemento.                                                                                                |                |                                            |
| POST            | [/session/:sessionId/element/:id/clear](#sessionsessionidelementidclear)                                                                     | Elimina el valor de un elemento `TEXTAREA` o `text INPUT`.                                                                                            |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/seleccionado](#sessionsessionidelementidselected)                                                           | Determina si un elemento `OPTION`, o un elemento `INPUT` de tipo `checkbox` o `radiobutton` está seleccionado actualmente.                            |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/enabled](#sessionsessionidelementidenabled)                                                                 | Determinar si un elemento está habilitado actualmente.                                                                                                |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/attribute/:name](#sessionsessionidelementidattribute/:name)                                 | Obtener el valor del atributo de un elemento.                                                                                                         |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/equals/:other](#sessionsessionidelementidequals/:other)                                     | Evalúa si dos IDs de elementos se refieren al mismo elemento DOM.                                                                                     |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/displayed](#sessionsessionidelementiddisplayed)                                                             | Determinar si un elemento se muestra actualmente.                                                                                                     |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/location](#sessionsessionidelementidlocation)                                                               | Determinar la ubicación de un elemento en la página.                                                                                                  |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/location\_in\_view](#sessionsessionidelementidlocation_in_view) | Determina la ubicación de un elemento en la pantalla una vez que haya sido desplazado a la vista.                                                     |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/size](#sessionsessionidelementidsize)                                                                       | Determina el tamaño de un elemento en píxeles.                                                                                                        |                |                                            |
| RECOGER         | [/session/:sessionId/element/:id/css/:propertyName](#sessionsessionidelementidcss/:propertyName)                             | Consulta el valor de la propiedad CSS computada de un elemento.                                                                                       |                |                                            |
| RECOGER         | [/session/:sessionId/orientation](#sessionsessionidorientation)                                                                                              | Obtener la orientación actual del navegador.                                                                                                          |                |                                            |
| POST            | [/session/:sessionId/orientation](#sessionsessionidorientation)                                                                                              | Establecer la orientación del navegador.                                                                                                              |                |                                            |
| RECOGER         | [/session/:sessionId/alert\_text](#sessionsessionidalert_text)                                                                         | Obtiene el texto del cuadro de diálogo `alert()` de JavaScript mostrado actualmente, `confirm()` o `prompt()`.                                        |                |                                            |
| POST            | [/session/:sessionId/alert\_text](#sessionsessionidalert_text)                                                                         | Envía pulsaciones de teclado a un diálogo JavaScript `prompt()`.                                                                                      |                |                                            |
| POST            | [/session/:sessionId/accept\_alert](#sessionsessionidaccept_alert)                                                                     | Acepta el diálogo de alerta que se muestra actualmente.                                                                                               |                |                                            |
| POST            | [/session/:sessionId/dismiss\_alert](#sessionsessioniddismiss_alert)                                                                   | Descarta el diálogo de alerta que se muestra actualmente.                                                                                             |                |                                            |
| POST            | [/session/:sessionId/moveto](#sessionsessionidmoveto)                                                                                                        | Mueva el ratón por un desplazamiento del elemento especificado.                                                                                       |                |                                            |
| POST            | [/session/:sessionId/click](#sessionsessionidclick)                                                                                                          | Haga clic en cualquier botón del ratón (en las coordenadas definidas por el último comando de movet).                              |                |                                            |
| POST            | [/session/:sessionId/buttondown](#sessionsessionidbuttondown)                                                                                                | Haga clic y mantenga pulsado el botón izquierdo del ratón (en las coordenadas fijadas por el último comando de move).              |                |                                            |
| POST            | [/session/:sessionId/buttonup](#sessionsessionidbuttonup)                                                                                                    | Libera el botón del ratón previamente presionado (donde el ratón está actualmente).                                                |                |                                            |
| POST            | [/session/:sessionId/doubleclick](#sessionsessioniddoubleclick)                                                                                              | Haga doble clic en las coordenadas actuales del ratón (definidas por moveto).                                                      |                |                                            |
| POST            | [/session/:sessionId/touch/click](#sessionsessionidtouchclick)                                                                                               | Toque un solo en el dispositivo habilitado.                                                                                                           |                |                                            |
| POST            | [/session/:sessionId/touch/down](#sessionsessionidtouchdown)                                                                                                 | Dedo abajo en la pantalla.                                                                                                                            |                |                                            |
| POST            | [/session/:sessionId/touch/up](#sessionsessionidtouchup)                                                                                                     | Deduzca en la pantalla.                                                                                                                               |                |                                            |
| POST            | [sesión/:sessionId/toque/move](#sessionsessionidtouchmove)                                                                                                   | Mover el dedo en la pantalla.                                                                                                                         |                |                                            |
| POST            | [session/:sessionId/touch/scroll](#sessionsessionidtouchscroll)                                                                                              | Desplácese en la pantalla táctil utilizando eventos de movimiento basados en dedos.                                                                   |                |                                            |
| POST            | [session/:sessionId/touch/scroll](#sessionsessionidtouchscroll)                                                                                              | Desplácese en la pantalla táctil utilizando eventos de movimiento basados en dedos.                                                                   |                |                                            |
| POST            | [session/:sessionId/touch/doubleclick](#sessionsessionidtouchdoubleclick)                                                                                    | Doble toque en la pantalla táctil usando eventos de movimiento de dedos.                                                                              |                |                                            |
| POST            | [session/:sessionId/touch/longclick](#sessionsessionidtouchlongclick)                                                                                        | Pulsación larga en la pantalla táctil usando eventos de movimiento de dedos.                                                                          |                |                                            |
| POST            | [session/:sessionId/touch/flick](#sessionsessionidtouchflick)                                                                                                | Desliza en la pantalla táctil usando eventos de movimiento de dedos.                                                                                  |                |                                            |
| POST            | [session/:sessionId/touch/flick](#sessionsessionidtouchflick)                                                                                                | Desliza en la pantalla táctil usando eventos de movimiento de dedos.                                                                                  |                |                                            |
| RECOGER         | [/session/:sessionId/location](#sessionsessionidlocation)                                                                                                    | Obtener la geolocalización actual.                                                                                                                    |                |                                            |
| POST            | [/session/:sessionId/location](#sessionsessionidlocation)                                                                                                    | Establecer la geolocalización actual.                                                                                                                 |                |                                            |
| RECOGER         | [/session/:sessionId/local\_storage](#sessionsessionidlocal_storage)                                                                   | Obtener todas las claves del almacenamiento.                                                                                                          |                |                                            |
| POST            | [/session/:sessionId/local\_storage](#sessionsessionidlocal_storage)                                                                   | Establece el elemento de almacenamiento para la clave dada.                                                                                           |                |                                            |
| BORRAR          | [/session/:sessionId/local\_storage](#sessionsessionidlocal_storage)                                                                   | Limpiar el almacenamiento.                                                                                                                            |                |                                            |
| RECOGER         | [/session/:sessionId/local\_storage/key/:key](#sessionsessionidlocal_storagekeykey)                                    | Obtener el elemento de almacenamiento para la clave dada.                                                                                             |                |                                            |
| BORRAR          | [/session/:sessionId/local\_storage/key/:key](#sessionsessionidlocal_storagekeykey)                                    | Elimina el elemento de almacenamiento de la clave dada.                                                                                               |                |                                            |
| RECOGER         | [/session/:sessionId/local\_storage/size](#sessionsessionidlocal_storagesize)                                                          | Obtener el número de elementos en el almacenamiento.                                                                                                  |                |                                            |
| RECOGER         | [/session/:sessionId/session\_storage](#sessionsessionidsession_storage)                                                               | Obtener todas las claves del almacenamiento.                                                                                                          |                |                                            |
| POST            | [/session/:sessionId/session\_storage](#sessionsessionidsession_storage)                                                               | Establece el elemento de almacenamiento para la clave dada.                                                                                           |                |                                            |
| BORRAR          | [/session/:sessionId/session\_storage](#sessionsessionidsession_storage)                                                               | Limpiar el almacenamiento.                                                                                                                            |                |                                            |
| RECOGER         | [/session/:sessionId/session\_storage/key/:key](#sessionsessionidsession_storagekeykey)                                | Obtener el elemento de almacenamiento para la clave dada.                                                                                             |                |                                            |
| BORRAR          | [/session/:sessionId/session\_storage/key/:key](#sessionsessionidsession_storagekeykey)                                | Elimina el elemento de almacenamiento de la clave dada.                                                                                               |                |                                            |
| RECOGER         | [/session/:sessionId/session\_storage/size](#sessionsessionidsession_storagesize)                                                      | Obtener el número de elementos en el almacenamiento.                                                                                                  |                |                                            |
| POST            | [/session/:sessionId/log](#sessionsessionidlog)                                                                                                              | Obtener el registro para un tipo de registro determinado.                                                                                             |                |                                            |
| RECOGER         | [/session/:sessionId/log/types](#sessionsessionidlogtypes)                                                                                                   | Obtener tipos de registro disponibles.                                                                                                                |                |                                            |
| RECOGER         | [/session/:sessionId/application\_cache/status](#sessionsessionidapplication_cachestatus)                                              | Obtener el estado de la caché de aplicaciones html5.                                                                                                  |                |                                            |

### Detalle del comando

#### /estado

<dl>
<dd>
<h4>GET /estado</h4>
</dd>
<dd>
<dl>
<dd>
Consultar el estado actual del servidor.  El servidor debe responder con una respuesta general "HTTP 200 OK" si está vivo y acepta comandos. El cuerpo de respuesta debe ser un objeto JSON que describa el estado del servidor. Todas las implementaciones del servidor deben devolver dos objetos básicos que describen la plataforma actual del servidor y cuando el servidor fue construido. Todos los campos son opcionales; si se omite, el cliente debe asumir que el valor es uknown. Además, las implementaciones del servidor pueden incluir campos adicionales no listados aquí.<br>
<br>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Tipo</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> construir      </td><td> objeto      </td><td>                    </td></tr>
<tr><td> build.version </td><td> cadena      </td><td> Una etiqueta genérica de liberación (es decir, "2.0rc3") </td></tr>
<tr><td> crear.revisión </td><td> cadena      </td><td> La revisión del cliente de control de código fuente local desde el cual se construyó el servidor </td></tr>
<tr><td> construir.hora </td><td> cadena      </td><td> Una marca de tiempo desde cuando se construyó el servidor. </td></tr>
<tr><td> os         </td><td> objeto      </td><td>                    </td></tr>
<tr><td> os.arch    </td><td> cadena      </td><td> La arquitectura actual del sistema. </td></tr>
<tr><td> os.name    </td><td> cadena      </td><td> El nombre del sistema operativo que el servidor está ejecutando actualmente: "windows", "linux", etc. </td></tr>
<tr><td> os.version </td><td> cadena      </td><td> La versión del sistema operativo. </td></tr></tbody></table>

</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{object}</code> Un objeto que describe el estado general del servidor.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /sesión

<dl>
<dd>
<h4>POST /session</h4>
</dd>
<dd>
<dl>
<dd>
Crear una nueva sesión. El servidor debería intentar crear una sesión que coincida más estrechamente con las capacidades deseadas y requeridas. Las capacidades requeridas tienen mayor prioridad que las capacidades deseadas y deben establecerse para que la sesión sea creada.</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>deseadas capacidades</code> - <code>{object}</code> Un objeto que describe las capacidades deseadas <a href='#Desired_Capabilities.md'>de la sesión</a>.</dd>
<dd><code>requerimientos</code> - <code>{object}</code> Un objeto que describe las capacidades requeridas <a href='#Desired_Capabilities.md'>de la sesión</a> (Opcional).</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{object}</code> Un objeto que describe las capacidades <a href='#Actual_Capabilities.md'>de la sesión</a>.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>SessionNotCreatedException</code> - Si no se pudo establecer una capacidad requerida.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /sesiones

<dl>
<dd>
<h4>GET /sessions</h4>
</dd>
<dd>
<dl>
<dd>
Devuelve una lista de las sesiones activas actualmente. Cada sesión se devolverá como una lista de objetos JSON con las siguientes claves:<br>
<br>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Tipo</b> </th><th><b>Descripción</b></th></tr></thead><tbody>
<tr><td> id         </td><td> cadena      </td><td> La sesión ID. </td></tr>
<tr><td> capacidades </td><td> objeto      </td><td> Un objeto que describe las capacidades <a href='#Actual_Capabilities.md'>de la sesión</a>. </td></tr></tbody></table>

</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;Object&gt;}</code> Una lista de las sesiones activas.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId

<dl>
<dd>
<h4>GET /session/:sessionId</h4>
</dd>
<dd>
<dl>
<dd>Recuperar las capacidades de la sesión especificada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{object}</code> Un objeto que describe las capacidades <a href='#Actual_Capabilities.md'>de la sesión</a>.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId</h4>
</dd>
<dd>
<dl>
<dd>Eliminar la sesión.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/timeouts

<dl>
<dd>
<h4>POST /session/:sessionId/timeouts</h4>
</dd>
<dd>
<dl>
<dd>
Configure the amount of time that a particular type of operation can execute for before they are aborted and a |Timeout| error is returned to the client.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>tipo</code> - <code>{string}</code> El tipo de operación para establecer el tiempo de espera. Los valores válidos son: "script" para los tiempos de espera del script, "implicit" para modificar el tiempo de espera implícito y "carga de página" para establecer un tiempo de espera de la página de espera.</dd>
<dd><code>ms</code> - <code>{number}</code> La cantidad de tiempo, en milisegundos, que los comandos por tiempo limitado pueden ejecutar.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/timeouts/async\_script

<dl>
<dd>
<h4>POST /session/:sessionId/timeouts/async_script</h4>
</dd>
<dd>
<dl>
<dd>Ajusta la cantidad de tiempo, en milisegundos, que se permita ejecutar scripts asíncronos ejecutados por <code>/session/:sessionId/execute_async</code> antes de que sean abortados y se devuelva un error |Timeout| al cliente.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>ms</code> - <code>{number}</code> La cantidad de tiempo, en milisegundos, que los comandos por tiempo limitado pueden ejecutar.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/timeouts/implicit\_wait

<dl>
<dd>
<h4>POST /session/:sessionId/timeouts/implicit_wait</h4>
</dd>
<dd>
<dl>
<dd>Establecer la cantidad de tiempo que el controlador debe esperar al buscar elementos. Cuando<br>
busca un solo elemento, el controlador debe sondear la página hasta que se encuentre un elemento o<br>
el tiempo de espera expire, lo que ocurra primero. Al buscar múltiples elementos, el controlador<br>
debería sondear la página hasta que al menos se encuentre un elemento o el tiempo de espera caduque, en cuyo punto<br>
debería devolver una lista vacía.<br>
<br>
If this command is never sent, the driver should default to an implicit wait of 0ms.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>ms</code> - <code>{number}</code> La cantidad de tiempo para esperar, en milisegundos. Este valor tiene un límite inferior a 0.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/window\_handle

<dl>
<dd>
<h4>GET /session/:sessionId/window_handle</h4>
</dd>
<dd>
<dl>
<dd>Recuperar el manejador de ventana actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> El manejador de ventana actual.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/window\_handles

<dl>
<dd>
<h4>GET /session/:sessionId/window_handles</h4>
</dd>
<dd>
<dl>
<dd>Recuperar la lista de todos los manejadores de ventanas disponibles para la sesión.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;string&gt;}</code> Una lista de manejadores de ventanas.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/url

<dl>
<dd>
<h4>GET /session/:sessionId/url</h4>
</dd>
<dd>
<dl>
<dd>Recuperar la URL de la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> La URL actual.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/url</h4>
</dd>
<dd>
<dl>
<dd>Navega a una nueva URL.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>url</code> - <code>{string}</code> La URL a la que navegar.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/forward

<dl>
<dd>
<h4>POST /session/:sessionId/forward</h4>
</dd>
<dd>
<dl>
<dd>Navegar hacia adelante en el historial del navegador, si es posible.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/back

<dl>
<dd>
<h4>POST /session/:sessionId/back</h4>
</dd>
<dd>
<dl>
<dd>Navegar hacia atrás en el historial del navegador, si es posible.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/refresh

<dl>
<dd>
<h4>POST /session/:sessionId/refrescar</h4>
</dd>
<dd>
<dl>
<dd>Actualizar la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/execute

<dl>
<dd>
<h4>POST /session/:sessionId/execute</h4>
</dd>
<dd>
<dl>
<dd>
Inyectar un fragmento de JavaScript en la página para su ejecución en el contexto del fotograma seleccionado actualmente. Se asume que el script ejecutado es sincrónico y que el resultado de la evaluación del script es devuelto al cliente.<br>
<br>
El argumento <code>script</code> define el script a ejecutar en forma de un cuerpo de función.  El valor devuelto por esa función será devuelto al cliente.  The function will be invoked with the provided <code>args</code> array and the values may be accessed via the <code>arguments</code> object in the order specified.<br>
<br>
Los argumentos pueden ser cualquier objeto JSON-primitivo, array o JSON.  Los objetos JSON que definen una referencia <a href='#WebElement_JSON_Object.md'>WebElement</a> se convertirán al elemento DOM correspondiente. Del mismo modo, cualquier WebElements en el resultado del script será devuelto al cliente como objetos <a href='#WebElement_JSON_Object.md'>WebElement JSON</a>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>script</code> - <code>{string}</code> El script a ejecutar.</dd>
<dd><code>args</code> - <code>{Array.&lt;*&gt;}</code> Los argumentos del script.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{*}</code> The script result.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si uno de los argumentos del script es un WebElement que no está conectado al DOM de la página.</dd>
<dd><code>JavaScriptError</code> - If the script throws an Error.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/execute\_async

<dl>
<dd>
<h4>POST /session/:sessionId/execute_async</h4>
</dd>
<dd>
<dl>
<dd>
Inyectar un fragmento de JavaScript en la página para su ejecución en el contexto del fotograma seleccionado actualmente. Se asume que el script ejecutado es asíncrono y debe indicar que se hace invocando el callback proporcionado, que siempre se proporciona como argumento final a la función.  El valor de este callback será devuelto al cliente.<br>
<br>
Los comandos de script asincrónicos no pueden expandir la carga de página.  Si se dispara un evento <code>descargando</code> mientras se espera un resultado del script, se debe devolver un error al cliente.<br>
<br>
El argumento <code>script</code> define el script a ejecutar en forma teh del cuerpo de una función.  The function will be invoked with the provided <code>args</code> array and the values may be accessed via the <code>arguments</code> object in the order specified. El argumento final siempre será una función de devolución de llamada que debe ser invocada para indicar que el script ha terminado.<br>
<br>
Los argumentos pueden ser cualquier objeto JSON-primitivo, array o JSON.  Los objetos JSON que definen una referencia <a href='#WebElement_JSON_Object.md'>WebElement</a> se convertirán al elemento DOM correspondiente. Del mismo modo, cualquier WebElements en el resultado del script será devuelto al cliente como objetos <a href='#WebElement_JSON_Object.md'>WebElement JSON</a>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>script</code> - <code>{string}</code> El script a ejecutar.</dd>
<dd><code>args</code> - <code>{Array.&lt;*&gt;}</code> Los argumentos del script.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{*}</code> The script result.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si uno de los argumentos del script es un WebElement que no está conectado al DOM de la página.</dd>
<dd><code>Tiempo de espera</code> - Si el callback del script no es invocado antes de que el tiempo de espera caduque. Los tiempos de espera son controlados por el comando <code>/session/:sessionId/timeout/async_script</code>.</dd>
<dd><code>JavaScriptError</code> - Si el script arroja un Error o si un evento <code>de descarga</code> es disparado mientras espera que el script termine.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/screenshot

<dl>
<dd>
<h4>GET /session/:sessionId/screenshot</h4>
</dd>
<dd>
<dl>
<dd>Tomar una captura de pantalla de la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> La captura de pantalla como PNG codificado en base64.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/ime/available\_engines

<dl>
<dd>
<h4>GET /session/:sessionId/ime/available_engines</h4>
</dd>
<dd>
<dl>
<dd>Listar todos los motores disponibles en la máquina. Para utilizar un motor, tiene que estar presente en esta lista.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;string&gt;}</code> Una lista de motores disponibles</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>ImeNotavailableException</code> - Si el host no soporta IME</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/ime/active\_engine

<dl>
<dd>
<h4>GET /session/:sessionId/ime/active_engine</h4>
</dd>
<dd>
<dl>
<dd>Obtener el nombre del motor IME activo. El nombre de cadena es específico de la plataforma.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> El nombre del motor IME activo.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>ImeNotavailableException</code> - Si el host no soporta IME</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/ime/activado

<dl>
<dd>
<h4>GET /session/:sessionId/ime/activado</h4>
</dd>
<dd>
<dl>
<dd>Indica si la entrada IME está activa en este momento (no si está disponible.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{boolean}</code> verdadero si la entrada IME está disponible y actualmente está activa, de lo contrario es falso</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>ImeNotavailableException</code> - Si el host no soporta IME</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/ime/deactivar

<dl>
<dd>
<h4>POST /session/:sessionId/ime/deactivar</h4>
</dd>
<dd>
<dl>
<dd>Desactiva el motor IME actualmente activo.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>ImeNotavailableException</code> - Si el host no soporta IME</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/ime/activate

<dl>
<dd>
<h4>POST /session/:sessionId/ime/activate</h4>
</dd>
<dd>
<dl>
<dd>Hacer activo un motor disponible (aparece en la lista<br>
devuelto por getResourableEngines). Después de esta llamada, el motor<br>
será añadido a la lista de motores cargados en el daemon IME y la entrada enviada<br>
usando sendKeys será convertida por el motor activo.<br>
Tenga en cuenta que este es un método independiente de la plataforma para activar IME<br>
(la forma específica de la plataforma usando atajos de teclado</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>engine</code> - <code>{string}</code> Nombre del motor a activar.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>ImeActivationFailedException</code> - Si el motor no está disponible o si la activación falla por otras razones.</dd>
<dd><code>ImeNotavailableException</code> - Si el host no soporta IME</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /sesión/:sessionId/frame

<dl>
<dd>
<h4>POST /session/:sessionId/frame</h4>
</dd>
<dd>
<dl>
<dd>Cambia el enfoque a otro fotograma de la página. Si el frame <code>id</code> es <code>nulo</code>, el servidor<br>
debería cambiar al contenido predeterminado de la página.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>id</code> - <code>{string|number|null|WebElement JSON Object}</code> Identificador para que el fotograma cambie de enfoque.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>NochFrame</code> - Si el fotograma especificado por <code>id</code> no se puede encontrar.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/frame/parent

<dl>
<dd>
<h4>POST /session/:sessionId/frame/parent</h4>
</dd>
<dd>
<dl>
<dd>Cambie el enfoque al contexto padre. Si el contexto actual es el contexto de navegación de más alto nivel, el contexto permanece sin cambios.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/window

<dl>
<dd>
<h4>POST /session/:sessionId/window</h4>
</dd>
<dd>
<dl>
<dd>Cambia el enfoque a otra ventana. La ventana a la que cambiar de enfoque puede ser especificada por su manejador de ventanas asignado<br>
del servidor, o por el valor de su atributo <code>nombre</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>nombre</code> - <code>{string}</code> La ventana a la que cambiar de enfoque.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana especificada por <code>name</code> no se puede encontrar.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId/window</h4>
</dd>
<dd>
<dl>
<dd>Cerrar la ventana actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ya está cerrada</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/window/:windowHandle/size

<dl>
<dd>
<h4>POST /session/:sessionId/window/:windowHandle/size</h4>
</dd>
<dd>
<dl>
<dd>Cambia el tamaño de la ventana especificada. Si el parámetro URL de :windowHandle es "actual", la ventana activa será redimensionada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>ancho</code> - <code>{number}</code> El ancho de la nueva ventana.</dd>
<dd><code>altura</code> - <code>{number}</code> La nueva altura de la ventana.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>GET /session/:sessionId/window/:windowHandle/size</h4>
</dd>
<dd>
<dl>
<dd>Obtener el tamaño de la ventana especificada. Si el parámetro URL :windowHandle es "actual", se devolverá el tamaño de la ventana activa.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{width: number, height: number}</code> El tamaño de la ventana.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si no se encuentra la ventana especificada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/window/:windowHandle/position

<dl>
<dd>
<h4>POST /session/:sessionId/window/:windowHandle/position</h4>
</dd>
<dd>
<dl>
<dd>Cambia la posición de la ventana especificada. Si el parámetro URL de :windowHandle es "actual", la ventana activa se moverá.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>x</code> - <code>{number}</code> La coordenada X para colocar la ventana, relativa a la esquina superior izquierda de la pantalla.</dd>
<dd><code>y</code> - <code>{number}</code> La coordenada Y para colocar la ventana, relativa a la esquina superior izquierda de la pantalla.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si no se encuentra la ventana especificada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>GET /session/:sessionId/window/:windowHandle/position</h4>
</dd>
<dd>
<dl>
<dd>Obtiene la posición de la ventana especificada. Si el parámetro URL de :windowHandle es "actual", la posición de la ventana actual será retornada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{x: number, y: number}</code> The X and Y coordinates for the window, relative to the upper left corner of the screen.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si no se encuentra la ventana especificada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/window/:windowHandle/maximize

<dl>
<dd>
<h4>POST /session/:sessionId/window/:windowHandle/maximize</h4>
</dd>
<dd>
<dl>
<dd>Maximice la ventana especificada si no está maximizada. Si el parámetro :windowHandle URL es "actual", la ventana activa se maximizará.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si no se encuentra la ventana especificada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/cookie

<dl>
<dd>
<h4>GET /session/:sessionId/cookie</h4>
</dd>
<dd>
<dl>
<dd>Recuperar todas las cookies visibles en la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;object&gt;}</code> Una lista de <a href='#Cookie_JSON_Object.md'>galletas</a>.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/cookie</h4>
</dd>
<dd>
<dl>
<dd>Establecer una cookie. Si la ruta <a href='#Cookie_JSON_Object.md'>de la cookie</a> no se especifica, debería establecerse en <code>"/"</code>. De la misma manera, si el dominio es omitido, debe ser por defecto en el dominio de la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>cookie</code> - <code>{object}</code> Un objeto <a href='#Cookie_JSON_Object.md'>JSON</a> que define la cookie a añadir.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId/cookie</h4>
</dd>
<dd>
<dl>
<dd>Borrar todas las cookies visibles en la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>InvalidCookieDomain</code> - Si el dominio <code></code> de la cookie no es visible desde la página actual.</dd>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>UnableToSetCookie</code> - Si intenta configurar una cookie en una página que no soporta cookies (e. . páginas con tipo mime <code>text/plain</code>).</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/cookie/:name

<dl>
<dd>
<h4>DELETE /session/:sessionId/cookie/:name</h4>
</dd>
<dd>
<dl>
<dd>Elimina la cookie con el nombre dado. Este comando debería ser un no-op si no hay<br>
tal cookie visible para la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:name</code> - El nombre de la cookie a eliminar.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/source

<dl>
<dd>
<h4>GET /session/:sessionId/source</h4>
</dd>
<dd>
<dl>
<dd>Obtener la fuente de la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> La fuente actual de la página.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/título

<dl>
<dd>
<h4>GET /session/:sessionId/title</h4>
</dd>
<dd>
<dl>
<dd>Obtener el título de la página actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> El título de la página actual.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/elemento

<dl>
<dd>
<h4>POST /session/:sessionId/element</h4>
</dd>
<dd>
<dl>
<dd>Buscar un elemento en la página, comenzando por la raíz del documento. El elemento localizado será devuelto como un objeto WebElement JSON. La siguiente tabla muestra las estrategias de localización que cada servidor debería soportar. Cada locador debe retornar el primer elemento que coincida ubicado en el DOM.<br>
<br>
<table><thead><tr><th><b>Estrategia</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> nombre de clase      </td><td> Devuelve un elemento cuyo nombre de clase contiene el valor de búsqueda; no se permiten nombres compuestos de clases. </td></tr>
<tr><td> selector de censos    </td><td> Devuelve un elemento que coincide con un selector CSS. </td></tr>
<tr><td> id              </td><td> Devuelve un elemento cuyo atributo ID coincide con el valor de búsqueda. </td></tr>
<tr><td> nombre            </td><td> Devuelve un elemento cuyo atributo NOMBRE coincide con el valor de búsqueda. </td></tr>
<tr><td> texto del enlace       </td><td> Devuelve un elemento de ancla cuyo texto visible coincide con el valor de búsqueda. </td></tr>
<tr><td> texto de enlace parcial </td><td> Devuelve un elemento de ancla cuyo texto visible coincide parcialmente con el valor de búsqueda. </td></tr>
<tr><td> nombre de etiqueta        </td><td> Devuelve un elemento cuyo nombre de etiqueta coincide con el valor de búsqueda. </td></tr>
<tr><td> xpath           </td><td> Devuelve un elemento que coincide con una expresión XPath. </td></tr></tbody></table>

</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>usando</code> - <code>{string}</code> La estrategia de localización a utilizar.</dd>
<dd><code>valor</code> - <code>{string}</code> El objetivo de búsqueda.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{ELEMENT:string}</code> Un objeto WebElement JSON para el elemento ubicado.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>NochElement</code> - Si el elemento no puede ser encontrado.</dd>
<dd><code>XPathLookupError</code> - Si usar XPath y la expresión de entrada no es válida.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/elements

<dl>
<dd>
<h4>POST /session/:sessionId/elements</h4>
</dd>
<dd>
<dl>
<dd>Buscar múltiples elementos en la página, comenzando desde la raíz del documento. Los elementos ubicados serán devueltos como un objeto WebElement JSON. La siguiente tabla muestra las estrategias de localización que cada servidor debería soportar. Los elementos deben ser devueltos en el pedido ubicado en el DOM.<br>
<br>
<table><thead><tr><th><b>Estrategia</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> nombre de clase      </td><td> Devuelve todos los elementos cuyo nombre de clase contiene el valor de búsqueda; no se permiten nombres compuestos de clases. </td></tr>
<tr><td> selector de censos    </td><td> Devuelve todos los elementos que coinciden con un selector CSS. </td></tr>
<tr><td> id              </td><td> Devuelve todos los elementos cuyo atributo ID coincide con el valor de búsqueda. </td></tr>
<tr><td> nombre            </td><td> Devuelve todos los elementos cuyo atributo NOMBRE coincide con el valor de búsqueda. </td></tr>
<tr><td> texto del enlace       </td><td> Devuelve todos los elementos de ancla cuyo texto visible coincide con el valor de búsqueda. </td></tr>
<tr><td> texto de enlace parcial </td><td> Devuelve todos los elementos de ancla cuyo texto visible coincide parcialmente con el valor de búsqueda. </td></tr>
<tr><td> nombre de etiqueta        </td><td> Devuelve todos los elementos cuyo nombre de etiqueta coincide con el valor de búsqueda. </td></tr>
<tr><td> xpath           </td><td> Devuelve todos los elementos que coinciden con una expresión XPath. </td></tr></tbody></table>

</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>usando</code> - <code>{string}</code> La estrategia de localización a utilizar.</dd>
<dd><code>valor</code> - <code>{string}</code> El objetivo de búsqueda.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;{ELEMENT:string}&gt;}</code> A list of WebElement JSON objects for the located elements.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>XPathLookupError</code> - Si usar XPath y la expresión de entrada no es válida.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/activo

<dl>
<dd>
<h4>POST /session/:sessionId/element/active</h4>
</dd>
<dd>
<dl>
<dd>Obtener el elemento en la página que actualmente se ha centrado. El elemento será devuelto como un objeto WebElement JSON.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{ELEMENT:string}</code> Un objeto WebElement JSON para el elemento activo.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id</h4>
</dd>
<dd>
<dl>
<dd>Describa el elemento identificado.<br>
<br>
<b>Nota:</b> Este comando está reservado para uso futuro; su tipo de retorno no está definido actualmente.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/element

<dl>
<dd>
<h4>POST /session/:sessionId/element/:id/element</h4>
</dd>
<dd>
<dl>
<dd>Buscar un elemento en la página, comenzando por el elemento identificado. El elemento localizado será devuelto como un objeto WebElement JSON. La siguiente tabla muestra las estrategias de localización que cada servidor debería soportar. Cada locador debe retornar el primer elemento que coincida ubicado en el DOM.<br>
<br>
<table><thead><tr><th><b>Estrategia</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> nombre de clase      </td><td> Devuelve un elemento cuyo nombre de clase contiene el valor de búsqueda; no se permiten nombres compuestos de clases. </td></tr>
<tr><td> selector de censos    </td><td> Devuelve un elemento que coincide con un selector CSS. </td></tr>
<tr><td> id              </td><td> Devuelve un elemento cuyo atributo ID coincide con el valor de búsqueda. </td></tr>
<tr><td> nombre            </td><td> Devuelve un elemento cuyo atributo NOMBRE coincide con el valor de búsqueda. </td></tr>
<tr><td> texto del enlace       </td><td> Devuelve un elemento de ancla cuyo texto visible coincide con el valor de búsqueda. </td></tr>
<tr><td> texto de enlace parcial </td><td> Devuelve un elemento de ancla cuyo texto visible coincide parcialmente con el valor de búsqueda. </td></tr>
<tr><td> nombre de etiqueta        </td><td> Devuelve un elemento cuyo nombre de etiqueta coincide con el valor de búsqueda. </td></tr>
<tr><td> xpath           </td><td> Devuelve un elemento que coincide con una expresión XPath. La expresión XPath proporcionada debe aplicarse al servidor "tal cual"; si la expresión no es relativa a la raíz del elemento, el servidor no debería modificarla. En consecuencia, una consulta XPath puede devolver elementos no contenidos en el subárbol del elemento raíz. </td></tr></tbody></table>

</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>usando</code> - <code>{string}</code> La estrategia de localización a utilizar.</dd>
<dd><code>valor</code> - <code>{string}</code> El objetivo de búsqueda.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{ELEMENT:string}</code> Un objeto WebElement JSON para el elemento ubicado.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
<dd><code>NochElement</code> - Si el elemento no puede ser encontrado.</dd>
<dd><code>XPathLookupError</code> - Si usar XPath y la expresión de entrada no es válida.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/elements

<dl>
<dd>
<h4>POST /session/:sessionId/element/:id/elements</h4>
</dd>
<dd>
<dl>
<dd>Buscar múltiples elementos en la página, comenzando por el elemento identificado. Los elementos ubicados serán devueltos como un objeto WebElement JSON. La siguiente tabla muestra las estrategias de localización que cada servidor debería soportar. Los elementos deben ser devueltos en el pedido ubicado en el DOM.<br>
<br>
<table><thead><tr><th><b>Estrategia</b> </th><th><b>Descripción</b> </th></tr></thead><tbody>
<tr><td> nombre de clase      </td><td> Devuelve todos los elementos cuyo nombre de clase contiene el valor de búsqueda; no se permiten nombres compuestos de clases. </td></tr>
<tr><td> selector de censos    </td><td> Devuelve todos los elementos que coinciden con un selector CSS. </td></tr>
<tr><td> id              </td><td> Devuelve todos los elementos cuyo atributo ID coincide con el valor de búsqueda. </td></tr>
<tr><td> nombre            </td><td> Devuelve todos los elementos cuyo atributo NOMBRE coincide con el valor de búsqueda. </td></tr>
<tr><td> texto del enlace       </td><td> Devuelve todos los elementos de ancla cuyo texto visible coincide con el valor de búsqueda. </td></tr>
<tr><td> texto de enlace parcial </td><td> Devuelve todos los elementos de ancla cuyo texto visible coincide parcialmente con el valor de búsqueda. </td></tr>
<tr><td> nombre de etiqueta        </td><td> Devuelve todos los elementos cuyo nombre de etiqueta coincide con el valor de búsqueda. </td></tr>
<tr><td> xpath           </td><td> Devuelve todos los elementos que coinciden con una expresión XPath. La expresión XPath proporcionada debe aplicarse al servidor "tal cual"; si la expresión no es relativa a la raíz del elemento, el servidor no debería modificarla. En consecuencia, una consulta XPath puede devolver elementos no contenidos en el subárbol del elemento raíz. </td></tr></tbody></table>

</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>usando</code> - <code>{string}</code> La estrategia de localización a utilizar.</dd>
<dd><code>valor</code> - <code>{string}</code> El objetivo de búsqueda.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;{ELEMENT:string}&gt;}</code> A list of WebElement JSON objects for the located elements.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
<dd><code>XPathLookupError</code> - Si usar XPath y la expresión de entrada no es válida.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/click

<dl>
<dd>
<h4>POST /session/:sessionId/element/:id/click</h4>
</dd>
<dd>
<dl>
<dd>Haga clic en un elemento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
<dd><code>ElementNotVisible</code> - Si el elemento referenciado no es visible en la página (ya sea que esté oculto por CSS, tiene 0-anchura o tiene 0-altura)</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/submit

<dl>
<dd>
<h4>POST /session/:sessionId/element/:id/submit</h4>
</dd>
<dd>
<dl>
<dd>Envía un elemento <code>FORM</code>. El comando de envío también se puede aplicar a cualquier elemento que sea un descendiente de un elemento <code>FORM</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/text

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/text</h4>
</dd>
<dd>
<dl>
<dd>Devuelve el texto visible para el elemento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/valor

<dl>
<dd>
<h4>POST /session/:sessionId/element/:id/valor</h4>
</dd>
<dd>
<dl>
<dd>Envía una secuencia de toques clave a un elemento.<br>
<br>
Any UTF-8 character may be specified, however, if the server does not support native key events, it should simulate key strokes for a standard US keyboard layout. Los puntos de código de Unicode <a href='http://unicode.org/faq/casemap_charprop.html#8'>Área de Uso Privado</a> , 0xE000-0xF8FF, se utilizan para representar teclas pressables y no de texto (ver tabla abajo).<br>
<br>
<br>
<table cellpadding='5' cellspacing='5'>
<tbody><tr><td valign='top'>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Código</b> </th></tr></thead><tbody>
<tr><td> NÚLL       </td><td> U+E000      </td></tr>
<tr><td> Cancelar     </td><td> U+E001      </td></tr>
<tr><td> Ayuda       </td><td> U+E002      </td></tr>
<tr><td> Retroceso </td><td> U+E003      </td></tr>
<tr><td> Tab        </td><td> U+E004      </td></tr>
<tr><td> Claro      </td><td> U+E005      </td></tr>
<tr><td> Devuelve<sup>1</sup> </td><td> U+E006      </td></tr>
<tr><td> Introduzca<sup>1</sup> </td><td> U+E007      </td></tr>
<tr><td> Cambio      </td><td> U+E008      </td></tr>
<tr><td> Control    </td><td> U+E009      </td></tr>
<tr><td> Alt        </td><td> U+E00A      </td></tr>
<tr><td> Pausa      </td><td> U+E00B      </td></tr>
<tr><td> Escape     </td><td> U+E00C      </td></tr></tbody></table>

</td><td valign='top'>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Código</b> </th></tr></thead><tbody>
<tr><td> Espacio      </td><td> U+E00D      </td></tr>
<tr><td> Pageup     </td><td> U+E00E      </td></tr>
<tr><td> Pagedown   </td><td> U+E00F      </td></tr>
<tr><td> Fin        </td><td> U+E010      </td></tr>
<tr><td> Inicio       </td><td> U+E011      </td></tr>
<tr><td> Flecha izquierda </td><td> U+E012      </td></tr>
<tr><td> Flecha hacia arriba   </td><td> U+E013      </td></tr>
<tr><td> Flecha derecha </td><td> U+E014      </td></tr>
<tr><td> Flecha abajo </td><td> U+E015      </td></tr>
<tr><td> Insert     </td><td> U+E016      </td></tr>
<tr><td> Eliminar     </td><td> U+E017      </td></tr>
<tr><td> Semicolon  </td><td> U+E018      </td></tr>
<tr><td> Iguales     </td><td> U+E019      </td></tr></tbody></table>

</td><td valign='top'>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Código</b> </th></tr></thead><tbody>
<tr><td> Numpad 0   </td><td> U+E01A      </td></tr>
<tr><td> Numpad 1   </td><td> U+E01B      </td></tr>
<tr><td> Numpad 2   </td><td> U+E01C      </td></tr>
<tr><td> Numpad 3   </td><td> U+E01D      </td></tr>
<tr><td> Numpad 4   </td><td> U+E01E      </td></tr>
<tr><td> Numpad 5   </td><td> U+E01F      </td></tr>
<tr><td> Numpad 6   </td><td> U+E020      </td></tr>
<tr><td> Numpad 7   </td><td> U+E021      </td></tr>
<tr><td> Numpad 8   </td><td> U+E022      </td></tr>
<tr><td> Numpad 9   </td><td> U+E023      </td></tr></tbody></table>

</td><td valign='top'>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Código</b> </th></tr></thead><tbody>
<tr><td> Multiplicar   </td><td> U+E024      </td></tr>
<tr><td> Añadir        </td><td> U+E025      </td></tr>
<tr><td> Separador  </td><td> U+E026      </td></tr>
<tr><td> Restar   </td><td> U+E027      </td></tr>
<tr><td> Decimal    </td><td> U+E028      </td></tr>
<tr><td> Dividir     </td><td> U+E029      </td></tr></tbody></table>

</td><td valign='top'>
<table><thead><tr><th><b>Tecla</b> </th><th><b>Código</b> </th></tr></thead><tbody>
<tr><td> F1         </td><td> U+E031      </td></tr>
<tr><td> F2         </td><td> U+E032      </td></tr>
<tr><td> F3         </td><td> U+E033      </td></tr>
<tr><td> F4         </td><td> U+E034      </td></tr>
<tr><td> F5         </td><td> U+E035      </td></tr>
<tr><td> F6         </td><td> U+E036      </td></tr>
<tr><td> F7         </td><td> U+E037      </td></tr>
<tr><td> F8         </td><td> U+E038      </td></tr>
<tr><td> F9         </td><td> U+E039      </td></tr>
<tr><td> F10        </td><td> U+E03A      </td></tr>
<tr><td> F11        </td><td> U+E03B      </td></tr>
<tr><td> F12        </td><td> U+E03C      </td></tr>
<tr><td> Comando/Meta </td><td> U+E03D      </td></tr></tbody></table>

</td></tr>
<tr><td><sup>1</sup> La clave de retorno es <i>no la misma</i> que la <a href='http://en.wikipedia.org/wiki/Enter_key'>ingrese la tecla</a>.</td></tr></tbody></table>

El servidor debe procesar la secuencia de claves de la siguiente manera:<br>

<ul><li>Cada tecla que aparece en el teclado sin necesidad de modificadores se envía como una tecla hacia abajo, seguida de una tecla hacia arriba.<br>
</li><li>Si el servidor no soporta eventos nativos y debe simular trazos de teclas con JavaScript, debe generar eventos de teclado, teclas y teclas, en ese orden. El evento de la tecla solo debe dispararse cuando la tecla correspondiente es para un carácter imprimible.<br>
</li><li>Si una clave requiere una clave modificadora (p. ej. "!" en un teclado estándar estadounidense), la secuencia es: <var>modificador</var> abajo, <var>tecla</var> abajo, <var>tecla</var> arriba, Modificador <var></var> arriba, donde la tecla <var></var> es el valor de clave ideal sin modificar (usando el ejemplo anterior, un "1").<br>
</li><li>Las teclas de modificador (Ctrl, Mayúsculas, Alt y Comando/Meta) se asumen como "pegajosas"; cada modificador debe mantenerse presionado (p.e. sólo un evento de tecla) hasta que el modificador se encuentre de nuevo en la secuencia, o la tecla <code>NULL</code> (U+E000) se encuentra.<br>
</li><li>Cada secuencia de teclas se termina con una clave implícita <code>NULL</code>. Posteriormente, todas las teclas modificadoras deprimidas deben ser liberadas (con los eventos de teclado correspondientes) al final de la secuencia.<br>
</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>valor</code> - <code>{Array.&lt;string&gt;}</code> La secuencia de claves para escribir. Debe proporcionarse una matriz. El servidor debe aplanar los elementos de la matriz a una sola cadena que se va a teclear.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
<dd><code>ElementNotVisible</code> - Si el elemento referenciado no es visible en la página (ya sea que esté oculto por CSS, tiene 0-anchura o tiene 0-altura)</dd>
</dl>
</dd>
</dl>
</dd>
</li></ul>

---

#### /session/:sessionId/keys

<dl>
<dd>
<h4>POST /session/:sessionId/keys</h4>
</dd>
<dd>
<dl>
<dd>Envía una secuencia de teclas al elemento activo. Este comando es similar al comando <a href='JsonWireProtocol#/session/:sessionId/element/:id/value.md'>enviar las teclas</a> en cada aspecto excepto la terminación implícita: Los modificadores son <b>no</b> liberados al final de la llamada. Más bien, el estado de las teclas modificadoras se mantiene entre las llamadas, así que las interacciones del ratón se pueden realizar mientras se depresionan las teclas modificadoras.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>valor</code> - <code>{Array.&lt;string&gt;}</code> La secuencia de teclas a enviar. La secuencia está definida en el comando<a href='JsonWireProtocol#/session/:sessionId/element/:id/value.md'>enviar las teclas</a>.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/name

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/name</h4>
</dd>
<dd>
<dl>
<dd>Consulta para el nombre de la etiqueta de un elemento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> El nombre de la etiqueta del elemento, como una cadena en minúscula.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/clear

<dl>
<dd>
<h4>POST /session/:sessionId/element/:id/clear</h4>
</dd>
<dd>
<dl>
<dd>Clear a <code>TEXTAREA</code> or <code>text INPUT</code> element's value.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
<dd><code>ElementNotVisible</code> - Si el elemento referenciado no es visible en la página (ya sea que esté oculto por CSS, tiene 0-anchura o tiene 0-altura)</dd>
<dd><code>InválidElementState</code> - Si el elemento referenciado está desactivado.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/seleccionado

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/selected</h4>
</dd>
<dd>
<dl>
<dd>Determinar si un elemento <code>OPTION</code> o un elemento <code>INPUT</code> de tipo <code>checkbox</code> o <code>radiobutton</code> está seleccionado actualmente.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{boolean}</code> Si el elemento está seleccionado.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/habilitado

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/habilitado</h4>
</dd>
<dd>
<dl>
<dd>Determinar si un elemento está habilitado actualmente.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{boolean}</code> Si el elemento está activado.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/attribute/:name

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/attribute/:name</h4>
</dd>
<dd>
<dl>
<dd>Obtener el valor del atributo de un elemento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string|null}</code> The value of the attribute, or null if it is not set on the element.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/equals/:other

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/equals/:other</h4>
</dd>
<dd>
<dl>
<dd>Evalúa si dos IDs de elementos se refieren al mismo elemento DOM.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
<dd><code>:other</code> - ID del elemento a comparar.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{boolean}</code> Si los dos IDs se refieren al mismo elemento.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento al que hace referencia <code>:id</code> o <code>:other</code> ya no está vinculado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/displayed

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/displayed</h4>
</dd>
<dd>
<dl>
<dd>Determinar si un elemento se muestra actualmente.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{boolean}</code> Si se muestra el elemento.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/location

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/location</h4>
</dd>
<dd>
<dl>
<dd>Determinar la ubicación de un elemento en la página. El punto <code>(0, 0)</code> se refiere a la esquina superior izquierda de la página. Las coordenadas del elemento se retornan como un objeto JSON con propiedades <code>x</code> y <code>y</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{x:number, y:number}</code> Las coordenadas X e Y del elemento de la página.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/location\_in\_view

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/location_in_view</h4>
</dd>
<dd>
<dl>
<dd>Determina la ubicación de un elemento en la pantalla una vez que se ha desplazado a la vista.<br>
<br>
<b>Nota:</b> Esto se considera un comando interno y debe <b>sólo</b> ser utilizado para determinar la ubicación de un elemento<br>
para generar correctamente eventos nativos.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{x:number, y:number}</code> Las coordenadas X e Y del elemento.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/size

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/size</h4>
</dd>
<dd>
<dl>
<dd>Determina el tamaño de un elemento en píxeles. El tamaño se devolverá como un objeto JSON con propiedades <code>ancho</code> y <code>altura</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{width:number, height:number}</code> El ancho y la altura del elemento, en píxeles.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/element/:id/css/:propertyName

<dl>
<dd>
<h4>GET /session/:sessionId/element/:id/css/:propertyName</h4>
</dd>
<dd>
<dl>
<dd>Consulta el valor de la propiedad CSS computada de un elemento. La propiedad CSS a consultar debe especificarse usando el nombre de propiedad CSS, <b>no</b> el nombre de la propiedad JavaScript (e. . <code>color de fondo</code> en lugar de <code>fondo Color</code>).</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:id</code> - ID del elemento al que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> El valor de la propiedad CSS especificada.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
<dd><code>StaleElementReference</code> - Si el elemento referenciado por <code>:id</code> ya no está conectado al DOM de la página.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/orientation

<dl>
<dd>
<h4>GET /session/:sessionId/orientation</h4>
</dd>
<dd>
<dl>
<dd>Obtener la orientación actual del navegador. El servidor debe devolver un valor de orientación válido como se define en <a href='http://selenium.googlecode.com/git/docs/api/java/org/openqa/selenium/ScreenOrientation.html'>ScreenOrientation</a>: <code>{LANDSCAPE|PORTRAIT}</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> La orientación actual del navegador correspondiente a un valor definido en <a href='http://selenium.googlecode.com/git/docs/api/java/org/openqa/selenium/ScreenOrientation.html'>ScreenOrientation</a>: <code>{LANDSCAPE|PORTRAIT}</code>.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/orientation</h4>
</dd>
<dd>
<dl>
<dd>Establecer la orientación del navegador. La orientación debe especificarse como se define en <a href='http://selenium.googlecode.com/git/docs/api/java/org/openqa/selenium/ScreenOrientation.html'>ScreenOrientation</a>: <code>{LANDSCAPE|PORTRAIT}</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>orientación</code> - <code>{string}</code> La nueva orientación del navegador como se define en <a href='http://selenium.googlecode.com/git/docs/api/java/org/openqa/selenium/ScreenOrientation.html'>ScreenOrientation</a>: <code>{LANDSCAPE|PORTRAIT}</code>.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/alert\_texto

<dl>
<dd>
<h4>GET /session/:sessionId/alert_text</h4>
</dd>
<dd>
<dl>
<dd>Obtiene el texto de la visualización actual de JavaScript <code>alert()</code>, <code>confirmar</code>o <code>prompt()</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{string}</code> El texto de la alerta que se muestra actualmente.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoAlertPresent</code> - Si no se muestra ninguna alerta.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/alert_text</h4>
</dd>
<dd>
<dl>
<dd>Envía toques de teclado a un diálogo <code>prompt()</code>.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>texto</code> - <code>{string}</code> golpes de teclado para enviar al diálogo <code>prompt()</code>.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoAlertPresent</code> - Si no se muestra ninguna alerta.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/accept\_alert

<dl>
<dd>
<h4>POST /session/:sessionId/accept_alert</h4>
</dd>
<dd>
<dl>
<dd>Acepta el diálogo de alerta que se muestra actualmente. Normalmente, esto equivale a hacer clic en el botón 'OK' en el diálogo.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoAlertPresent</code> - Si no se muestra ninguna alerta.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/dismiss\_alert

<dl>
<dd>
<h4>POST /session/:sessionId/dismiss_alert</h4>
</dd>
<dd>
<dl>
<dd>Descarta el diálogo de alerta que se muestra actualmente. Para los diálogos <code>confirm()</code> y <code>prompt()</code> , esto es equivalente a hacer clic en el botón 'Cancelar'. Para diálogos <code>alert()</code> , esto es equivalente a hacer clic en el botón 'OK'.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoAlertPresent</code> - Si no se muestra ninguna alerta.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/moveto

<dl>
<dd>
<h4>POST /session/:sessionId/moveto</h4>
</dd>
<dd>
<dl>
<dd>Mueva el ratón por un desplazamiento del elemento especificado. Si no se especifica ningún elemento, el movimiento es relativo al cursor actual del ratón. Si se proporciona un elemento pero no se desplaza, el ratón se moverá al centro del elemento. Si el elemento no es visible, será desplazado a la vista.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>element</code> - <code>{string}</code> ID opaco asignado al elemento al que mover, como se describe en el objeto WebElement JSON. Si no se especifica o es nulo, el desplazamiento es relativo a la posición actual del ratón.</dd>
<dd><code>xoffset</code> - <code>{number}</code> desplazamiento X al que mover, en relación con la esquina superior izquierda del elemento. Si no se especifica, el ratón se moverá al centro del elemento.</dd>
<dd><code>yoffset</code> - <code>{number}</code> Y desplazamiento al que mover, en relación con la esquina superior izquierda del elemento. Si no se especifica, el ratón se moverá al centro del elemento.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/click

<dl>
<dd>
<h4>POST /session/:sessionId/click</h4>
</dd>
<dd>
<dl>
<dd>Haga clic en cualquier botón del ratón (en las coordenadas definidas por el último comando de movet). Tenga en cuenta que llamar este comando después de llamar al botón y antes de llamar al botón arriba (o a cualquier secuencia de interacciones fuera de orden) producirá un comportamiento indefinido).</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>button</code> - <code>{number}</code> Cual botón, enum: <code>{LEFT = 0, MIDDLE = 1 , DERECHO = 2}</code>. Por defecto es el botón izquierdo del ratón si no se especifica.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/buttondown

<dl>
<dd>
<h4>POST /session/:sessionId/buttondown</h4>
</dd>
<dd>
<dl>
<dd>Haga clic y mantenga pulsado el botón izquierdo del ratón (en las coordenadas fijadas por el último comando de move). Tenga en cuenta que el siguiente comando relacionado con el ratón que debería seguir es el botón . Cualquier otro comando del ratón (como clic u otra llamada al botón) producirá un comportamiento indefinido.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>button</code> - <code>{number}</code> Cual botón, enum: <code>{LEFT = 0, MIDDLE = 1 , DERECHO = 2}</code>. Por defecto es el botón izquierdo del ratón si no se especifica.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/buttonup

<dl>
<dd>
<h4>POST /session/:sessionId/buttonup</h4>
</dd>
<dd>
<dl>
<dd>Libera el botón del ratón previamente presionado (donde el ratón está actualmente). Debe llamarse una vez por cada comando de botón. Vea la nota con clic y botón sobre las implicaciones de los comandos fuera de orden.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>button</code> - <code>{number}</code> Cual botón, enum: <code>{LEFT = 0, MIDDLE = 1 , DERECHO = 2}</code>. Por defecto es el botón izquierdo del ratón si no se especifica.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/doubleclick

<dl>
<dd>
<h4>POST /session/:sessionId/doubleclick</h4>
</dd>
<dd>
<dl>
<dd>Haga doble clic en las coordenadas actuales del ratón (definidas por moveto).</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/touch/click

<dl>
<dd>
<h4>POST /session/:sessionId/touch/click</h4>
</dd>
<dd>
<dl>
<dd>Toque un solo en el dispositivo habilitado.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>elemento</code> - <code>{string}</code> ID del elemento en el que tocar un solo toque.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/touch/down

<dl>
<dd>
<h4>POST /session/:sessionId/touch/down</h4>
</dd>
<dd>
<dl>
<dd>Dedo abajo en la pantalla.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>x</code> - <code>{number}</code> coordenada X en la pantalla.</dd>
<dd><code>y</code> - <code>{number}</code> coordenada Y en la pantalla.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/touch/up

<dl>
<dd>
<h4>POST /session/:sessionId/touch/up</h4>
</dd>
<dd>
<dl>
<dd>Deduzca en la pantalla.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>x</code> - <code>{number}</code> coordenada X en la pantalla.</dd>
<dd><code>y</code> - <code>{number}</code> coordenada Y en la pantalla.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/tocar/mover

<dl>
<dd>
<h4>POST sesión/:sessionId/tocar/mover</h4>
</dd>
<dd>
<dl>
<dd>Mover el dedo en la pantalla.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>x</code> - <code>{number}</code> coordenada X en la pantalla.</dd>
<dd><code>y</code> - <code>{number}</code> coordenada Y en la pantalla.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/touch/scroll

<dl>
<dd>
<h4>Sesión POST/:sessionId/touch/scroll</h4>
</dd>
<dd>
<dl>
<dd>Desplácese en la pantalla táctil utilizando eventos de movimiento basados en dedos. Utilice este comando para comenzar a desplazarse en una ubicación de pantalla en particular.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>element</code> - <code>{string}</code> ID del elemento donde comienza el desplazamiento.</dd>
<dd><code>xoffset</code> - <code>{number}</code> El desplazamiento x en píxeles para desplazar.</dd>
<dd><code>yoffset</code> - <code>{number}</code> El desplazamiento y en píxeles hacia adentro.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/touch/scroll

<dl>
<dd>
<h4>Sesión POST/:sessionId/touch/scroll</h4>
</dd>
<dd>
<dl>
<dd>Desplácese en la pantalla táctil utilizando eventos de movimiento basados en dedos. Utilice este comando si no le importa dónde se inicia el desplazamiento en la pantalla.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>xoffset</code> - <code>{number}</code> El desplazamiento x en píxeles a desplazar.</dd>
<dd><code>yoffset</code> - <code>{number}</code> El desplazamiento y en píxeles a desplazar.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/touch/doubleclick

<dl>
<dd>
<h4>Sesión POST/:sessionId/touch/doubleclick</h4>
</dd>
<dd>
<dl>
<dd>Doble toque en la pantalla táctil usando eventos de movimiento de dedos.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>elemento</code> - <code>{string}</code> ID del elemento en el que tocar doble.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/touch/longclick

<dl>
<dd>
<h4>POST session/:sessionId/touch/longclick</h4>
</dd>
<dd>
<dl>
<dd>Pulsación larga en la pantalla táctil usando eventos de movimiento de dedos.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>element</code> - <code>{string}</code> ID del elemento al que se va a mantener presionado.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/touch/flick

<dl>
<dd>
<h4>Sesión POST/:sessionId/touch/flick</h4>
</dd>
<dd>
<dl>
<dd>Desliza en la pantalla táctil usando eventos de movimiento de dedos. Este comando de parpadeo comienza en una ubicación de la pantalla de particulatos.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>elemento</code> - <code>{string}</code> ID del elemento donde comienza el parpadeo.</dd>
<dd><code>xoffset</code> - <code>{number}</code> El desplazamiento x en píxeles para flicear.</dd>
<dd><code>yoffset</code> - <code>{number}</code> El desplazamiento y en píxeles a los que parpadear.</dd>
<dd><code>velocidad</code> - <code>{number}</code> La velocidad en píxeles por segundos.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### sesión/:sessionId/touch/flick

<dl>
<dd>
<h4>Sesión POST/:sessionId/touch/flick</h4>
</dd>
<dd>
<dl>
<dd>Desliza en la pantalla táctil usando eventos de movimiento de dedos. Utilice este comando de flick si no le importa dónde comienza el flick en la pantalla.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>xspeed</code> - <code>{number}</code> La velocidad x en píxeles por segundo.</dd>
<dd><code>velocidad</code> - <code>{number}</code> Velocidad y en píxeles por segundo.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /sesión/:sessionId/ubicación

<dl>
<dd>
<h4>GET /session/:sessionId/location</h4>
</dd>
<dd>
<dl>
<dd>Obtener la geolocalización actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{latitude: number, longitude: number, altitude: number}</code> La geolocalización actual.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/location</h4>
</dd>
<dd>
<dl>
<dd>Establecer la geolocalización actual.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>ubicación</code> - <code>{latitude: number, longitude: number, altitude: number}</code> La nueva ubicación.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/local\_storage

<dl>
<dd>
<h4>GET /session/:sessionId/local_storage</h4>
</dd>
<dd>
<dl>
<dd>Obtener todas las claves del almacenamiento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;string&gt;}</code> La lista de claves.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/local_storage</h4>
</dd>
<dd>
<dl>
<dd>Establece el elemento de almacenamiento para la clave dada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>tecla</code> - <code>{string}</code> La clave a establecer.</dd>
<dd><code>valor</code> - <code>{string}</code> El valor a establecer.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId/local_storage</h4>
</dd>
<dd>
<dl>
<dd>Limpiar el almacenamiento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/local\_storage/key/:key

<dl>
<dd>
<h4>GET /session/:sessionId/local_storage/key/:key</h4>
</dd>
<dd>
<dl>
<dd>Obtener el elemento de almacenamiento para la clave dada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:key</code> - La clave a obtener.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId/local_storage/key/:key</h4>
</dd>
<dd>
<dl>
<dd>Elimina el elemento de almacenamiento de la clave dada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:key</code> - La clave a eliminar.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/local\_storage/size

<dl>
<dd>
<h4>GET /session/:sessionId/local_storage/size</h4>
</dd>
<dd>
<dl>
<dd>Obtener el número de elementos en el almacenamiento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{number}</code> El número de elementos en el almacenamiento.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/session\_storage

<dl>
<dd>
<h4>GET /session/:sessionId/session_storage</h4>
</dd>
<dd>
<dl>
<dd>Obtener todas las claves del almacenamiento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;string&gt;}</code> La lista de claves.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>POST /session/:sessionId/session_storage</h4>
</dd>
<dd>
<dl>
<dd>Establece el elemento de almacenamiento para la clave dada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>tecla</code> - <code>{string}</code> La clave a establecer.</dd>
<dd><code>valor</code> - <code>{string}</code> El valor a establecer.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId/session_storage</h4>
</dd>
<dd>
<dl>
<dd>Limpiar el almacenamiento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/session\_storage/key/:key

<dl>
<dd>
<h4>GET /session/:sessionId/session_storage/key/:key</h4>
</dd>
<dd>
<dl>
<dd>Obtener el elemento de almacenamiento para la clave dada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:key</code> - La clave a obtener.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

<dl>
<dd>
<h4>DELETE /session/:sessionId/session_storage/key/:key</h4>
</dd>
<dd>
<dl>
<dd>Elimina el elemento de almacenamiento de la clave dada.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
<dd><code>:key</code> - La clave a eliminar.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/session\_storage/size

<dl>
<dd>
<h4>GET /session/:sessionId/session_storage/size</h4>
</dd>
<dd>
<dl>
<dd>Obtener el número de elementos en el almacenamiento.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{number}</code> El número de elementos en el almacenamiento.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Errores potenciales:</b></dt>
<dd><code>NoSuchWindow</code> - Si la ventana seleccionada ha sido cerrada.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/log

<dl>
<dd>
<h4>POST /session/:sessionId/log</h4>
</dd>
<dd>
<dl>
<dd>Obtener el registro para un tipo de registro determinado. El búfer de registro se restablece después de cada petición.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Parámetros JSON:</b></dt>
<dd><code>type</code> - <code>{string}</code> El tipo <a href='#Log_Type.md'>de registro</a>. Esto es algo que hay que hacer.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;object&gt;}</code> The list of <a href='#Log_Entry_JSON_Object.md'>log entries</a>.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/log/types

<dl>
<dd>
<h4>GET /session/:sessionId/log/types</h4>
</dd>
<dd>
<dl>
<dd>Obtener tipos de registro disponibles.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{Array.&lt;string&gt;}</code> La lista de registros <a href='#Log_Type.md'>disponibles tipos</a>.</dd>
</dl>
</dd>
</dl>
</dd>
</dl>

---

#### /session/:sessionId/application\_cache/status

<dl>
<dd>
<h4>GET /session/:sessionId/application_cache/status</h4>
</dd>
<dd>
<dl>
<dd>Obtener el estado de la caché de aplicaciones html5.</dd>
<dd>
<dl>
<dt><b>Parámetros URL:</b></dt>
<dd><code>:sessionId</code> - ID de la sesión a la que enrutar el comando.</dd>
</dl>
</dd>
<dd>
<dl>
<dt><b>Devuelve:</b></dt>
<dd><code>{number}</code> Código de estado para el caché de la aplicación: {UNCACHED = 0, IDLE = 1, CHECKING = 2, DOWNLOADING = 3, UPDATE_READY = 4, OBSOLETE = 5}</dd>
</dl>
</dd>
</dl>
</dd>
</dl>
