---
title: Sesiones de conductor
linkTitle: Conductores
weight: 3
---

Iniciar y detener una sesión es para abrir y cerrar un navegador.

## Creando Sesiones

Crear una nueva sesión corresponde al comando del W3C para [Nueva sesión](https://w3c.github.io/webdriver/#new-session)

La sesión se crea automáticamente inicializando un nuevo objeto de clase Driver .

Cada idioma permite crear una sesión con argumentos de una de estas clases (o equivalentes):

- [Options]({{< ref "opciones. d" >}}) para describir el tipo de sesión que desee; los valores por defecto se utilizan para local, pero
  esto es necesario para el control remoto
- Alguna forma de [configuración de cliente HTTP]({{< ref "http_client.md" >}}) (la implementación varía entre idiomas)
- [Listeners]({{< ref "listeners.md" >}})

### Controlador local

El argumento único principal para iniciar un controlador local incluye información acerca de cómo iniciar el servicio de controlador requerido
en la máquina local.

- El objeto [Service]({{< ref "service.md" >}}) sólo se aplica a los controladores locales y proporciona información sobre el controlador
  del navegador

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/drivers/OptionsTest.java#L23" >}}
{{< /tab >}}
{{< gh-codeblock path="ejemplos/python/tests/drivers/test_options.py#L9" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/BaseTest.cs#L42" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/drivers/options_spec.rb#L14" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/drivers/service.spec.js#L32-L36" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Controlador remoto

El argumento único principal para iniciar un controlador remoto incluye información sobre dónde ejecutar el código.
Lee los detalles en la [Sección de Controlador Remote]({{< ref "remote_webdriver.md" >}})

## Saliendo de sesiones

Salir de una sesión corresponde al comando W3C para [Eliminando una Sesión](https://w3c.github.io/webdriver/#delete-session).

Nota importante: el método `quit` es diferente del método `close`,
y se recomienda usar siempre `quit` para terminar la sesión

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L29" >}}
{{< /tab >}}
{{< gh-codeblock path="ejemplos/python/tests/drivers/test_options.py#L11" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L28" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/drivers/options_spec.rb#L16" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L28" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L35" >}}
{{< /tab >}}
{{< /tabpane >}}
