---
title: Resumen de Selenium
linkTitle: Resumen
weight: 1
description: |
  ¿Es Selenium para usted? Vea una visión general de los diferentes componentes del proyecto.
aliases:
  - /documentation/es/introduction/
---

Selenium no es solo una herramienta o API;
contiene muchas herramientas.

## WebDriver

Si está comenzando con la automatización de pruebas del sitio web de escritorio o del sitio web móvil, entonces
va a usar las API de WebDriver . [WebDriver](/documentation/webdriver)
utiliza API de automatización del navegador proporcionadas por los proveedores del navegador para controlar el navegador y
ejecutar pruebas. Esto es como si un usuario real estuviera operando el navegador. Dado que
WebDriver no requiere que su API sea compilada con el código
de la aplicación, no es intrusiva. Por lo tanto, está probando la
misma aplicación que empuja en directo.

## IDE

[IDE](//selenium.dev/selenium-ide) (Entorno de desarrollo integrado)
es la herramienta que utiliza para desarrollar sus casos de prueba de Selenium. Es una extensión de Chrome
y Firefox fácil de usar y es generalmente la forma más eficiente de desarrollar casos
de prueba. It records the users' actions in the browser for you, using
existing Selenium commands, with parameters defined by the context of
that element. Esto no es solo un ahorrador de tiempo, sino también una excelente manera
de aprender la sintaxis de scripts de Selenium.

## Rejilla

Selenium Grid le permite ejecutar casos de prueba en diferentes máquinas
entre diferentes plataformas. El control de
desencadenando los casos de prueba está en el extremo local y
cuando los casos de prueba se activan, son automáticamente
ejecutados por el extremo remoto.

Después del desarrollo de las pruebas de WebDriver, usted puede enfrentar
la necesidad de ejecutar sus pruebas en múltiples navegadores y
combinaciones del sistema operativo.
Aquí es donde [Grid](/documentation/grid) entra en la foto.
