---
title: Registrando comandos de Selenium
linkTitle: Loggando
weight: 4
description: |
  Obtener información sobre la ejecución de Selenium.
---

Activar el registro es una forma valiosa de obtener información adicional que puede ayudarte a determinar
por qué podría estar teniendo un problema.

## Obteniendo un Logger

{{< tabpane text=verdad >}}

{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L31" >}}

{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L5" >}}

Para guardar los registros en un archivo, puedes hacer esto:

```py
log_path = '/ruta/a/log'
handler = logging.FileHandler(log_path)
logger.addHandler(handler)
```

Para mostrar los registros en la consola, puedes hacer esto:

```py
handler = logging.StreamHandler()
logger.addHandler(handler)
```

{{% /tab %}}
{{% tab header="CSharp" %}}
. ET logger se administra con una clase estática, por lo que todo el acceso al registro se gestiona simplemente haciendo referencia a `Log` desde el namespace `OpenQA.Selenium.Internal.Logging`.
{{% /tab %}}
{{% tab header="Ruby" %}}
If you want to see as much debugging as possible in all the classes,
you can turn on debugging globally in Ruby by setting `$DEBUG = true`.

Para un control más ajustado, Ruby Selenium creó su propia clase Logger para envolver la clase predeterminada `Logger`.
Esta implementación proporciona algunas características adicionales interesantes.
Obtén el registrador directamente desde el método de clase `#logger`en el módulo `Selenium::WebDriver`:

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L11" >}}

```javascript
const logging = require('selenium-webdriver/lib/logging')
logger = logging.getLogger('webdriver')
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

## Nivel de Logger

El nivel de Logger ayuda a filtrar los registros basándose en su gravedad.

{{< tabpane text=verdad >}}

{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L32-L35" >}}

{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L7" >}}

Para mostrar siempre registros con PyTest necesitas ejecutar con argumentos adicionales.
Primero, `-s` para evitar que PyTest capture la consola.
Second, `-p no:logging`, which allows you to override the default PyTest logging settings so logs can
be displayed regardless of errors.

Así que necesitas establecer estas banderas en tu IDE, o ejecutar PyTest en línea de comandos como:

```bash
pytest -s -p no:logging
```

Finalmente, como desactivaste el registro en los argumentos anteriores, ahora necesitas añadir configuración a
volver a activar.

```py
logging.basicConfig(level=logging.WARN)
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET tiene 6 niveles de registro: `Error`, `Warn`, `Info`, `Debug`, `Trace` y `Ning`. El nivel por defecto es `Info`.

{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Troubleshooting/LoggingTest.cs#L18" >}}

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L13" >}}

Para cambiar el nivel del registrador:

```javascript
logger.setLevel(logging.Level.INF)?
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

### Elementos Accionables

Las cosas se registran como advertencias si son algo en lo que el usuario necesita actuar. Esto se utiliza a menudo
para las desaprobaciones. Por varias razones, el proyecto Selenium no sigue las prácticas de Versionamiento Semántico estándar.
Nuestra política es marcar las cosas como obsoletas para 3 lanzamientos y luego eliminarlas, así que las desaprobaciones
pueden ser registradas como advertencias.

{{< tabpane text=verdad >}}

Ejemplo:

```text
8 de mayo de 2023 9:23:38 dev.selenium.troubleshooting.LoggingTest logging
ADVERTENCIA: esta es una advertencia
```

{{% /tab %}}
{{% tab header="Python" %}}
Python registra contenido accionable a nivel de logger — `WARNING`
Los detalles sobre las desaprobaciones se registran en este nivel.

Ejemplo:

```text
ADVERTENCIA selenium:test_logging.py:23 esta es una advertencia
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET registra contenido accionable en el nivel de logger `Warn`.

Ejemplo:

```text
11:04:40.986 WARN LoggingTest: esta es una advertencia
```

{{% /tab %}}
{{% tab header="Ruby" %}}
Ruby registra contenido accionable a nivel de logger — `:warn`.
Los detalles sobre las desaprobaciones se registran en este nivel.

Por ejemplo:

```text
2023-05-08 20:53:13 ATENCIA Selenium [:example_id] esta es una advertencia 
```

  {{< tab header="JavaScript" >}}
  {{< alert-content >}}
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

### Información útil

Este es el nivel por defecto en el que Selenium registra cosas que los usuarios deben tener en cuenta, pero no necesitan tomar acciones.
Esto puede hacer referencia a un nuevo método o dirigir a los usuarios a más información sobre algo

{{< tabpane text=verdad >}}

Ejemplo:

```text
May 08, 2023 9:23:38 PM dev.selenium.troubleshooting.LoggingTest logging
INFO: esta es información útil
```

{{% /tab %}}
{{% tab header="Python" %}}
Python registra información útil a nivel de registrador — `INFO`

Ejemplo:

```text
INFO selenium:test_logging.py:22 esta es información útil
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET registra información útil en el nivel de logger `Info`.

Ejemplo:

```text
11:04:40.986 INFO LoggingTest: esta es información útil
```

{{% /tab %}}
{{% tab header="Ruby" %}}
Ruby registra información útil a nivel de logger — `:info`.

Ejemplo:

```text
2023-05-08 20:53:13 INFO Selenium [:example_id] esta es información útil 
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

### Detalles de depuración

El nivel de registro de depuración se utiliza para obtener información que puede ser necesaria para diagnosticar problemas y solucionar problemas.

{{< tabpane text=verdad >}}

Ejemplo:

```text
May 08, 2023 9:23:38 PM dev.selenium.troubleshooting.LoggingTest logging
FINE: esto es información detallada de depuración
```

{{% /tab %}}
{{% tab header="Python" %}}
Python registra los detalles de depuración a nivel del registrador — `DEBUG`

Ejemplo:

```text
DEBUG selenium:test_logging.py:24 esta es información detallada de depuración
```

{{% /tab %}}
{{% tab header="CSharp" %}}
.NET registra la mayor parte del contenido de depuración en el nivel de logger `Debug`.

Ejemplo:

```text
11:04:40.986 DEBUG LoggingTest: esta es información detallada de depuración
```

{{% /tab %}}
{{% tab header="Ruby" %}}
Ruby solo proporciona un nivel para la depuración, así que todos los detalles están en el nivel de logger — `:debug`.

Ejemplo:

```text
2023-05-08 20:53:13 DEBUG Selenium [:example_id] esto es información detallada de depuración 
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

## Logger output

Los registros pueden mostrarse en la consola o almacenarse en un archivo. Los diferentes idiomas tienen valores por defecto diferentes.

{{< tabpane text=verdad >}}

{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L37-L38" >}}
{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L9-L10" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Troubleshooting/LoggingTest.cs#L20" >}}

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L15" >}}

Para enviar registros a la salida de la consola:

```javascript
logging.installConsoleHandler()
```

  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}

## Filtrado de Logger

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/troubleshooting/LoggingTest.java#L40-L41" >}}
  {{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/troubleshooting/test_logging.py#L12-L13" >}}
  {{< /tab >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Troubleshooting/LoggingTest.cs#L22-L23" >}}

{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#17" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/ruby/spec/troubleshooting/logging_spec.rb#L18" >}}
  {{< tab header="JavaScript" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
  {{< alert-content >}}
{{< /alert-content >}}
  {{< /tab >}}
{{< /tabpane >}}
