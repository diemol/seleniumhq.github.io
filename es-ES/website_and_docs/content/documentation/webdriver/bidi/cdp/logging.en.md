---
title: Características de registro de Chrome DevTools
linkTitle: Loggando
weight: 2
description: |
  Registrando características usando CDP.
---

{{% pageinfo color="warning" %}}
Mientras Selenium 4 proporciona acceso directo al Protocolo de Chrome DevTools, estos métodos
serán eliminados eventualmente cuando WebDriver BiDi implementado.
{{% /pageinfo %}}

## Registros de consola

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/LoggingTest.java#L31" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_logs.py#L11-12" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/LoggingTest.cs#L19-L25" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/logging_spec.rb#L12" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Excepciones JavaScript

{{< tabpane text=verdad >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_logs.py#L22-L23" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/LoggingTest.cs#L41-L47" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/logging_spec.rb#L26" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}
