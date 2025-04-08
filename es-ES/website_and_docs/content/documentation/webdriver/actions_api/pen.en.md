---
title: Acciones Pen
linkTitle: Pen
weight: 5
description: |
  Una representación de un lápiz de entrada de puntero para interactuar con una página web.
---

{{< badge-browser browser=Cromo wpt="perform_actions/pointer.py" >}}

Un Pen es un tipo de entrada de puntero que tiene más del mismo comportamiento que un ratón, pero puede
también tener propiedades de eventos únicas para un estilo. Además, mientras que un ratón
tiene 5 botones, un lápiz tiene 3 estados equivalentes:

- 0 — Toque Contacto (el valor por defecto; equivalente a un clic izquierdo)
- 2 — Botón de cañón (equivalente a un clic derecho)
- 5 — Botón de borrador (actualmente no soportado por los controladores)

## Usando un Pen

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< badge-version version="4.2" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/actions_api/PenTest.java#L26-L33" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< badge-version version="4.2" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_pen.py#L12-L20" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/PenTest.cs#L19-L28" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.2" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/pen_spec.rb#L11-L17" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/PenTest.kt#L23-L30" >}}
{{< /tab >}}
{{< /tabpane >}}

## Agregar atributos de evento del puntero

{{< badge-version version="4.2" >}}

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/actions_api/PenTest.java#L67-L81" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_pen.py#L53-L61" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/PenTest.cs#L64-L77" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/pen_spec.rb#L50-L56" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/PenTest.kt#L64-L78" >}}
{{< /tab >}}
{{< /tabpane >}}

