---
title: Organizar y ejecutar código de Selenium
linkTitle: Usando Selenium
weight: 10
description: |
  Escalando la ejecución de Selenium con un IDE y una biblioteca de ejecutores de pruebas
---

{{< alert-content >}}
{{< /alert-content >}}

Si quieres ejecutar más de un puñado de scripts únicos, necesitas
ser capaz de organizar y trabajar con tu código. Esta página debería darte
ideas sobre cómo hacer realmente cosas productivas con tu código de Selenium.

## Usos comunes

La mayoría de la gente usa Selenium para ejecutar pruebas automatizadas para aplicaciones web,
pero Selenium soporta cualquier caso de uso de automatización del navegador.

### Tareas repetitivas

Tal vez necesite iniciar sesión en un sitio web y descargar algo, o enviar un formulario.
Puede crear un script de Selenium para ejecutarse con un servicio en tiempos predefinidos.

### Raspado web

¿Está buscando recopilar datos de un sitio que no tiene una API? Selenium
te permitirá hacer esto, pero asegúrese de que está familiarizado con los términos
del sitio web ya que algunos sitios web no lo permiten y otros incluso bloquearán Selenium.

### Pruebas

Ejecutar Selenium para realizar pruebas requiere hacer afirmaciones sobre las acciones tomadas por Selenium.
Por lo tanto, se requiere una buena biblioteca de afirmaciones. Funciones adicionales para proporcionar estructura para las pruebas
requieren el uso de [Ejecutador de prueba](#test-runner).

## IDEs

Independientemente de cómo utilices el código de Selenium,
no serás muy eficaz escribirlo o ejecutarlo sin un buen Entorno de Desarrollador Integrado
. Aquí hay algunas opciones comunes...

- [Eclipse](https://www.eclipse.org/)
- [IntelliJ IDEA](https://www.jetbrains.com/idea/)
- [PyCharm](https://www.jetbrains.com/pycharm/)
- [RubyMine](https://www.jetbrains.com/ruby/)
- [Rider](https://www.jetbrains.com/rider/)
- [WebStorm](https://www.jetbrains.com/webstorm/)
- [Código VS](https://code.visualstudio.com/)

## Ejecutar prueba

Incluso si no estás usando Selenium para pruebas, si tienes casos de uso avanzados, podría tener sentido
usar un corredor de pruebas para organizar mejor su código. Ser capaz de usar antes/después de los ganchos
y ejecutar cosas en grupos o en paralelo puede ser muy útil.

### Eligiendo

Hay muchos corredores de prueba diferentes disponibles.

Todos los ejemplos de código de esta documentación se pueden encontrar (o se está moviendo a) nuestros directoriosformat@@0 de ejemplo
que utilizan corredores de prueba y se ejecutan cada versión para asegurarse de que todo el código es correcto y actualizado.
Aquí hay una lista de corredores de prueba con enlaces. El primer elemento es el que utiliza este repositorio y el
que se utilizará para todos los ejemplos de esta página.

{{< tabpane text=verdad >}}

- [JUnit](https://junit.org/junit5/) - Un marco de pruebas ampliamente utilizado para las pruebas Selenium basadas en Java.
- [TestNG](https://testng.org/) - Ofrece características extra como ejecución de pruebas paralelas y pruebas parameterizadas.
  {{% /tab %}}

{{% tab header="Python" %}}

- [pytest](https://pytest.org/) - Una elección preferida para muchos, gracias a su simplicidad y poderosos plugins.
- [unittest](https://docs.python.org/3/library/unittest.html) - framework de prueba de librerías estándar de Python.
  {{% /tab %}}

{{% tab header="CSharp" %}}

- [NUnit](https://nunit.org/) - Un marco de prueba de unidad popular para .NET.
- [MS Test](https://docs.microsoft.com/en-us/visualstudio/test/getting-started-with-unit-testing?view=vs-2019) - Marco de pruebas unitarias propio de Microsoft.
  {{% /tab %}}

{{% tab header="Ruby" %}}

- [RSpec](https://rspec.info/) - La biblioteca de pruebas más utilizada para ejecutar las pruebas de Selenium en Ruby.
- [Minitest](https://github.com/seattlerb/minitest) - Un marco de prueba ligero que viene con la biblioteca estándar de Ruby.
  {{% /tab %}}

{{% tab header="JavaScript" %}}

- [Jest](https://jestjs.io/) - Principalmente conocido como un marco de pruebas para React, también puede ser utilizado para pruebas de Selenium.
- [Mocha](https://mochajs.org/) - La biblioteca JS más común para ejecutar las pruebas de Selenium.
  {{% /tab %}}

{{% tab header="Kotlin" %}}

- [Kotest](https://kotest.io/) - Un marco de pruebas flexible y completo diseñado específicamente para Kotlin.
- [JUnit5](https://junit.org/junit5/) - El framework de pruebas estándar de Java, totalmente compatible con Kotlin.
  {{% /tab %}}

{{< /tabpane >}}

### Instalando

Esto es muy similar a lo que se necesitaba en [Instalar una biblioteca Selenium]({{< ref "install_library.md" >}}).
Este código sólo muestra ejemplos de lo que está siendo utilizado en nuestro proyecto de Ejemplos de Documentación.

{{< tabpane text=verdad >}}

**Maven**

**Gradle**

{{% /tab %}}
{{% tab header="Python" %}}

Para usarlo en un proyecto, añádelo al archivo `requirements.txt`:

{{% /tab %}}
{{% tab header="CSharp" %}}
en el archivo `csproj` del proyecto, especifica la dependencia como `PackageReference` en `ItemGroup`:

{{% /tab %}}
{{% tab header="Ruby" %}}

Añadir a gemfile del proyecto

{{% /tab %}}
{{% tab header="JavaScript" %}}
En el `package.json` de tu proyecto, añade el requisito a `dependencies`:

{{< tab header="Kotlin" >}}
{{< /tab >}}
{{< /tabpane >}}

### Validando

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/UsingSeleniumTest.java#L30-L31" >}}
{{< /tab >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/using_selenium_tests.py#L8-L9" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/GettingStarted/UsingSeleniumTest.cs#L19-L20" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/using_selenium_spec.rb#L14-L15" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/runningTests.spec.js#L14-L15" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Configuración de arriba y Tearing Down

{{< tabpane text=verdad >}}

### Configurar

{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/getting_started/UsingSeleniumTest.java#L19-L22" >}}

### Tear abajo

{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/UsingSeleniumTest.java#L45-L48" >}}

{{% /tab %}}
{{% tab header="Python" %}}

### Configurar

{{< gh-codeblock path="ejemplos/python/tests/getting_started/using_selenium_tests.py#L25-L28" >}}

### Tear abajo

{{< gh-codeblock path="ejemplos/python/tests/getting_started/using_selenium_tests.py#L30-31" >}}

{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}

### Configurar

{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/using_selenium_spec.rb#L7-L9" >}}

### Tear abajo

{{< gh-codeblock path="ejemplos/ruby/spec/spec_helper.rb#L30" >}}
{{< tab header="JavaScript" >}}

### Configurar

{{< gh-codeblock path="ejemplos/javascript/test/getting_started/runningTests.spec.js#L7-L9" >}}

### Tear abajo

{{< gh-codeblock path="ejemplos/javascript/test/getting_started/runningTests.spec.js#L30" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Ejecutando

{{< tabpane text=verdad >}}

### Maven

```shell
prueba de limpieza mvn
```

### Gradle

```shell
prueba de limpieza de grados
```

{{< gh-codeblock path="ejemplos/python/README.md#L35" >}}
{{< tab header="Carrete" >}}
{{< badge-code >}}
{{< /tab >}}
{{< gh-codeblock path="ejemplos/ruby/README.md#L26" >}}

### Mocha

```shell
mocha runningTests.spec.js
```

### npx

```shell
mocha npx runningTests.spec.js
```

{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

### Ejemplos

En [Primer script]({{< ref "first_script.md" >}}), vimos cada uno de los componentes de un script de Selenium.
Aquí hay un ejemplo de ese código usando un corredor de pruebas:

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/getting_started/UsingSeleniumTest.java" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/getting_started/using_selenium_tests.py" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="examples/dotnet/SeleniumDocs/GettingStarted/UsingSeleniumTest.cs" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/getting_started/using_selenium_spec.rb" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/getting_started/runningTests.spec.js" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}

## Siguiente paso

¡Toma lo que has aprendido y construye tu código de Selenium!

As you find more functionality that you need, read up on the rest of our
[WebDriver documentation]({{< ref "/documentation/webdriver/" >}}).
