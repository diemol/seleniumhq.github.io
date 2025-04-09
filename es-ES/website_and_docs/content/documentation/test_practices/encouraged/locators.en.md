---
title: Consejos para trabajar con localizadores
linkTitle: Localizadores
weight: 8
description: |
  Cuándo usar qué locadores y cómo administrarlos mejor en tu código.
---

Echa un vistazo a los ejemplos de las [estrategias de localización soportadas]({{< ref "/documentation/webdriver/elements/locators.md" >}}).

En general, si los IDs HTML están disponibles, únicos y consistentemente
predecibles, son el método preferido para localizar un elemento en
una página. Tienden a trabajar muy rápidamente, y para mucho procesamiento
que viene con complicados travesías de DOM.

Si los ID únicos no están disponibles, un selector CSS bien escrito es el método
preferido para localizar un elemento. XPath funciona tan bien como selectores de CSS
, pero la sintaxis es complicada y frecuentemente difícil de depurar
. Though XPath selectors are very flexible, they are typically
not performance tested by browser vendors and tend to be quite slow.

Selection strategies based on _linkText_ and _partialLinkText_ have
drawbacks in that they only work on link elements. Additionally, they
call down to [querySelectorAll](https://www.w3.org/TR/webdriver/#link-text) selectors internally in WebDriver.

El nombre de la etiqueta puede ser una forma peligrosa de localizar elementos. There are
frequently multiple elements of the same tag present on the page.
Esto es principalmente útil cuando se llama al método _findElements(By)_ el cual
devuelve una colección de elementos.

La recomendación es mantener sus locadores tan compactos y
legibles como sea posible. Pedir a WebDriver que recorra la estructura
de DOM es una operación costosa, y cuanto más puede reducir el alcance de
su búsqueda, mejor.
