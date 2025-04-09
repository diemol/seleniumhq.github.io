---
title: Características de la red de Chrome DevTools
linkTitle: Red
weight: 4
description: |
  Características de red usando CDP.
---

{{% pageinfo color="warning" %}}
Mientras Selenium 4 proporciona acceso directo al Protocolo de Chrome DevTools, estos métodos
serán eliminados eventualmente cuando WebDriver BiDi implementado.
{{% /pageinfo %}}

## Autenticación básica

Algunas aplicaciones hacen uso de la autenticación del navegador para asegurar las páginas.
Solía ser común manejarlos en la URL, pero los navegadores dejaron de soportar esto.
Con este código puede insertar las credenciales en el encabezado cuando sea necesario

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L41-L43" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_network.py#L13-15" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L25-L32" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L9-L11" >}}
{{< badge-implementation >}}
{{< badge-implementation >}}
{{< /tabpane >}}

## Intercepción de red

Ambas solicitudes y respuestas pueden registrarse o transformarse.

#### Información de respuesta

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L56-L65" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L46-L51" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L20-L24" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

#### Responder transformación

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L75-L85" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L62-L73" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L31-L35" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

#### Solicitud de intercepción

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L97-L110" >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L85-L97" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L42-L46" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Métricas de rendimiento

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L125-L126" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_network.py#L26-L28" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L114-L118" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L56-L57" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Configurando Cookies

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L142-L157" >}}
{{< gh-codeblock path="/examples/python/tests/bidi/cdp/test_network.py#L37-L44" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/BiDi/CDP/NetworkTest.cs#L136-L143" >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L68-L71" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}

## Esperando por descargas

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/bidi/cdp/NetworkTest.java#L171-L176" >}}
{{< badge-implementation >}}
{{< badge-implementation >}}
{{< gh-codeblock path="/examples/ruby/spec/bidi/cdp/network_spec.rb#L82-L88" >}}
{{< badge-implementation >}}
{{< badge-code >}}
{{< /tabpane >}}
