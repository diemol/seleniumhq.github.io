---
title: Limitaciones de pruebas de escalado en Selenium 2
linkTitle: Ejecución paralela
weight: 11
description: |
  Resumen de restricciones adicionales que surgen al ejecutar Selenium2 en paralelo.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Scaling-WebDriver)

## Ejecutando paralelo Selenium2

Esta página trata de resumir restricciones adicionales que surgen cuando se ejecuta Selenium2 en paralelo.

### Instanciación WebDriver

Mientras que una instancia individual de WebDriver no se puede compartir entre los hilos, es fácil crear múltiples instancias de WebDriver.

### Sockets efeméricos

Hay un problema general de TCP/IP v4, donde la pila TCP/IP utiliza puertos efeméricos cuando se hace una conexión entre dos sockets. El síntoma típico de esto es que las fallas de conexión comienzan a aparecer después de un corto tiempo de funcionamiento, a menudo de un minuto o dos. El mensaje variará un poco pero siempre aparece después de algún tiempo, y si reduce el número de navegadores eventualmente funcionará bien.

[Wikipedia on Ephemeral ports](http://en.wikipedia.org/wiki/Ephemeral_port) o un Google rápido de "efemeral sockets <your os name>" te dirá qué entrega tu sistema operativo actual y cómo configurarlo.

Actualmente (2.13. ) parece que un firefox que corre a plena explosión consume algo en el rango de 2000 puertos efeméricos por bombero; su kilometraje variará aquí. Esto significa que puede
quedarse sin puerto efemeral en Windows XP con tan poco como 2 navegadores, tal vez incluso 1 si por ejemplo iteran extermly rápido .

#### ¿Se arreglará?

La solución al problema del socket efemeral es HTTP1.1 mantener vivo las conexiones. Firefox no soporta keep-alive desde la versión 2.13.0.

#### Cosas que están arregladas

- El cliente Java.
- Servidor Selenium ("rc").
- Selenium grid hub & nodes
- Los enlaces de rubí (ver notas en [RubyBindings](RubyBindings.md)).
- El controlador IE.
- Controlador de cromo

Esto significa que puede usar el cliente java para escalar a cajas remotas ejecutando selenium server y nunca tener problemas en el servidor central de compilación. Sin embargo, es posible que tenga que resolver problemas de socket en las cajas remotas.

#### Microsoft Windows

Si está utilizando las versiones antiguas de Windows (<=2003, inc XP) no debería estar
esperando que el uso del puerto sea lo suficientemente bajo como para caber en este espacio. Puede que eso simplemente nunca suceda, aunque algunas combinaciones probablemente lo harán. Consulte http://support.microsoft.com/kb/196271 sobre cómo ajustarlo.

Si por razones técnicas no puede ajustar el rango de puertos de su máquina Windows no podrá ejecutar más de 2-3 navegadores firefox.

### Evitar bloqueo de socket

Iniciar nuevos navegadores entre cada clase de prueba/método de prueba es lento, y el bloqueo de socket también utiliza sockets Ephemeral, empeorando el problema descrito anteriormente.

Si está utilizando una configuración de prueba sin soporte (como muchos usuarios JUnit4), a menudo inicia/detiene los navegadores en los métodos @BeforeClass/@AfterClass. Otra opción es iniciar los navegadores en @BeforeClass y usar algo como JUnit/TestNG run listeners para apagar todos los navegadores al final de la ejecución de pruebas.  Maven surefire soporta escuchadores tanto para JUnit como para TestNG.

(TODO: Estrategias para desactivar el bloqueo de socket y administrar los puertos usted mismo)

### Eventos nativos

Debido a un archivo compartido en la lógica de eventos nativos, el controlador firefox probablemente no debería estar usando eventos nativos cuando se ejecuta simultáneamente. (Ver [este problema](http://code.google.com/p/selenium/issues/detail?id=1326)).
