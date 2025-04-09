---
title: Observabilidad en Selenium Grid
linkTitle: Observabilidad
weight: 1
aliases:
  - /documentation/es/grid/grid_4/avanzado_características/observabilidad/
---

## Tabla de contenidos

- [Selenium Grid](#selenium-grid)
- [Observability](#observability)
 - [Rastreo distribuido](#distributed-tracing)
 - [Registro de eventos](#event-logging)
- [Observabilidad de cuadrícula](#grid-observability)
 - [Rastros de visualización](#visualizing-traces)
 - [Registros de eventos de apalancamiento](#leveraging-event-logs)
- [References](#references)

## Selenium Grid

Grid ayuda a escalar y distribuir pruebas mediante la ejecución de pruebas en varias combinaciones de navegadores y sistemas operativos.

## Observabilidad

La observabilidad tiene tres pilares: trazas, métricas y troncos. Dado que Selenium Grid 4 está diseñado para ser completamente distribuido, la observabilidad hará que sea más fácil entender y depurar los internos.

## Rastreo distribuido

Una sola solicitud o transacción abarca múltiples servicios y componentes.  Rastrear el ciclo de vida de la petición a medida que cada servicio ejecuta la solicitud. Es útil para depurar en un escenario de error.
Algunos términos clave usados en el contexto de rastreo son:

**Trámite**
El seguimiento permite rastrear una solicitud a través de múltiples servicios, comenzando desde su origen hasta su destino final. El viaje de esta solicitud ayuda a depurar, controlar el flujo de extremo a extremo e identificar fallos. Una traza representa el flujo de petición de extremo a extremo. Cada trace tiene un identificador único como su identificador.

**España**
Cada rastro se compone de operaciones temporizadas llamadas espacios. Un span tiene una hora de inicio y fin y representa las operaciones realizadas por un servicio. La granularidad de la superficie depende de cómo se instrumente. Cada span tiene un identificador único.  Todos los spans dentro de un trace tienen el mismo trace id.

\*\*Atributos de Span **Atributos**
Los atributos de Span son pares clave-valor que proporcionan información adicional sobre cada espacio.

**Eventos**
Los eventos son registros con sello de tiempo dentro de un lapso de tiempo. Proporcionan un contexto adicional a las franjas existentes. Los eventos también contienen pares clave-valor como atributos de eventos.

## Registro de eventos

El registro es esencial para depurar una aplicación. El registro a menudo se realiza en un formato legible por humanos. Pero para que las máquinas busquen y analicen los registros, tiene que tener un formato bien definido. El registro estructurado es una práctica común de grabar registros consistentemente en un formato fijo. Contiene comúnmente campos como:

- Timestamp
- Nivel de registro
- Clase Logger
- Mensaje de registro (esto se divide en campos relevantes para la operación donde se registró el registro)

Los registros y eventos están estrechamente relacionados. Los eventos encapsulan toda la información posible disponible para realizar una sola unidad de trabajo. Los registros son esencialmente subconjuntos de un evento. En el fondo, ambas ayudas para la depuración.
Consulte los siguientes recursos para una comprensión detallada:

1. [https://www.honeycomb.io/blog/how-are-structured-logs-different-from-events/](https://www.honeycomb.io/blog/how-are-structured-logs-different-from-events/)
2. [https://charity.wtf/2019/02/05/logs-vs-structured-events/](https://charity.wtf/2019/02/05/logs-vs-structured-events/)

## Observabilidad de cuadrícula

Selenium server está instrumentado con seguimiento usando OpenTelemetry. Cada petición al servidor se rastrea de principio a fin. Cada trace consiste en una serie de spans ya que una petición se ejecuta dentro del servidor.
La mayoría de las partidas en el servidor de Selenium consisten en dos eventos:

1. Evento normal - Graba toda la información sobre una unidad de trabajo y marca la finalización exitosa de la obra.
2. Evento de error - registra toda la información hasta que ocurre el error y luego registra la información del error. Marca un evento de excepción.

Ejecutando servidor de Selenium

1. [Standalone](https://github.com/SeleniumHQ/selenium/wiki/Selenium-Grid-4#standalone-mode)
2. [Hub y Nodo](https://github.com/SeleniumHQ/selenium/wiki/Selenium-Grid-4#hub-and-node)
3. [Distribuido completamente](https://github.com/SeleniumHQ/selenium/wiki/Selenium-Grid-4#fully-distributed)
4. [Docker](https://github.com/SeleniumHQ/selenium/wiki/Selenium-Grid-4#using-docker)

## Visualizando huellas

Todos los espacios, eventos y sus respectivos atributos forman parte de un trazado. Seguimiento funciona mientras se ejecuta el servidor en todos los modos mencionados anteriormente.

De forma predeterminada, el seguimiento está activado en el servidor Selenium. El servidor Selenium exporta las huellas a través de dos exportadores:

1. Consola - Registra todos los rastros y sus spans incluidos a nivel FINE. De forma predeterminada, Selenium imprime registros a nivel INFO o superior.
 La bandera **nivel de registro** se puede usar para pasar un nivel de registro de elección mientras se ejecuta el jarro o jarras Selenium Grid.

```shell
java -jar selenium-server-4.0.0-<selenium-version>.jar standalone --log-level FINE
```

2. Jaeger UI - OpenTelemetry proporciona las APIs y SDKs a trazas de instrumentos en el código. Whereas Jaeger es un sistema de rastreo, que ayuda a recolectar los datos de la telemetría y a proporcionar consultas, filtrado y visualización de características para los datos.

Instrucciones detalladas para visualizar trazos usando la interfaz de usuario de Jaeger se pueden obtener ejecutando el comando:

```shell
java -jar selenium-server-4.0.0-<selenium-version>seguimiento de información .jar
```

[Un muy buen ejemplo y scripts para ejecutar el servidor y enviar traces a Jaeger](https://github.com/manoj9788/tracing-selenium-grid)

## Apalancamiento de registros de eventos

El seguimiento también debe estar habilitado para el registro de eventos, incluso si uno no desea exportar trazas para visualizarlas.\
**Por defecto, el seguimiento está habilitado. No es necesario pasar ningún parámetro adicional para ver los registros en la consola.**
Todos los eventos dentro de un lapso se registran en el nivel FINE. Los eventos de error se registran a nivel de Guerra.

Todos los registros de eventos tienen los siguientes campos:

| Campo                | Valor del campo     | Descripción                                                                                                                                                                                                                                     |
| -------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hora del evento      | eventId             | Marca de tiempo del registro de eventos en nanosegundos de epoch.                                                                                                                                                               |
| Traza Id             | Id tracado          | Cada trace es identificado de forma única por un trace id.                                                                                                                                                                      |
| Id de Span           | spanId              | Cada tramo dentro de un rastro se identifica de forma única por un span id.                                                                                                                                                     |
| Span Kind            | spanKind            | El tipo Span es una propiedad que indica el tipo de span. Ayuda a comprender la naturaleza de la unidad de trabajo realizada por el español.                                                                    |
| Nombre del evento    | eventName           | Este mapea al mensaje de registro.                                                                                                                                                                                              |
| Atributos del evento | atributos de evento | Esto forma el quid de los registros de eventos, basado en la operación ejecutada, tiene pares de clave-valor con formato JSON. Esto también incluye un atributo de clase handler, para mostrar la clase logger. |

Registro de ejemplo

    FINE [LoggingOptions$1.lambda$export$1] - {
      "traceId": "fc8aef1d44b3cc8bc09eb8e581c4a8eb",
      "spanId": "b7d3b9865d3ddd45",
      "spanKind": "INTERNAL",
      "eventTime": 1597819675128886121,
      "eventName": "Ejecución de la solicitud de sesión completada",
      "atributos": {
        "http. tatus_code": 200,
        "http.handler_class": "org.openqa.selenium.grid.router.HandleSession",
        "http. rl": "\u002fsesión\u002fdd35257f104bb43fdfb06242953f4c85",
        "http. ethod": "DELETE",
        "session.id": "dd35257f104bb43fdfb06242953f4c85"
      }
    }

Además de los campos de arriba, basado en [especificación OpenTelemetry](https://github.com/open-telemetry/opentelemetry-specification/blob/master/specification/trace/semantic_conventions/exceptions.md) registros de error consisten en:

| Campo                | Valor del campo                      | Descripción                                                                                                                                           |
| -------------------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tipo de excepción    | exception.type       | El nombre de la clase de la excepción.                                                                                                |
| Mensaje de excepción | exception.message    | Motivo de la excepción.                                                                                                               |
| Excepción stacktrace | exception.stacktrace | Muestra la pila de llamadas en el momento en que se lanzó la excepción. Ayuda a comprender el origen de la excepción. |

Registro de errores de ejemplo

    WARN [LoggingOptions$1.lambda$export$1] - {
      "traceId": "7efa5ea57e02f89cdf8de586fe09f564",
      "spanId": "914df6bc9a1f6e2b",
      "spanKind": "INTERNAL",
      "eventTime": 1597820253450580272,
      "eventName": "exception",
      "attributes": {
        "exception. ype": "org.openqa.selenium.ScriptTimeoutException",
        "exception.message": "Unable to execute request: java.sql.SQLSyntaxErrorException: Table '(0)[video] ql. essions_mappa' no existe ..." (el mensaje completo será impreso),
        "exception.stacktrace": "org.openqa.selenium.ScriptTimeoutException: java. ql.SQLSyntaxErrorException: Tabla '/etcql.sessions_mappa' no existe\nBuild info: version: '4.0.0-alpha-7', revision: 'Desconocido'\nInformación del sistema: host: 'XYZ-MacBook-Pro. ocal', ip: 'fe80:0:0:0:10d5:b63a:bdc6:1%en0', os.name: 'Mac OS X', os.arch: 'x86_64', os.version: '10.13.6', java. ersion: '11.0.7'\nDriver info: driver.version: unknown ...." (stack completo será impreso),
        "http.handler_class": "org.openqa.selenium. rid.distributor.remote.RemoteDistributor",
        "http.url": " Sesión\u002f",
        "http.method": "POST"
      }
    }

Nota: Los registros son bastante impresos arriba para legibilidad. La impresión pretty para los registros está desactivada en el servidor Selenium.

Los pasos anteriores deberían configurarte para ver trazas y registros.

## Referencias

1. [Rastreo Entendido](https://lightstep.com/blog/opentelemetry-101-what-is-tracing/)
2. [Especificación de la API de seguimiento de OpenTelemetry ] (https://github.com/open-telemetry/opentelemetry-specification/blob/master/specification/trace/api.md#status)
3. [Selenium Wiki](https://github.com/SeleniumHQ/selenium/wiki)
4. [Registros estructurados vs eventos](https://www.honeycomb.io/blog/how-are-structured-logs-different-from-events/)
5. [Jaeger framework](https://github.com/jaegertracing/jaeger)
