---
title: Robar foco de Firefox en Linux
linkTitle: Robo de foco
weight: 12
description: |
  Cómo trabajar con eventos nativos en la extensión Legacy Firefox.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Focus-Stealing-On-Linux)

Esta página describe un componente esencial de la implementación de eventos nativos en Linux - mantenimiento del enfoque.
Para que los eventos nativos sean procesados en Firefox, siempre debe mantener el foco.
En caso de que el usuario decida cambiar a otra ventana (algo que podría ser entendido),
Firefox no debe saber que perdió el enfoque.

### Resumen de soluciones

#### idea básica

La idea básica es obtener entre la capa XLib (X-Windows cliente) y la aplicación. X-Windows notifica la aplicación de eventos (entrada de usuario, ventanas que están siendo destruidas, movimientos del ratón) por eventos asíncronos. Los eventos que indican la pérdida del foco [FocusOut](http://tronche.com/gui/x/xlib/events/input-focus/) son descartados. La idea se basa en la implementación de Jordan Sisel de una biblioteca precargada que sobre-rides XNextEvent - vea http://www.semicomplete.com/blog/geekery/xsendevent-xdotool-and-ld_preload.html.

#### Extensión

Esta sencilla implementación funciona bien siempre y cuando haya una ventana del navegador. Cuando se implican múltiples ventanas, surgen varios desafíos:

- Aunque se pueden abrir nuevas ventanas, los eventos nativos deben continuar fluyendo hacia la ventana activa. Sin embargo, la mayoría de los gestores de ventanas se centrarán en las ventanas recién abiertas.
- Cambio de ventana: Cuando se desea cambiar a otra ventana, el enfoque tiene que ser movido. Esto requiere cooperación entre la extensión de Firefox de WebDriver y este componente.
- Cerrando ventanas: cuando una ventana está cerrada, el foco debe moverse a otra ventana. Por diseño, WebDriver no garantiza nada si la ventana activa está cerrada - hasta que se cambie una nueva ventana. En esta situación, hay que prestar especial atención.

### Interacción con otros componentes

La idea básica no requiere ninguna interacción con otros componentes de WebDriver.
Sin embargo, cuando hay múltiples ventanas involucradas - creando, cambiando o destruyendo, este componente debe ser consciente de ello.
La creación de nuevas ventanas no puede ser rastreada - ya que puede ocurrir como un efecto secundario de muchas operaciones.
Se puede seguir el cambio y el cierre.

### Tecnologías implicadas

Para entender esta solución, uno debe estar familiarizado con X-Windows y sus eventos.
El conocimiento del ciclo de procesamiento de eventos GDK también es útil.

## Detalles de Implementación

Todo esto describe el código en `firefox/src/cpp/linux-specific/x_ignore_nofocus.c`.

### La biblioteca compartida

Los eventos de Pekín se realizan a través de XNextEvent.
Una biblioteca compartida que contiene una implementación modificada de `XNextEvent` se carga usando `LD_PRELOAD`.
La función modificada abre `/usr/lib/libX11.so.6` e invoca la función real.
Luego se inspecciona el evento que retorna la función real (es decir, el evento real).

### Identificando eventos

Bajo la idea básica, los eventos `FocusOut` serán simplemente descartados. Sin embargo, el interruptor de ventanas complica las cosas.

#### Estructura de datos

Hay una estructura global de datos que recuerda la siguiente información:

- El ID de la ventana activa (si existe uno en este momento)
- El ID de una nueva ventana que se está creando (nuevamente, si existe)
- Si el interruptor de ventana está en curso.
- Si se está cerrando la ventana.
- ¿Se ha dado el foco a otra ventana y debería ser robado de nuevo a la activa?
- ¿Un evento `FocusIn` ya fue recibido por la ventana activa?
- ¿Hemos establecido la ventana activa como resultado de una operación de cierre?

#### Firefox inicia

El evento `FocusIn` llega y el ID de la ventana activa es 0. Se ha establecido una nueva ventana activa. Tenga en cuenta que durante la creación de la ventana principal, se crea otra sub-ventana y se envía un evento `FocusOut` a la ventana activa. Afortunadamente, este evento `FocusOut` indica que el foco se va a mover a una sub-ventana (identificado por `NotifyInferior`) así que está permitido.

#### El usuario ha cambiado a otra ventana

Esto está indicado por un evento `FocusOut` con un campo de detalle que no es `NotifyAncestor` ni `NotifyInferior`. Este evento es simplemente descartado y reemplazado por un evento `KeymapNotify`, que es descartado rápidamente por GDK.

#### Se está creando una nueva ventana

Esta condición es identificada por un evento `ReparentNotify`. Cuando esto sucede, el campo new\_window se establecerá en el ID de la ventana recién creada. Los eventos posteriores 'FocusOut' serán permitidos - durante la creación de nueva ventana los eventos fluirán como de costumbre (evento 'FocusOut' desde la ventana activa, Evento `FocusIn` a la nueva ventana, `FocusOut` a la nueva ventana y `FocusIn` a una subventana de la nueva ventana). Después de que la subventana de la nueva ventana reciba `FocusIn`, se emitirá una llamada a `XSetInputFocus` para devolver el foco a la ventana activa.

#### Se produce un interruptor de ventana

Durante una ventana, los eventos de conmutación fluirán como siempre. Un interruptor de ventana se considera hecho cuando la subventana de una ventana recibe el evento `FocusIn`. Un interruptor de ventana comienza identificando el archivo `/tmp/switch_window_started`. En este archivo, se escribe una cadena `switch:` siguiendo un ID de ventana (el ID es sólo para depurar). Esto cambiará el ID de ventana activa a 0 y el estado a "durante el cambio". Durante un interruptor (o cuando no hay una ventana activa) no hay eventos descartados.

#### Una ventana está siendo cerrada

Muy similar al interruptor de ventanas (también identificado leyendo el archivo). Sin embargo, se indica que se está cerrando la ventana; en caso de que se cierre, no se producirá robo de enfoque. Además, el evento `DestroyNotify` está siendo identificado para averiguar cuándo la ventana activa está siendo cerrada (explícitamente por el usuario o implícitamente por alguna otra operación que no sea una llamada explícita para cerrar). En este caso, el ID de ventana activa también se establecerá en 0.

## Enlaces importantes

- Sisel de Jordan original [XSendEvent hack](http://www.semicomplete.com/blog/geekery/xsendevent-xdotool-and-ld_preload.html)
- [Eventos XLib](http://tronche.com/gui/x/xlib/events/structures.html) y el [Manual de programación XLib](http://www.sbin.org/doc/Xlib/)
- [Manual de programación X / especificación](http://www.x.org/docs/X11/xlib.pdf)
