---
title: Solución de problemas de asistencia
linkTitle: Solución de problemas
weight: 20
description: |
  Cómo resolver problemas de WebDriver.
---

No siempre es evidente la raíz de los errores en Selenium.

1. El error más común relacionado con Selenium es el resultado de una mala sincronización.
  Lee sobre [Esperando estrategias]({{< ref "../waits" >}}). Si no estás seguro de si
  es una estrategia de sincronización puedes intentar programar _temporalmente_ duramente un sueño grande
  donde ves el problema, y sabrá si añadir una espera explícita puede ayudar.

2. Note that many errors that get reported to the project are actually caused by
  issues in the underlying drivers that Selenium sends the commands to. Puedes descartar
  un problema de controlador ejecutando el comando en múltiples [browsers]({{< ref "../browsers/" >}}).

3. Si tienes preguntas sobre cómo hacer las cosas, revisa las [opciones de soporte](/support/)
  para encontrar formas de obtener asistencia.

4. Si crees que has encontrado un problema con el código de Selenium, sigue adelante y archiva un
  Informe de error
  en GitHub.


