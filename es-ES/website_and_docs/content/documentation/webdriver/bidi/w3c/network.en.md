---
title: Red
linkTitle: Red
weight: 1
aliases:
  - /documentation/es/webdriver/bidirectional/bidirectional_w3c/network
---

## Comandos

Esta sección contiene las APIs relacionadas con los comandos de red.

### Añadir interceptación de red

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkCommandsTest.java#L36-L38" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_commands.spec.js#L29" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Eliminar interceptación de red

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkCommandsTest.java#L46-L50" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_commands.spec.js#L34-L35" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Continuar la solicitud bloqueada en la fase requerida con credenciales

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkCommandsTest.java#L57-L64" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_commands.spec.js#L42-L46" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Continuar la solicitud bloqueada en la fase requerida sin credenciales

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkCommandsTest.java#L74-L80" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_commands.spec.js#L56-L60" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Cancelar solicitud bloqueada en fase obligatoria

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkCommandsTest.java#L90-L96" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_commands.spec.js#L71-L75" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Solicitud de fallo

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkCommandsTest.java#L104-L108" >}}
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

## Eventos

Esta sección contiene las APIs relacionadas con eventos de red.

### Antes de la solicitud enviada

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkEventsTest.java#L30-L35" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_events.spec.js#L23-L29" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Respuesta iniciada

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkEventsTest.java#L45-L51" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_events.spec.js#L83-L89" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Respuesta completada

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkEventsTest.java#L62-L68" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/network_events.spec.js#L97-L103" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Aut requerido

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.17" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/NetworkEventsTest.java#L101-L106" >}}
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


