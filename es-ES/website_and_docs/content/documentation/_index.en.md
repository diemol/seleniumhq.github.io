---
title: El proyecto de automatización del navegador Selenium
linkTitle: Documentación
cascade:
  - type: documentos
aliases:
  - /es/documentation/es/
---

Selenium es un proyecto paraguas para una gama de herramientas y bibliotecas
que permiten y apoyan la automatización de navegadores web.

Provee extensiones para emular la interacción del usuario con los navegadores,
un servidor de distribución para la asignación de escala del navegador,
y la infraestructura para implementaciones de la
[W3C WebDriver specification](//www.w3.org/TR/webdriver/)
que le permite escribir código intercambiable para todos los principales navegadores web.

Este proyecto es posible gracias a los colaboradores voluntarios
que han puesto miles de horas de su propio tiempo,
y hizo que el código fuente
[disponible libremente]({{< ref "copyright. d#license" >}})
para cualquiera a usar, disfrutar y mejorar.

Selenium reúne a proveedores de navegadores, ingenieros y entusiastas
para promover una discusión abierta acerca de la automatización de la plataforma web.
El proyecto organiza [una conferencia anual](//seleniumconf.com/)
para enseñar y nutrir a la comunidad.

At the core of Selenium is [WebDriver]({{< ref "webdriver" >}}),
an interface to write instruction sets that can be run interchangeably in many
browsers. Once you've installed everything, only a few lines of code get you inside
a browser. Puedes encontrar un ejemplo más completo en [Escribir tu primer script de Selenio]({{< ref "first_script.md" >}})

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="/examples/java/src/test/java/dev/selenium/hello/HelloSelenium.java" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="/examples/python/tests/hello/hello_selenium.py" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="/examples/dotnet/HelloSelenium.cs" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="/examples/ruby/spec/hola/hola/hola_selenium.rb" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="/examples/javascript/test/hello/helloSelenium.js" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="/examples/kotlin/src/test/kotlin/dev/selenium/hello/HelloSelenium.kt" >}}
{{< /tab >}}
{{< /tabpane >}}

Mira la [Overview]({{< ref "overview" >}}) para comprobar los diferentes componentes
del proyecto y decidir si Selenium es la herramienta adecuada para ti.

Deberías continuar con [Empezando]({{< ref "webdriver/getting_started" >}})
para entender cómo puedes instalar Selenium y usarlo con éxito como una herramienta de automatización
, y pruebas simples escalables como esta para ejecutarse en entornos grandes distribuidos
en múltiples navegadores, en varios sistemas operativos diferentes.
