---
title: Navegando Contexto
linkTitle: Navegando Contexto
weight: 1
aliases:
  - /documentation/es/webdriver/bidirectional/bidirectional_w3c/browsing_context
---

## Comandos

Esta sección contiene las APIs relacionadas con comandos contextuales de navegación.

### Abrir una nueva ventana

Crea un nuevo contexto de navegación en una nueva ventana.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L44-L47" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L33-L35" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Abrir una nueva pestaña

Crea un nuevo contexto de navegación en una nueva pestaña.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L58-L61" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L48-L50" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Usar el identificador de ventana existente

Crea un contexto de navegación para que la pestaña/ventana existente ejecute comandos.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L37-L41" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L25-L28" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Abrir una ventana con un contexto de navegación de referencia

Un contexto de navegación de referencia es un [contexto de navegación de nivel superior](https://html.spec.whatwg.org/multipage/document-sequences.html#top-level-browsing-context).
La API permite pasar el contexto de navegación de referencias, que se utiliza para crear una nueva ventana. La implementación es específica del sistema operativo.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L50-L55" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L40-L43" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Abrir una pestaña con un contexto de navegación de referencia

Un contexto de navegación de referencia es un [contexto de navegación de nivel superior](https://html.spec.whatwg.org/multipage/document-sequences.html#top-level-browsing-context).
La API permite pasar el contexto de navegación de referencias, que se utiliza para crear una nueva pestaña. La implementación es específica del sistema operativo.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L64-L69" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L55-L58" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Navegar a una URL

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L72-L80" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L67" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Navegar a una URL con estado de preparación

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L83-L92" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L79-L82" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Obtener árbol de contexto de navegación

Proporciona un árbol de todos los contextos de navegación que descienden del contexto de navegación padre, incluyendo el contexto de navegación padre.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L95-L108" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L90-L96" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Obtener el árbol de contexto de navegación con profundidad

Proporciona un árbol de todos los contextos de navegación que descienden del contexto de navegación padre, incluyendo el contexto de navegación padre hasta el valor de profundidad pasado.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L111-L123" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L103-L109" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Obtener todos los contextos de navegación de nivel superior

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L126-L133" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.20.0" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L426-L431" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Cerrar una pestaña/ventana

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L136-L153" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L115-L118" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Activar un contexto de navegación

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.14.1" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L157-L161" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L192-L194" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L204" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Recargar un contexto de navegación

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.13.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L169-L173" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L351" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Preguntar usuario

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.13.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L220-L228" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L301" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Captura de pantalla

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.13.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L248-L252" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L362" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Captura de pantalla de visualización

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.14.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L259-L268" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L165-L169" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Captura de pantalla de Elemento

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.14.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L275-L280" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L184" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Configurar vista

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.14.1" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L304-L307" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L335" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Print page

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.14.1" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L317-L322" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L145-L157" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Navegar atrás

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.16.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L330-L336" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.17" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L396" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Avanzar hacia adelante

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.16.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L342-L352" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.17" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L420" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Historial de recorrido

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.16.0" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextTest.java#L359-L365" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.17" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContext.spec.js#L378" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Eventos

Esta sección contiene las APIs relacionadas con la navegación de eventos de contexto.

### Evento creado por el contexto de navegación

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L34-L41" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.9.2" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContextInspector.spec.js#L23-L28" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Evento cargado de contenido de Dom

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L54-L63" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.9.2" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContextInspector.spec.js#L53-L62" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Evento Cargado Contexto de Navegación

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L81-88" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.9.2" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContextInspector.spec.js#L70-L78" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Evento Navegado Iniciado

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L97-104" >}}
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

### Evento Navegado por Fragmento

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L113-123" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.15.0" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContextInspector.spec.js#L86-L97" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Evento Abierto del Usuario

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L113-123" >}}
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

### Evento cerrado de comprobación de usuario

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.15" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L150-163" >}}
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

### Evento de exploración del contexto destruido

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.18" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidirectional/webdriver_bidi/BrowsingContextInspectorTest.java#L170-L181" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-version version="4.18.0" >}}
{{< gh-codeblock path="/examples/javascript/test/bidirectional/browsingContextInspector.spec.js#L105-L113" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}
