---
title: WebDrivers para navegadores móviles
linkTitle: Móvil
weight: 13
description: |
  Describe cómo Selenium 2 soporta Android e iOS antes de que se creó Appium
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Untrusted-SSL-Certificates)

## Introducción

Proporcionamos controladores móviles para dos plataformas móviles principales: Android e iOS (iPhone e iPad).

Pueden ejecutarse en dispositivos reales y en un emulador Android o en el simulador de iOS, según corresponda. Están empaquetados como una aplicación. La aplicación necesita estar instalada en el emulador o dispositivo. La aplicación incrusta un [Servidor RemoteWebDriver](https://github.com/SeleniumHQ/selenium/wiki/RemoteWebDriverServer) y un servidor HTTP ligero que recibe, y responde, las solicitudes de los clientes WebDriver i. . de sus pruebas automatizadas.

La conexión entre el servidor en la plataforma móvil y sus pruebas utiliza una conexión IP. La conexión puede necesitar ser configurada. Para Android se puede conectar establecer una conexión IP por USB.

En algunos casos las pruebas existentes de WebDriver pueden ejecutarse con éxito p.ej. donde un sitio web común sirve a usuarios móviles y de escritorio y donde la interfaz de usuario es relativamente sencilla. Sin embargo, en otros casos puede que tenga que crear pruebas específicas para el sitio móvil; particularmente cuando el sitio proporciona capacidades específicas, interfaces de usuario, etc. para navegadores móviles.

Incluso cuando un sitio web común sirve navegadores de escritorio y móviles, puedes considerar la posibilidad de escribir pruebas específicas que incorporen factores como el tamaño de pantalla de los dispositivos móviles, y diferentes maneras de que los usuarios puedan interactuar con su sitio web o aplicación web.

## Comenzando

[Android Setup](https://github.com/SeleniumHQ/selenium/wiki/AndroidDriver)

[Configuración de iPhone y iPad](https://github.com/SeleniumHQ/selenium/wiki/IPhoneDriver)

## Plataformas móviles adicionales

Hay varios proyectos de código abierto relacionados que incluyen soporte para otras plataformas móviles. Estos incluyen:

[Blackberry WebDriver](http://code.google.com/p/webdriver-blackberry/), para BlackBerry 5.0 y posterior.

[Headless WebKit WebDriver](http://code.google.com/p/webkitdriver/). Muchos navegadores móviles están basados en WebKit. WebKit sin cabezas proporciona una solución rápida de peso ligero.

Estos proyectos no parecen estar activos, pero pueden proporcionar un punto de partida para futuros trabajos en estas plataformas.
