---
title: Logo
linkTitle: Logo
weight: 1
aliases:
  - /documentation/es/webdriver/bidirectional/bidirectional_w3c/log
---

Esta sección contiene las APIs relacionadas con el registro.

## Registros de consola

Escucha los eventos de `console.log` y registra los callbacks para procesar el evento.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/LogTest.java#L33-L39" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/logInspector.spec.js#L23-37" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Excepciones JavaScript

Escucha las Excepciones JS
y registra las devoluciones de llamada para procesar los detalles de la excepción.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/LogTest.java#L73-L78" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/logInspector.spec.js#L44-54" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Escuchar registros JS

Escuche todos los registros JS en todos los niveles y registre las llamadas para procesar el registro.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/LogTest.java#L55-L60" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}