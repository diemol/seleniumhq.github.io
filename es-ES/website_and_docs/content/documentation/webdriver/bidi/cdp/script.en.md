---
title: Características del script de Chrome DevTools
linkTitle: Escribir
weight: 6
description: |
  Características del script usando CDP.
---

{{% pageinfo color="warning" %}}
Mientras Selenium 4 proporciona acceso directo al Protocolo de Chrome DevTools, estos métodos
serán eliminados eventualmente cuando WebDriver BiDi implementado.
{{% /pageinfo %}}

## Fijar script

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/ScriptTest.java#L32-L34" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/ScriptTest.cs#L21-L22" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/script_spec.rb#L12-L13" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## DOM Mutation Handlers

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L44" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_script.py#L10-L11" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/ScriptTest.cs#L39-L46" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/script_spec.rb#L22" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}
