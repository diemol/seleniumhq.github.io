---
title: Información sobre elementos web
linkTitle: Información
weight: 4
description: |
  Lo que puedes aprender sobre un elemento.
---

Hay una serie de detalles que puede consultar sobre un elemento específico.

## Se muestra

Este método se utiliza para comprobar si el elemento conectado es
mostrado en una página web. Devuelve un valor `Boolean`,
True si el elemento conectado se muestra en el contexto actual
de navegación devuelve falso.

Esta funcionalidad está [mencionada en](https://w3c.github.io/webdriver/#element-displayedness), pero no definido por
la especificación w3c debido a la
[imposibilidad de cubrir todas las condiciones potenciales](https://www.youtube.com/watch?v=LAD_XPGP_kk).
Como tal, Selenium no puede esperar que los controladores implementen
esta funcionalidad directamente, y ahora depende de
ejecutando directamente una función JavaScript grande.
Esta función hace muchas aproximaciones sobre la naturaleza y relación
de un elemento en el árbol para devolver un valor.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/elements/InformationTest.java#L20-L24" >}}
{{< /tab >}}
{{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="ejemplos/python/tests/elements/test_information.py#L12-L15" >}}
{{< /tab >}}
{{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Elements/InformationTest.cs#L18-L22" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L12" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L16-L17" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}

//devuelve true si el elemento se muestra devuelve falso
val flag = driver.findElement(By.name("email_input")).isDisplayed()

{{< /tab >}}
{{< /tabpane >}}

## Está habilitado

Este método se utiliza para comprobar si el elemento conectado
está habilitado o deshabilitado en una página web.
Devuelve un valor booleano, **True** si el elemento conectado es
**habilitado** en el contexto de navegación actual de lo contrario devuelve **false**.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/elements/InformationTest.java#L27-L29" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="ejemplos/python/tests/elements/test_information.py#L19" >}}
  {{< /tab >}}
 {{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Elements/InformationTest.cs#L25-L27" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L17" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L23-L24" >}}
{{< /tab >}}
  {{< tab header="Kotlin" >}}

  {{< /tab >}}
{{< /tabpane >}}

## Está seleccionado

Este método determina si el elemento referenciado
es _Seleccionado_ o no. Este método se utiliza ampliamente en
Cajas de verificación, botones de radio, elementos de entrada y elementos de opción.

Devuelve un valor booleano, **True** si el elemento referenciado es
**seleccionado** en el contexto de navegación actual, de lo contrario devuelve **false**.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/elements/InformationTest.java#L32-L34" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
  {{< gh-codeblock path="ejemplos/python/tests/elements/test_information.py#L23" >}}
  {{< /tab >}}
 {{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Elements/InformationTest.cs#L30-L32" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L22" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L30-L31" >}}
{{< /tab >}}
  {{< tab header="Kotlin" >}}

  {{< /tab >}}
{{< /tabpane >}}

## Tag Name

It is used to fetch the [TagName](https://www.w3.org/TR/webdriver/#dfn-get-element-tag-name)
of the referenced Element which has the focus in the current browsing context.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/elements/InformationTest.java#L37-L39" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="examples/python/tests/elements/test_information.py#L27" >}}
  {{< /tab >}}
     {{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="examples/dotnet/SeleniumDocs/Elements/InformationTest.cs#L35-L37" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L27" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L37-L38" >}}
{{< /tab >}}
  {{< tab header="Kotlin" >}}

  {{< /tab >}}
{{< /tabpane >}}

## Size and Position

It is used to fetch the dimensions and coordinates
of the referenced element.

The fetched data body contain the following details:

- X-axis position from the top-left corner of the element
- y-axis position from the top-left corner of the element
- Height of the element
- Width of the element

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/elements/InformationTest.java#L42-L44" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="examples/python/tests/elements/test_information.py#L31" >}}
  {{< /tab >}}
{{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="examples/dotnet/SeleniumDocs/Elements/InformationTest.cs#L40-L43" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L32" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L45" >}}
{{< /tab >}}
  {{< tab header="Kotlin" >}}

// Returns height, width, x and y coordinates referenced element
val res = driver.findElement(By.name("range_input")).rect

  {{< /tab >}}
{{< /tabpane >}}

## Get CSS Value

Retrieves the value of specified computed style property
of an element in the current browsing context.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/elements/InformationTest.java#L49-L50" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="examples/python/tests/elements/test_information.py#L35-L37" >}}
{{< /tab >}}
{{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="examples/dotnet/SeleniumDocs/Elements/InformationTest.cs#L49-L50" >}}
{{< /tab >}}
  {{< tab header="Ruby" text=verdad >}}
  {{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L38" >}}
  {{< /tab >}}
  {{< tab header="JavaScript" text=verdad >}}
  {{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L76-L78" >}}
  {{< /tab >}}
  {{< tab header="Kotlin" >}}

// Navigate to Url
driver.get("https://www.selenium.dev/selenium/web/colorPage.html")

// Retrieves the computed style property 'color' of linktext
val cssValue = driver.findElement(By.id("namedColor")).getCssValue("background-color")

  {{< /tab >}}
{{< /tabpane >}}

## Text Content

Devuelve el texto renderizado del elemento especificado.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/elements/InformationTest.java#L54-L56" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="ejemplos/python/tests/elements/test_information.py#L41" >}}
  {{< /tab >}}
{{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Elements/InformationTest.cs#L53-L55" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L43" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L84-L86" >}}
{{< /tab >}}
  {{< tab header="Kotlin" >}}

  {{< /tab >}}
{{< /tabpane >}}

## Obteniendo atributos o propiedades

Obtiene el valor de tiempo de ejecución asociado con un atributo
DOM. Devuelve los datos asociados
con el atributo DOM o la propiedad del elemento.

{{< tabpane langEqualsHeader=verdad >}}
{{< tab header="Java" text=verdad >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/elements/InformationTest.java#L60-L64" >}}
{{< /tab >}}
  {{< tab header="Python" text=verdad >}}
{{< gh-codeblock path="ejemplos/python/tests/elements/test_information.py#L44-L46" >}}
  {{< /tab >}}
{{< tab header="Carrete" text=verdad >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/Elements/InformationTest.cs#L58-L62" >}}
{{< /tab >}}
{{< tab header="Ruby" text=verdad >}}
{{< gh-codeblock path="/examples/ruby/spec/elements/information_spec.rb#L48" >}}
{{< /tab >}}
{{< tab header="JavaScript" text=verdad >}}
{{< gh-codeblock path="/examples/javascript/test/elements/information.spec.js#L55-L59" >}}
{{< /tab >}}
  {{< tab header="Kotlin" >}}

  {{< /tab >}}
{{< /tabpane >}}
