---
title: Acciones de rueda
linkTitle: Rueda
weight: 6
description: |
  Una representación de un dispositivo de entrada de rueda de desplazamiento para interactuar con una página web.
---

{{< badge-version version="4.2" >}}
{{< badge-browser browser=Cromo wpt="perform_actions/wheel.py" >}}

Hay 5 escenarios para desplazarse en una página.

## Desplazar hasta el elemento

Este es el escenario más común. A diferencia de los métodos tradicionales de hacer clic y enviar claves,
la clase de acciones no desplaza automáticamente el elemento objetivo en la vista,
así que este método tendrá que ser usado si los elementos no están ya dentro de la viewport.

Este método toma un elemento web como único argumento.

Independientemente de si el elemento está arriba o debajo de la pantalla de la vista actual,
la vista se desplazará para que la parte inferior del elemento esté en la parte inferior de la pantalla.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/actions_api/wheelTest.java#L17-L20" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_wheel.py#L11-L14" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/wheelTest.cs#L17-L20" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/wheel_spec.rb#L11-L14" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/actionsApi/wheelTest.spec.js#L16-L19" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/wheelTest.kt#L18-L21" >}}
{{< /tab >}}
{{< /tabpane >}}

## Desplazar por el monto dado

Este es el segundo escenario más común para el desplazamiento. Pase en un delta x y un valor delta y para cuánto desplazar
en la dirección derecha y hacia abajo. Los valores negativos representan a izquierda y arriba, respectivamente.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/actions_api/wheelTest.java#L29-L33" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_wheel.py#L22-L26" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/wheelTest.cs#L31-L35" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/wheel_spec.rb#L22-L26" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/actionsApi/wheelTest.spec.js#L26-L31" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/wheelTest.kt#L30-L34" >}}
{{< /tab >}}
{{< /tabpane >}}

## Desplazar desde un elemento por una cantidad determinada

Este escenario es en realidad una combinación de los dos métodos anteriores.

Para ejecutar esto utilice el método "Scroll From", que toma 3 argumentos.
El primero representa el punto de origen, que designamos como elemento,
y el segundo son los valores delta x y delta y delta.

Si el elemento está fuera de la vista,
se desplazará a la parte inferior de la pantalla, entonces la página será desplazada por el delta
y los valores delta y delta y proporcionados.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/actions_api/wheelTest.java#L42-L46" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_wheel.py#L35-L39" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/wheelTest.cs#L46-L53" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/wheel_spec.rb#L34-L38" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/actionsApi/wheelTest.spec.js#L40-L44" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/wheelTest.kt#L43-L47" >}}
{{< /tab >}}
{{< /tabpane >}}

## Desplazar desde un elemento con desplazamiento

Este escenario se utiliza cuando necesita desplazar sólo una porción de la pantalla, y está fuera de la vista.
O está dentro de la vista y la porción de la pantalla que debe desplazarse
es un desplazamiento conocido lejos de un elemento específico.

Esto utiliza el método "Desplazar desde" de nuevo, y además de especificar el elemento,
se especifica un desplazamiento para indicar el punto de origen del desplazamiento. El desplazamiento es
calculado desde el centro del elemento suministrado.

Si el elemento está fuera de la vista,
primero se desplazará a la parte inferior de la pantalla, entonces el origen del desplazamiento se determinará
añadiendo el desplazamiento a las coordenadas del centro del elemento, y finalmente
la página será desplazada por los valores delta x y delta y proporcionados.

Tenga en cuenta que si el desplazamiento desde el centro del elemento cae fuera de la vista,
resultará en una excepción.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="ejemplos/java/src/test/java/dev/selenium/actions_api/wheelTest.java#L57-L61" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_wheel.py#L50-L54" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/wheelTest.cs#L66-L75" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/wheel_spec.rb#L48-L52" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/actionsApi/wheelTest.spec.js#L57-L61" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/wheelTest.kt#L59-L63" >}}
{{< /tab >}}
{{< /tabpane >}}

## Desplazar desde una compensación de origen (elemento) por una cantidad determinada

El escenario final se utiliza cuando necesita desplazar sólo una porción de la pantalla,
y ya está dentro de la ventana.

Esto utiliza el método "Desplazar desde" de nuevo, pero la vista es designada
de un elemento. Un desplazamiento se especifica desde la esquina superior izquierda de la ventana gráfica
actual. Después de determinar el punto de origen,
la página será desplazada por los valores delta x y delta y proporcionados.

Tenga en cuenta que si el desplazamiento de la esquina superior izquierda de la vista cae fuera de la pantalla,
resultará en una excepción.

{{< tabpane text=verdad >}}
{{< tab header="Java" >}}
{{< gh-codeblock path="examples/java/src/test/java/dev/selenium/actions_api/wheelTest.java#L73-L76" >}}
{{< /tab >}}
{{< tab header="Python" >}}
{{< gh-codeblock path="ejemplos/python/tests/actions_api/test_wheel.py#L66-L70" >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< gh-codeblock path="ejemplos/dotnet/SeleniumDocs/ActionsAPI/wheelTest.cs#L89-L97" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< gh-codeblock path="ejemplos/ruby/spec/actions_api/wheel_spec.rb#L63-L66" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< gh-codeblock path="ejemplos/javascript/test/actionsApi/wheelTest.spec.js#L75-L77" >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< gh-codeblock path="ejemplos/kotlin/src/test/kotlin/dev/selenium/actions_api/wheelTest.kt#L75-L78" >}}
{{< /tab >}}
{{< /tabpane >}}
