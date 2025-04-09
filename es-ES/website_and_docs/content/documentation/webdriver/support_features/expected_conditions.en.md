---
title: Esperando con las condiciones esperadas
linkTitle: Condiciones Esperadas
weight: 1
description: |
  Estas son clases usadas para describir lo que hay que esperar.
---

Las condiciones esperadas se utilizan con [Esperas Explicitas]({{< ref "../waits#explícit-waits" >}}).
En lugar de definir el bloque de código a ser ejecutado con un _lambda_, se puede crear un método
condiciones esperado para representar cosas comunes que se esperan. Algunos métodosformat@@0
toman los localizadores como argumentos, otros toman elementos como argumentos.

Estos métodos pueden incluir condiciones como:

- el elemento existe
- elemento es obsoleto
- elemento es visible
- el texto es visible
- el título contiene el valor especificado

{{< tabpane text=verdad >}}
{{< badge-code >}}
{{< tab header="Python" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Carrete" >}}
{{< /tab >}}
{{< tab header="Ruby" >}}
{{< /tab >}}
{{< tab header="JavaScript" >}}
{{< badge-code >}}
{{< /tab >}}
{{< tab header="Kotlin" >}}
{{< badge-code >}}
{{< /tab >}}
{{< /tabpane >}}
