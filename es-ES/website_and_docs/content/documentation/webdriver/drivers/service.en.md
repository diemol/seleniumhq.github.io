---
title: Clase de Servicio de Conductor
linkTitle: Servicio
weight: 3
---

Las clases de servicio son para gestionar el inicio y la parada de los conductores locales.
No se pueden utilizar con una sesión de WebDriver remota.

Las clases de servicio le permiten especificar información sobre el controlador,
como ubicación y qué puerto utilizar.
También te permiten especificar qué argumentos pasan
a la línea de comandos. La mayoría de los argumentos útiles están relacionados con el registro.

## Instancia de servicio predeterminada

Para iniciar un controlador con una instancia de servicio predeterminada:

{{< tabpane text=verdad >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/drivers/ServiceTest.java#L15-L16" >}}
{{< badge-version version="4.11" >}}
{{< gh-codeblock path="ejemplos/python/tests/drivers/test_service.py#L5-L6" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Drivers/ServiceTest.cs#L14-L15" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/drivers/service_spec.rb#L14-L15" >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Ubicación del conductor

**Nota:** Si estás usando Selenium 4.6 o superior, no deberías tener que establecer una ubicación del controlador.
Si no puede actualizar Selenium o tiene un caso de uso avanzado, aquí está cómo especificar la ubicación del controlador:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/drivers/ServiceTest.java#L25-L26" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< badge-version version="4.11" >}}
{{< gh-codeblock path="ejemplos/python/tests/drivers/test_service.py#L15" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-version version="4.9" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Drivers/ServiceTest.cs#L23" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/drivers/service_spec.rb#L22" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Puerto conductor

Si desea que el controlador se ejecute en un puerto específico, puede especificarlo de la siguiente manera:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/drivers/ServiceTest.java#L33" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< badge-version version="4.11" >}}
{{< gh-codeblock path="ejemplos/python/tests/drivers/test_service.py#L23" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Drivers/ServiceTest.cs#L32" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/drivers/service_spec.rb#L29" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

<span id="setting-log-output"></span>

## Loggando

La funcionalidad de registro varía entre los navegadores. La mayoría de los navegadores le permiten especificar
ubicación y nivel de registros. Eche un vistazo a la página respectiva del navegador:

- [Chrome]({{< ref "../browsers/chrome#service" >}})
- [Edge]({{< ref "../browsers/edge#service" >}})
- [Firefox]({{< ref "../browsers/firefox#service" >}})
- [Internet Explorer]({{< ref "../browsers/internet_explorer#service" >}})
- [Safari]({{< ref "../browsers/safari#service" >}})
