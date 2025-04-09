---
title: Características de registro BiDi WebDriver
linkTitle: Loggando
weight: 1
description: |
  Estas características están relacionadas con el registro. Debido a que "logging" puede referirse a tantas cosas diferentes, estos métodos están disponibles a través de un namespace "script".
aliases:
  - /documentation/es/webdriver/bidirectional/bidirectional_w3c/log
  - /documentation/webdriver/bidirectional/webdriver_bidi/log
---

Recuerde que para usar WebDriver BiDi, debe activarlo en Opciones.
Para más detalles, visita [Activando BiDi]({{< ref "BiDi" >}})

## Manejadores de mensajes de consola

Grabar o tomar acciones en eventos `console.log`.

### Añadir Manejador

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/test_bidi_logging.py#L11" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/logging_spec.rb#L11" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< /tabpane >}}

### Remover Manejador

Necesita almacenar el ID devuelto al agregar el manejador para eliminarlo.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/test_bidi_logging.py#L23-24" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/logging_spec.rb#L22-L23" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< /tabpane >}}

## Manejadores de Excepciones JavaScript

Grabar o tomar acciones en eventos de excepción JavaScript.

### Añadir Manejador

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/test_bidi_logging.py#L35" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/logging_spec.rb#L33" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< /tabpane >}}

### Remover Manejador

Necesita almacenar el ID devuelto al agregar el manejador para eliminarlo.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/test_bidi_logging.py#L47-48" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/logging_spec.rb#L44-L45" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< /tabpane >}}
