---
title: Escribe tu primer script de Selenium
linkTitle: Primer script
weight: 8
description: |
  Instrucciones paso a paso para construir un script de Selenium
---

Una vez que tengas [Selenium instalado]({{< ref "install_library.md" >}}),
estás listo para escribir el código de Selenium.

## Ocho componentes básicos

Todo lo que Selenium hace es enviar los comandos del navegador para hacer algo o enviar solicitudes de información.
La mayoría de lo que harás con Selenium es una combinación de estos comandos básicos

Haga clic en el enlace "Ver ejemplo completo en GitHub" para ver el código en contexto.

### 1. Iniciar la sesión

Para más detalles sobre cómo iniciar una sesión, lea nuestra documentación sobre [sesiones de controladores]({{< ref "../drivers/" >}})

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L12" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L4" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L11" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L3" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L8" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L16" >}}
{{< /tab >}}
{{< /tabpane >}}

### 2. Hacer acción en el navegador

En este ejemplo estamos [navigating]({{< ref "/documentation/webdriver/interactions/navigation.md" >}}) a una página web.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L14" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L6" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L13" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L5" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L9" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L18" >}}
{{< /tab >}}
{{< /tabpane >}}

### 3. Solicitar información del navegador

Hay un montón de tipos de [información sobre el navegador]({{< ref "/documentation/webdriver/interactions" >}}) que puedes solicitar
. incluyendo los manejadores de ventanas, tamaño / posición del navegador, cookies, alertas, etc.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#16" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L8" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L15" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L7" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L11" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L20" >}}
{{< /tab >}}
{{< /tabpane >}}

### 4. Establecir estrategia de espera

Sincronizar el código con el estado actual del navegador es uno de los desafíos más grandes
con Selenium, y hacerlo bien es un tema avanzado.

Esencialmente quieres asegurarte de que el elemento está en la página antes de intentar ubicarlo
y que el elemento está en un estado interactable antes de intentar interactuar con él.

An implicit wait is rarely the best solution, but it's the easiest to demonstrate here, so
we'll use it as a placeholder.

Lee más sobre [Esperando estrategias]({{< ref "/documentation/webdriver/waits.md" >}}).

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L18" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L10" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L17" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L9" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L14" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L23" >}}
{{< /tab >}}
{{< /tabpane >}}

### 5. Buscar un elemento

La mayoría de los comandos en la mayoría de las sesiones de Selenium están relacionados con el elemento, y no puedes interactuar
con uno sin primero [encontrar un elemento]({{< ref "/documentation/webdriver/elements" >}})

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L20-L21" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L12-L13" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L19-L20" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L11-L12" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L16-L17" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L25-L26" >}}
{{< /tab >}}
{{< /tabpane >}}

### 6. Hacer acción en el elemento

Solo hay un puñado de [acciones para llevar a cabo un elemento]({{< ref "/documentation/webdriver/elements/interactions.md" >}}),
pero las usarás con frecuencia.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L23-L24" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L15-L16" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L22-L23" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L14-L15" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L19-L20" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L28-L29" >}}
{{< /tab >}}
{{< /tabpane >}}

### 7. Solicitar información del elemento

Los elementos almacenan mucha [información que puede ser solicitada]({{< ref "/documentation/webdriver/elements/information" >}}).

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L26-27" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L18-19" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L25-26" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L17-18" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L22-23" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L31-32" >}}
{{< /tab >}}
{{< /tabpane >}}

### 8. Terminar la sesión

Esto termina el proceso del controlador, que por defecto también cierra el navegador.
No se pueden enviar más comandos a esta instancia del controlador.
Ver [Sesiones de Salida]({{< ref "../drivers/#quitting-sessions" >}}).

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/FirstScript.java#L29" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/first_script.py#L21" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/FirstScript.cs#L28" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/first_script.rb#L20" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/firstScript.spec.js#L28" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/getting_started/FirstScriptTest.kt#L35" >}}
{{< /tab >}}
{{< /tabpane >}}

## Ejecutando archivo de Selenium

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/README.md#L60" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/README.md#L35" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/README.md#L36" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/README.md#L36" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Siguiente paso

La mayoría de los usuarios de Selenium ejecutan muchas sesiones y necesitan organizarlas para minimizar la duplicación y mantener el código
más mantenible. Lee para aprender cómo poner este código en contexto para tu caso de uso con
[Usando Selenium]({{< ref "using_selenium.md" >}}).
