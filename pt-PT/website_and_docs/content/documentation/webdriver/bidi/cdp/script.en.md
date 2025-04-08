---
title: Chrome DevTools Script Features
linkTitle: Script
weight: 6
description: |
  Script features using CDP.
---

{{% pageinfo color="warning" %}}
While Selenium 4 provides direct access to the Chrome DevTools Protocol, these
methods will eventually be removed when WebDriver BiDi implemented.
{{% /pageinfo %}}

## Script Pinning

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/ScriptTest.java#L32-L34" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/ScriptTest.cs#L21-L22" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/script_spec.rb#L12-L13" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## DOM Mutation Handlers

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L44" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_script.py#L10-L11" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/ScriptTest.cs#L39-L46" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/script_spec.rb#L22" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}
