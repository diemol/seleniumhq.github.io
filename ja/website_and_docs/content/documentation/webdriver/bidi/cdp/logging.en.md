---
title: Chrome DevTools Logging Features
linkTitle: Logging
weight: 2
description: |
  Logging features using CDP.
---

{{% pageinfo color="warning" %}}
While Selenium 4 provides direct access to the Chrome DevTools Protocol, these
methods will eventually be removed when WebDriver BiDi implemented.
{{% /pageinfo %}}

## Console Logs

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/LoggingTest.java#L31" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_logs.py#L11-12" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/LoggingTest.cs#L19-L25" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/logging_spec.rb#L12" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## JavaScript Exceptions

{{< tabpane text=true >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_logs.py#L22-L23" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/LoggingTest.cs#L41-L47" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/logging_spec.rb#L26" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}
