---
title: Instantánea de mapas de carreteras de Selenium Releases
linkTitle: Hoja de ruta
weight: 15
description: |
  La lista de planes y cosas a conseguir antes de un lanzamiento
---

## Preparación para Selenium 2

Fecha desconocida
Esta documentación previamente encontrada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/RoadMap/eef12bca5fdc865449ad2d1735ee08e40ba0bd2b)

Los siguientes problemas deben resolverse antes de la versión final:

| **Problema**                                                 | **Summary**                                             | \*\*Progreso de HtmlUnitDriver \*\* | **FirefoxDriver Progreso** | **Progreso de InternetExplorerDriver** | \*\*Progreso de ChromeDriver \*\* |
| :----------------------------------------------------------- | :------------------------------------------------------ | :---------------------------------- | :------------------------- | :------------------------------------- | :-------------------------------- |
| [27](http://code.google.com/p/webdriver/issues/detail?id=27) | Manejar alertas en navegadores con Javascript           | n/a                                 | Iniciado                   | Iniciado                               | No iniciado                       |
| [32](http://code.google.com/p/webdriver/issues/detail?id=32) | Guía de usuario                                         | Iniciado                            |                            |                                        |                                   |
| [34](http://code.google.com/p/webdriver/issues/detail?id=34) | Soporte HTTP básico y Digest Authentication             | No iniciado                         |                            |                                        |                                   |
| [35](http://code.google.com/p/webdriver/issues/detail?id=35) | [Selenium](http://www.openqa.org/selenium-rc) emulación | Hecho para Java y C#                |                            |                                        |                                   |
| [36](http://code.google.com/p/webdriver/issues/detail?id=36) | Soporte para el comportamiento de arrastrar y soltar    | n/a                                 | Hecho                      | Hecho                                  | Iniciado                          |
| ninguno                                                      | Ejemplos de pruebas                                     | No iniciado                         |                            |                                        |                                   |

Se hará una versión final una vez que se hayan implementado en Firefox, IE y al menos un navegador basado en un paquete web.

### El futuro

También se han planificado las siguientes opciones:

- **JsonWireProtocol** --- La formalización del protocolo de cable de RemoteWebDriver actual en [JSON](http://www.json.org/).

## Preparación para Selenium 3

A partir del 16 de marzo de 2015
Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Shipping-Selenium-3)

### Cambios visibles del usuario

- Migrar todos los controladores para usar las cadenas de estado en lugar de códigos de estado en las respuestas
- Actualizar enlaces del cliente para hacer frente a eso
- Escribe un nuevo runner para las pruebas html-suite
- Seguye la construcción para eliminar RC

### Limpieza

- Usar WebDriver después de quit() debería ser un IllegalStateException
- Acciones para tener un único punto final
- Capacidades para ser las mismas que la especificación
- Múltiples llamadas a WebDriver.quit() deberían ser seguras.
- Limpia a los constructores de WebDriver, empujando una pesada lógica de inicialización a una clase Builder
- Migrar a Netty o servidor webbit
- Eliminar crudo innecesario
- Landa un punto final más limpio para la emulación de rc

## Preparación para Selenium 4

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/RoadMap)
A partir del 12 de abril de 2017

- Terminar el [W3C WebDriver Spec](https://w3c.github.io/webdriver/webdriver-spec.html)
- Implementar los requerimientos finales locales de la especificación en selenium
- Implementar la conversión de protocolo en el servidor independiente
- Nave 4.0
-
