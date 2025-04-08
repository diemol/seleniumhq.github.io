---
title: Funcionalidad específica del borde
linkTitle: Borde
weight: 5
description: Estas son funciones y características específicas de los navegadores Microsoft Edge.
---

Microsoft Edge se implementa con Chromium, con la primera versión compatible de v79. Similar a Chrome,
el número de versión principal de edgedriver debe coincidir con la versión principal del navegador Edge.

## Opciones

Las capacidades comunes a todos los navegadores se describen en la [página de opciones]({{< ref "../drivers/options.md" >}}).

Las capacidades únicas de Chromium están documentadas en la página de Google para
[Capacidades y opciones de cromo](https://chromedriver.chromium.org/capabilities)

Iniciar una sesión Edge con opciones básicas definidas se ve así:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L38-L39" >}}
{{< /tab >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L9-L10" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Browsers/EdgeTest.cs#L30-L31" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L10-L11" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/getting_started/openEdgeTest.spec.js#L11-L15" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Argumentos

El parámetro `args` es para una lista de interruptores de línea de comandos que se usarán al iniciar el navegador.
Hay dos recursos excelentes para investigar estos argumentos:

- [Banderas Chrome para Herramientas](https://github.com/GoogleChrome/chrome-launcher/blob/main/docs/chrome-flags-for-tools.md)
- [Lista de Cambios de Línea de Comando de Chromium](https://peter.sh/experiments/chromium-command-line-switches/)

Comúnmente usados los argumentos incluyen `--start-maximized`, `--headless=new` y `--user-data-dir=...`

Añadir un argumento a las opciones:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L46" >}}
{{< /tab >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L18" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Navegadores/EdgeTest.cs#L39" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L17" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/browser/edgeSpecificCaps.spec.js#L12" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Iniciar navegador en una ubicación especificada

El parámetro `binary` toma la ruta de una ubicación alternativa del navegador a utilizar. With this parameter you can
use chromedriver to drive various Chromium based browsers.

Añadir una ubicación del navegador a las opciones:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L55" >}}
{{< /tab >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L29" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Browsers/EdgeTest.cs#L49" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L25" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Añadir extensiones

El parámetro `extensions` acepta archivos crx. En cuanto a los directorios desempaquetados,
utilice el argumento `load-extension`, como se menciona en
[esta publicación](https://chromedriver.chromium.org/extensions).

Añadir una extensión a las opciones:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L66" >}}
{{< /tab >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L40" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Browsers/EdgeTest.cs#L61" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L34" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/browser/edgeSpecificCaps.spec.js#L55" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Mantener el navegador abierto

Establecer el parámetro 'detach' a verdadero mantendrá el navegador abierto una vez que el proceso haya terminado,
siempre y cuando el comando de salir no sea enviado al controlador.

{{< tabpane text=verdad >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L51" >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L45" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/browser/edgeSpecificCaps.spec.js#L32" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Excluyendo argumentos

MSEdgedriver tiene varios argumentos por defecto que usa para iniciar el navegador.
Si no quieres que se añadan estos argumentos, pasarlos a `excludeSwitches`.
Un ejemplo común es volver a activar el bloqueador de ventanas emergentes. Una lista completa de los argumentos predeterminados
puede ser analizada desde el
[Chromium Source Code](https://source.chromium.org/chromium/chromium/src/+/main:chrome/test/chromedriver/chrome_launcher.cc)

Establecer argumentos excluidos en las opciones:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L79" >}}
{{< /tab >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L62" >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="/examples/dotnet/SeleniumDocs/Browsers/EdgeTest.cs#L76" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L53" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/browser/edgeSpecificCaps.spec.js#L22" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Servicio

Ejemplos para crear un objeto de servicio predeterminado, y para configurar la ubicación del controlador y el puerto
se pueden encontrar en el [Servicio de Motivador]({{< ref ". /drivers/service.md" >}}) página.

### Log de salida

Obtener registros de controladores puede ser útil para depurar problemas. La clase de servicio le permite
directo hacia dónde irán los registros. La salida de registro se ignora a menos que el usuario la dirija a alguna parte.

#### Salida de archivo

Para cambiar la salida de registro para guardar en un archivo específico:

{{< tabpane text=verdad >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L101" >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/browsers/test_edge.py#L71" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Browsers/EdgeTest.cs#L86" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/browsers/edge_spec.rb#L67" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

#### Salida de consola

Para cambiar la salida de registro a mostrar en la consola como STDOUT:

{{< tabpane text=verdad >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L114" >}}
{{< tab header="Python" >}}
{{< badge-version version="4.11" >}}
{{< gh-codeblock path="ejemplos/python/tests/browsers/test_edge.py#L82" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/browsers/edge_spec.rb#L76" >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Nivel de log

Hay 6 niveles de registro disponibles: `ALL`, `DEBUG`, `INFO`, `WARNING`, `SEVERE`, y `OFF`.
Ten en cuenta que `--verbose` es equivalente a `--log-level=ALL` y `--silent` es equivalente a `--log-level=OFF`,
así que este ejemplo solo establece el nivel de registro generalmente:

{{< tabpane text=verdad >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L127-L128" >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/browsers/test_edge.py#L93" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.10" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/browsers/edge_spec.rb#L87" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Características del archivo de registro

Hay 2 características que sólo están disponibles cuando se registra en un archivo:

- añadir registro
- marcas de tiempo legibles

Para usarlos, también necesita especificar explícitamente la ruta de registro y el nivel de registro.
La salida del registro será administrada por el controlador, no por el proceso, por lo que se pueden ver pequeñas diferencias.

{{< tabpane text=verdad >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L143-L144" >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="examples/python/tests/browsers/test_edge.py#L104" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-implementation >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="examples/ruby/spec/browsers/edge_spec.rb#L97-L98" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Disabling build check

Edge browser and msedgedriver versions should match, and if they don't the driver will error.
If you disable the build check, you can force the driver to be used with any version of Edge.
Note that this is an unsupported feature, and bugs will not be investigated.

{{< tabpane text=verdad >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L161-L162" >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="examples/python/tests/browsers/test_edge.py#L115" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="examples/dotnet/SeleniumDocs/Browsers/EdgeTest.cs#L155" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< badge-version version="4.8" >}}
{{< gh-codeblock path="examples/ruby/spec/browsers/edge_spec.rb#L108" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Internet Explorer Mode

Microsoft Edge can be driven in "Internet Explorer Compatibility Mode", which uses
the Internet Explorer Driver classes in conjunction with Microsoft Edge.
Read the [Internet Explorer page]({{< ref "internet_explorer.md" >}}) for more details.

## Special Features

Some browsers have implemented additional features that are unique to them.

### Casting

You can drive Chrome Cast devices with Edge, including sharing tabs

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L225-L230" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L170-L174" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L119-L123" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Network conditions

You can simulate various network conditions.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L198-L204" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L129-L135" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L129" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Logs

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L242" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L186" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L141" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Permisos

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/browsers/EdgeTest.java#L184" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/browsers/test_edge.py#L149" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/browsers/edge_spec.rb#L149-L150" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### DevTools

Vea la sección [Chrome DevTools]({{< ref "../bidi/cdp/" >}}) para más información sobre cómo usar DevTools en Borde
