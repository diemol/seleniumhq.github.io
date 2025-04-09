---
title: Chrome DevTools Network Features
linkTitle: Network
weight: 4
description: |
  Network features using CDP.
---

{{% pageinfo color="warning" %}}
While Selenium 4 provides direct access to the Chrome DevTools Protocol, these
methods will eventually be removed when WebDriver BiDi implemented.
{{% /pageinfo %}}

## Basic authentication

Some applications make use of browser authentication to secure pages.
It used to be common to handle them in the URL, but browsers stopped supporting this.
With this code you can insert the credentials into the header when necessary

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L41-L43" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_network.py#L13-15" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L25-L32" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L9-L11" >}}
{{< badge-implementation >}}
{{< badge-implementation >}}
{{< /tabpane >}}

## Network Interception

Both requests and responses can be recorded or transformed.

#### Response information

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L56-L65" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L46-L51" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L20-L24" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

#### Response transformation

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L75-L85" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L62-L73" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L31-L35" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

#### Request interception

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L97-L110" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L85-L97" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L42-L46" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Performance Metrics

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L125-L126" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_network.py#L26-L28" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L114-L118" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L56-L57" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Setting Cookies

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L142-L157" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_network.py#L37-L44" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L136-L143" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L68-L71" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Waiting for Downloads

{{< tabpane text=true >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L171-L176" >}}
{{< badge-implementation >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L82-L88" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}
