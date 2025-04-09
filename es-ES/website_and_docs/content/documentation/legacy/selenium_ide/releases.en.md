---
title: Notas de lanzamiento de Selenium IDE heredadas
linkTitle: Publicaciones
weight: 4
description: |
  Selenium IDE fue la extensión original de Firefox para Registro y Reproducción. La versión 2.x fue actualizada para soportar WebDriver.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/SeIDE-Release-Notes)

## 2.9.1 - a liberar

- Corregir - Corregir https://github.com/SeleniumHQ/selenium/issues/396
- Corregir - Cambiados enlaces de código de Google a GitHub.
- Enh - Se fusionaron los plugins de idioma oficial en el principal xpi eliminando la necesidad de multi-xpi con el principal xpi y el complemento de lenguaje múltiple xpis.
- Corregir - Corregir https://github.com/SeleniumHQ/selenium/issues/570

## 2.9.0

- Enh - Programar pruebas para la reproducción automática en un cierto tiempo o intervalos periódicos. (http://blog.reallysimplement. hts.com/2015/03/09/selenium-ide-scheduler-has-arriived-part-1/)
- Enh - Permitir el envío de información diagnóstica a través de un gist.
- Enh - Mejoras en la tala de salud, incluyendo alertas normalmente ocultas.

## 2.8.0

- Nuevo - Se ha añadido la opción de ayuda visual para ayudar a los usuarios que necesitan una apariencia más fuerte en colores, desactivada por defecto. Actívalo desde el diálogo Opciones. - Número 7696 (en Google Code)
- Nuevo - Servicio de salud para detectar excepciones no manejadas, estadísticas, métricas y diagnóstico
- Enh - Añadido elemento de menú Problemas de Búsqueda en el menú de Ayuda para hacer más fácil la búsqueda de todos los problemas para que no tengamos tantos informes duplicados del mismo problema
- Corregir - Corregido autocompletado roto - issue 7928 (en Google Code)
- Corregir - Se ha corregido la cancelación del botón de selección cuando se recarga la página - Emitir 7793 (en Google Code)
- Arreglar - Añadir botón de selección a la barra lateral y tamaño de botón reducido - Emitir 7815 (en Google Code)

## 2.7.0

- Corregir - Interrupción fija entre pestañas en el panel de información inferior de FF32 - Emitir 7824 (en Google Code)
- Corregir - Corregir para https://bugzilla.mozilla.org/show_bug.cgi?id=1016305
- Enh - Permitir que los comentarios (y comandos) abarquen el ancho completo de la tabla de comandos
- Enh - Mostrar el resultado del caso de prueba en el registro después de que se haya reproducido
- Enh - Agrupar elementos en el menú de acción por función
- Enh - Recoge más estadísticas sobre el caso de prueba y la suite incluyendo el tiempo de ejecución para propósitos reportados
- Enh - Mejorados listboxes soportando reordenar y arrastrar
- Enh - Proporciona una función de utilidad común para que los autores de plugins se ocupen de los archivos
- Enh - Permitir la pulsación de la pestaña en el cuadro de texto de comando para aceptar el autocompletado actual y mover al cuadro de texto de destino
- Enh - Selecciona una coincidencia de autocompletado cuando escribas en el cuadro de texto de comandos para acelerar la entrada manual de comandos
- Enh - Hacer que la implementación de promesas esté disponible a través de diferred.js para desarrolladores de plugins
- Enh - Hacer disponibles funciones http simples para desarrolladores de plugins
- Enh - Fácil de usar confirmaciones para uso interno y para plugins
- Corregir - Desactivar autocompletar al editar comentarios
- Corregir - Corregido error TypeError: command.isRollup no es una función
- Corregir - FixTypeError: debugContext.currentCommand no está definido
- Corregir - Fixed TypeError: this.treebox es indefinido treeView.js
- Corregir - Errores variados al seleccionar un comentario (normalmente ocultos al usuario)
- Corregir - Tipo de documento incorrecto en la superposición
- Corregir - Añadir elemento de Selenium IDE en Configuración->Menú de desarrollador - Emitir 7268 (en el código de Google)
- Corregir - Ignorar herramientas de desarrollador de Firefox durante la grabación

## 2.6.0

- Corregir - Corregido autocompletado roto en FF31+ - incidencia 7645 (en Google Code)
- Corregir - Validación de opciones en el restablecimiento de opciones - incidencia 1050 (en Google Code)
- Corregir - Formato de código C# fijo para elementos seleccionados

## 2.5.0

- Enh - Seleccione un elemento para un comando haciendo clic en el elemento en la ventana del navegador (http://blog.reallysimplehowever hts.com/2014/01/05/manually-adding-and-updating-element-locators-the-easy-way/)
- Enh - Comienza a reproducir una suite de pruebas desde cualquier caso de prueba (usando menú de clic derecho) - número 1987 (en Google Code)
- Enh - Añadir un nuevo caso de prueba usando un atajo de teclado (ctrl-N o cmd+N)
- Corregir - Borrado fijo de caso de prueba a través del menú de clic derecho a veces fue deshabilitado - problema 5003 (en Google Code)
- Corregir - El ícono de Selenium IDE arreglado a veces no es visible - issue 5712 (en Google Code)
- Corregir - Corregida ventana de selección usando una variable - incidencia 3270 (en Google Code)
- Algunos cambios menores

## 2.4.0

- Enh - Historia de URL base, los casos de prueba recientes y las suites de pruebas recientes se pueden eliminar - el número 6135 (en Google Code)
- Enh - La clave especial ahora tiene nombres más cortos (http://blog.reallysimplethough, 2013/09/25/using-special-keys-in-selenium-ide-part-2/)
- Enh - Soporte para las extensiones de usuario en la reproducción del controlador web - número 5675 (en Google Code)
- Corregir - La grabación de introducir texto en los campos utiliza el tipo en lugar de enviarKeys.
- Enh - Cuando las herramientas del desarrollador están activas, el último caso de prueba abierto o suite se abre automáticamente
- Corregir - Corregido es`*` comandos en la reproducción del controlador web en Selenium IDE - Emitir 6118 (en Google Code)
- Enh - Agregar capacidad para mostrar comandos como obsoletos en Selenium IDE y smartness para mostrar el comando alternativo correcto
- Enh - Desaprobar comandos de Selenium IDE `*`TextPresent, typeKeys, keyUp, keyDown y keypress
- Enh - Importar biblioteca json en las pruebas exportadas de Ruby Webdriver
- Enh - Añadir soporte para los comandos waitFor`*` y waitForNot`*` en la reproducción del controlador web - emitir 5913 (en Google Code)

## 2.3.0

- Nuevo - Añadido soporte para grabación de campos de entrada HTML5 - número 3765 (en Google Code)
- Nuevo - Grabación del comando sendKeys
- Enh - Quitar los comandos obsoletos `*`TextPresent desde el menú de clic derecho
- Corregir - Error de objeto muerto en la grabación de pruebas de IDE - issue 4761 (en Google Code)
- Corregir - Corregido no se pudo continuar en la grabación - problema 5820 (en Google Code)
- Enh - Soporte UTF-8 codificado user-extensions.js - issue 1646 (en Google Code)
- Nuevo soporte de claves especiales para sendKeys en Selenium IDE y reproducción del controlador web - número #6052 (en Google Code)
- Nuevo - Soporte de claves especiales para sendKeys en todos los formatos oficiales - número 6053 (en Google Code) (http://blog.reallysimplethough, hts.com/2013/09/25/using-special-keys-in-selenium-ide-part-1/)
- Enh - Mejora de Plugin api para especificar el tipo de formateador + comentarios de documentación
- Corregir - Error XPath no válido en Firefox 23 - incidencia 6055 (en Google Code)
- Nuevo - Añadido soporte para Firefox 23

## 2.2.0

- Corregir - keyUp, keyDown, keyPress, typeKeys arreglados en Firefox 22 - emitir 5883 (en Google Code), emitir 5884 (en Google Code)

## 2.1.0

- Enh - Plugin system changed (http://blog.reallysimplenonetheless 2013/07/changes-to-selenium-ide-plugin-system/)
- Nuevo - Añadido soporte para Firefox 22 + 23 beta
- Corregir - Click arreglado para Firefox 22 - issue 5841 (en Google Code)

## 2.0.0

- Nuevo - Soporte de reproducción de WebDriver (http://blog.reallysimpledeehts.com/2013/02/18/webdriver-playback-in-selenium-ide-is-here/)
- Nuevo - Añadido soporte para Firefox 19 y 20
- Nuevo - El icono de IDE de Selenium en la barra de herramientas se añade en la primera instalación

## 1.10.0

- Nuevo - Añadido soporte para Firefox 16 & 17
- Nuevo - Implementado formato para comandos de manejo de alertas
- Error - Opciones corregidas para el formato WebDriver de Java 4
- Error - Procesando localizadores antes de usar en getCssCount y getXpathCount. Corregir la incidencia 4784 (en Google Code)

## 1.9.1

- Nuevo - Añadido soporte para Firefox 15
- Nuevo - Añadido soporte para assertTextPresent, verifyTextPresent, waitForTextPresent, assertTextNotPresent, verifyTextNotPresent, waitForTextNotPresent comandos a los formatos WebDriver formatters. (http://blog.reallysimplehowever hts.com/2012/08/26/selenium-ide-webdriver-formatters-updated-to-support-textpresent-commands/)
- Nuevo - Se añadieron los parámetros de destino y valor en los comentarios cuando los formateadores WebDriver no soportan el comando

## 1.9.0

- Nuevo - Añadido sendKeys comando Selenese (http://blog.reallysimplehowever hts.com/2012/07/19/new-selenese-command-sendkeys/)
- Nuevo - Mejor nombre de formatos
- Nuevo - Añadido soporte para Firefox 14

## 1.8.1

- Nuevo - Añadido soporte para Firefox 13

## 1.8.0

- Nuevo - Añadido soporte para Firefox 12

## 1.7.2

- Error - Regresión corregida con tecleo en los campos de entrada del archivo - issue 3549 (en Google Code)

## 1.7.1

- Error - Regresión corregida con variables almacenadas - Emitir 3520 (en Google Code)

## 1.7.0

- Nuevo - Añadidos elementos de menú adicionales útiles al menú de ayuda
- Nuevo - Añadido soporte para Firefox 11
- Error - Las variables almacenadas pueden contener signos consecutivos en dólares - incidencia 834 (en Google Code)
- Error - No recortar espacios en blanco al decodificar casos de prueba HTML - emitir 755 (en Google Code)
- Nuevo - Los elementos del menú Formatter son ahora sensibles al contexto - problema 3327 (en el código de Google) y emite 3385 (en el código de Google)
- Error - Exportación de la suite de pruebas Ruby WebDriver corregida - incidencia 3243 (en Google Code)
- Error - Extensiones de archivo añadidas a todos los selectores de archivos - incidencia 3336 (en Google Code)
- Error - Grabar interacciones con elementos con un id de 'id' - emitir 3273 (en Google Code)

## 1.6.0

- Nuevo - Añadido soporte para Firefox 10
- Nuevo - Añadidos atajos de teclado para lanzar Selenium IDE - incidencia 3028 (en Google Code)
- Error - Se añadió un comando de ruptura a la lista de autocompletar - problema 3046 (en Google Code)
- Error - descripción incorrecta mostrada en la barra lateral - incidencia 3098 (en Google Code)
- Error - Grabación mejorada del localizador XPath cuando hay múltiples coincidencias - incidencia 3056 (en Google Code)
- Error - Locators can now be reorder on Mac - issue 3267 (en Google Code)

## 1.5.0

- Nuevo - Añadido soporte para Firefox 9
- Error - Los cambios a las extensiones de usuario no se actualizaban en Firefox 8 - número 2801 (en Google Code)
- Error - Error al intentar escribir en los campos de entrada de archivo (subir) de Firefox 8 - incidencia 2826 (en Google Code)
- Error - Mejora de la localización francesa - Problema 1912 (en Google Code)
- Error - comando break falló - emite 725 (en Google Code)
- Error - la vista de origen ahora es de ancho fijo (monospace) - Emite 522 (en Google Code)
- Nuevo - Implementado formato 'seleccionar' para enlaces WebDriver (Java, C#, Python, Ruby)
- Error - Se han corregido errores de tiempo de compilación y tiempo de ejecución en el código formateado para WebDriverBackedSelenium
- Error - Se corrigieron errores de formato 'baseUrl' y 'get' en varios formateadores para manejar URLs relativas y absolutas

## 1.4.1

- Error - Aparentemente he enviado sin cambiar todos los números de versión correctamente. (Adán)

## 1.4.0

- Nuevo - soporte para Firefox 8 (otra vez, sólo un bump de versión máxima)

## 1.3.0

Va a ser solo un lanzamiento rápido

- Nuevo - soporte para Firefox 7 (otra vez, sólo un bump de versión máxima)

dentro, pero entonces me ocupé y no lo empujé cuando había planeado y ahora

- Nuevo - El orden de los localizadores se puede controlar a través de un panel en opciones.

se ha filtrado. La mayoría de la gente querrá dejar esto de la manera predeterminada. Esto es nuevo en la marca y te permite hacer visualmente lo que pudiste antes de usar un poco arcano de JS en una extensión.

## 1.2.0

Sólo una versión rápida principalmente para

- Nuevo - soporte para Firefox 6 (que realmente estaba cambiando el número máximo de versión)

Pero también nos enganchamos en

- Error - Localizador CSS grabado no fue W3C clean wrt attributes
- Error - La eliminación de cookies funciona correctamente si el nombre de la cookie está escapado (como los sitios ASP)
- Error - Si el valor de la cookie tiene un = en ella, la cookie completa ahora es devuelta en lugar de sólo hasta la =

También notará que el paquete ahora sólo tiene formateadores para los idiomas oficialmente soportados del proyecto (Java, C#, Python, Ruby). Si alguien de los campamentos de Perl, Groovy o PHP quiere tomar posesión de esos formatos, le ayudaremos felizmente.

## 1.1.0

¡Hola! ¡Mira esto! ¡Una versión algo más significativa! ¿Por qué? Bueno...

- Nuevo - exportaciones de WebDriver para Ruby, Python, C# y Java

Cuatro idiomas apoyados en el proyecto Selenium. Esto también significa que Se-IDE está oficialmente obsoleto la inclusión de los plugins de formato Groovy, Perl y PHP en el paquete principal de lanzamientos. Sería excepcional que la comunidad alrededor de esos idiomas recogiera su desarrollo y mantenimiento. Lee más sobre los exportadores de WebDriver en [Samit blog](http://blog.reallysimplethoughts.com/2011/07/08/selenium-ide-and-selenium-2-webdriver/).

Por supuesto, el cambio de formato todavía está en purgatorio Experimental para al menos esta versión. Perder scripts de la gente debido a errores no es aceptable y estamos trabajando en ello. "Objetivo" es tenerlos de vuelta para la próxima versión.

También se incluyen en esta versión

- Nuevo - setIndent(n) ahora está disponible en formatos para un mayor control sobre el formato de los formatos de exportación
- Error - Hubo una regresión de rendimiento en lo profundo de algún código compartido que se ha abordado.
- Nuevo - En lugar de grabar 'foo' para un elemento que y un id de 'foo' es capturado como 'id=foo' para ser muy específico con qué elemento se interactuaría
- Nuevo - Igual con 'nombre'
- Nuevo - Las ventanas emergentes (alertas, confirmaciones, avisos) y nuevas ventanas vuelven a funcionar

## 1.0.12

Esta es una versión menor con nada demasiado grande incluido. Pero debido a que el último no fue empujado al mundo, es importante tomar nota de un gran cambio introducido en 1.0.11.

Hemos marcado el cambio de formatos como _Experimental_ debido a un par de errores de pérdida de todos sus datos. Como resultado, está desactivado en la barra de herramientas de forma predeterminada. Para activarlo, haga clic en la casilla de verificación del menú Opciones. Y porque **realmente** no queremos que pierdas tus datos, cuando cambies de formato, obtendrás una gran caja de advertencia. Esto también puede desactivarse en el menú Opciones. Pero si usted hace ambas cosas y su guión se envía al abismo, se le ha advertido. :)

Los cambios en esta versión incluyen lo siguiente:

- Nuevo - soporte para Firefox 5
- Nuevo - Al actualizar el Se-IDE, las notas de lanzamiento (estas) se muestran en el primer inicio
- Error - algunos cambios en el formato Java
- Error - algunos cambios en el formato PHP
- Error - el botón 'Encontrar' vuelve a funcionar
- Error - CSS generado cumple con los estándares
- Nuevo - se ha eliminado el soporte para FF 3.5 o anterior

## 1.0.11

Ha pasado medio año desde nuestra última versión de 1.0.10 y hemos puesto un gran esfuerzo para traerle esta versión. El resumen de las contribuciones a esta versión es el siguiente: -

| 73% (22) | Maldita Samit            |
| :-------------------------- | :----------------------- |
| 16%( 5)  | Goucher Adam             |
| 6% (2)   | Cacería de Dave          |
| 3% (1)   | Santiago Suarez Ordoñez |
| 3% (1)   | Simon Stewart            |

Aquí está la lista de cambios que excluyen algunas correcciones menores y refactorización de código.

### Características principales:

- Soporte para Firefox 4 (número 1470 (en Google Code), Simon Stewart y Samit Badle)
- ¡Nuevo constructor de localizadores CSS! Selenium IDE creará ahora localizadores usando CSS al grabar (Santiago Suarez Ordonëez)
- Se ha añadido más energía a los desarrolladores de plugins a través del nuevo soporte de constructores de comandos de Util (Issue 442 (en Google Code), Samit Badle)
- Nuevo comando getCssCount (Adam Goucher)

### Mejoras de usabilidad:

- Selenium IDE ya está disponible en el menú del desarrollador Web en Firefox 4 (número 1467 (en el código Google), Samit Badle)
- Se ha mejorado la búsqueda de Casos de Camello en el cuadro de comandos que permite escribir vTP para el comando VerifyTextPresent (Samit Badle with Dave Hunt)
- La mayoría de las acciones en Selenium IDE ahora son accesibles a través del nuevo menú Actions (número 1266 (en el código de Google), Samit Badle y Dave Hunt)
- Se eliminaron los elementos del menú de ayuda relacionados con Firefox de Selenium IDE (número 1704 (en Google Code), Samit Badle)
- Menos información al guardar la suite de pruebas (número 967 (en Google Code), Samit Badle)
- Un método para restablecer la ventana de IDE está ahora disponible a través del menú Opciones para personas que tienen problemas al cambiar desde múltiples monitores (Número 1249 (en Google Code), Mala de Samit)
- Mostrar el nombre del caso de prueba en el cuadro de diálogo de guardado (número 984 (en el código de Google), Samit Badle)
- Las preferencias para el formato actual se mostrarán automáticamente en el diálogo de opciones (Samit Badle)
- El panel de plugins en el diálogo de opciones ahora tiene un separador (Samit Badle)
- El campo Valor de tiempo de espera por defecto en el diálogo de opciones ahora menciona una unidad (asunto 896 (en Google Code), Adam Goucher)
- Opciones experimentales introducidas para ocultar algunas características inestables (Samit Badle)

### Corregir errores:

- El cambio de formato ahora está marcado como experimental debido a posibles problemas, puede activarlo desde el diálogo de opciones (Samit Badle)
- Se ha corregido el problema de cabecera al guardar el caso de prueba en otro formato (Número 1164 (en el código de Google), Samit Badle)
- Alerta mejorada al cambiar el formato (Samit Badle)
- El botón Buscar está de vuelta en Macs y utiliza una nueva forma de resaltarse (Número 1052 (en Google Code), Samit Badle)
- La grabación es posible en medio de un script de nuevo (Número 968 (en Google Code), Samit Badle)
- Se ha corregido el molesto saltar sobre un comando al grabar en medio del script (Issue 745 (en Google Code), Samit Badle)
- Durante la grabación, el comando "clickAndWait" se convierte en "click" ahora está arreglado (problema 419 (en Google Code), Samit Badle)
- El plegado del panel inferior del IDE Selenium ahora funciona correctamente (número 614 (en el código de Google), Insignia de Samit)
- Cambiado el ID del menú IDE de Selenium desde el nombre genérico para evitar choques con otros complementos. (Número 969 (en Google Code), Samit Badle)

### Mejores/Arreglos relacionados con los formatos:

- Soporte fijo para variables almacenadas en formato PHP (número 970 (en código Google), Samit Badle)
- Permitir a los formateadores personalizar cómo se maneja el set`*` (Adam Goucher)
- Algunas correcciones de errores en el formateador PHP (número 1281 (en el código de Google), Adam Goucher)
- Tipo de número fijo (Jeremy Herault)
- Nuevo formateador de Java: Formateador de Junit 4 respaldado
- Nuevo formateador PHP: Prueba de formato selenium (Adam Goucher)

### Problemas conocidos:

- Número 1728 (en Google Code) - Firefox 4 eliminó el soporte para el resaltado. Así que el botón Buscar ha dejado de funcionar bajo Firefox 4 en Windows.
- Número 1729 (en Google Code) - El panel del plugin en el diálogo Opciones no muestra ningún texto en Firefox 4 en Windows 7.
- Se han notificado problemas en Selenium IDE en Ubuntu 11, que no están relacionados con el IDE de Selenium. Ver comentarios sobre el número 1642 (en Google Code).

## 1.0.10

Otro problema de empaquetado rompió las diversas cosas que usaron getText(). ¿Cuál por supuesto es uno de los bits más utilizados de la API.

- BUG - incluyendo correctamente los átomos de se-core

Como resultado, hemos comenzado a reconstruir la suite de pruebas para las cosas. Va a tomar un tiempo para obtener la cobertura que esperamos, pero valdrá la pena si podemos ir al menos 2 días después de una liberación antes de quedar embarazado.

Notas de actualización:

- Debido a que los átomos se incluyen correctamente, algunos de los comportamientos en torno al acceso a los atributos booleanos han cambiado. Vea http://seleniumhq.wordpress.com/2010/12/09/atoms-have-come-to-selenium-ide/ para detalles.

## 1.0.9

Lo que comenzó como un cambio bastante importante en términos de empaquetamiento terminó incluyendo dos correcciones significativas de errores. Esperemos que evitemos este tipo de cosas con la liberación. No es que no lo espere. :)

- BUG - Biblioteca CSS de Sizzle no incluida
- BUG - Grabación funciona con FF 4.0b7

¿Qué se suponía que 1.0.9 sólo tendría que haber sido...

- NUEVO - Los Formatters son **todos** los plugins. Esto separa efectivamente el desarrollo de un formato individual del desarrollo del editor. Ahora, esto significa que cuando se instalan cosas por primera vez se obtiene una tonelada de complementos. Eso está bien. No te preocupes. Oh, y también significa si no quieres que tengan la opción. Esto no solo significa arreglos a formatos se distribuyen antes (PHP, Te estoy mirando), pero las terceras partes podrán hacer mejores opciones de empaquetado teniendo el editor más sus formateadores.

Otras cosas

- BUG - el formato JUnit 4 no intenta usar una cadena como número de puerto
- BUG - la ventana al crear nuevos formatos se cierra ahora correctamente
- BUG - eliminó el botón 'encontrar' si en OSX ya que no hace nada en esta plataforma (su error FF)
- BUG - algunas cadenas de código duro han sido internacionalizadas
- NUEVO - el autocompletado se ha mejorado algo - ver http://code.google.com/p/selenium/issues/detail?id=992
- BUG - al cambiar los sistemas de construcción, los iconos de los menús y tales quedaron fuera del paquete
- BUG - Los comandos son recortados de espacios en blanco antes de ejecutarse, lo cual a veces fue una fuente de gran confusión
- BUG - Ahora conserva espacios en blanco cuando se muestra difiere en el registro

## 1.0.8

Esta versión es principalmente para conseguir soporte para FF4 en salvaje ya que está llegando a la fase beta avanzada, pero también hay un poco de otras correcciones de errores allí. Aproximadamente el 75% de las correcciones en la versión son directamente obra de Samit Badle y el inmenso resto de Jérémy Hérault.

- BUG - Hubo un error molesto donde 'clickAndWait' se guardaría como clic, pero ha sido arreglado. vea http://code.google.com/p/selenium/issues/detail?id=419
- NUEVA -Esto podría considerarse una corrección de errores, pero si ha cambiado el formato de HTML a otra cosa, entonces hizo una edición y volvió a cambiar a HTML el contenido de su script se perdería. En su corazón, el HTML -> algo de conversión es un camino y ahora hay una advertencia sobre la posible pérdida de su código. La advertencia sólo ocurre la primera vez, así que todavía puedes dispararte a ti mismo en el pie; es más difícil
- BUG - el localizador de elementos funciona para las filas de la tabla. vea http://code.google.com/p/selenium/issues/detail?id=485
- BUG - la configuración predeterminada de tiempo de espera de se-ide ahora se utiliza. vea http://code.google.com/p/selenium/issues/detail?id=552
- NUEVO - la opción "correr en el testrunner de selenio" ha sido eliminada. Los métodos soportados en se-ide son el juego único, play suite y si necesita más siempre hay se-rc con un enlace de idioma o -htmlSuite
- BUG - la url base no cambiaría en ocasiones, mucho a la frustración de muchos
- NUEVO - se añadió un formateador JUnit 4
- BUG - el formato RSpec tenía algunos ajustes adicionales
- BUG - la suite de pruebas html ahora puede tener pruebas de diferentes carpetas
- BUG - prueba que los disparadores de ahorro de suite recibieron un poco de atención, así que añadir/eliminar/modificar es un poco más robusto
- NUEVA - si cambia el tamaño de su lado y/o lo mueve alrededor de su pantalla, el tamaño y la posición se guardan entre las sesiones
- BUG - la lógica alrededor de cuándo pedir ahorro no era realmente tan buena, pero se ha arreglado
- NUEVO - utiliza 'átomos del navegador' como el resto de Selenium
- Nueva - La ejecución del localizador CSS se gestiona a través de Sizzle
- NUEVO - ahora puede agregar múltiples casos de prueba a una suite a la vez
- NUEVO - adición a la api del plugin se-ide para añadir extensiones se-ide para manipular cómo se hace la grabación - http://reallysimplethings.wordpress.com/2010/10/11/the-selenium-ide-1-x-plugin-api-part-12-adding-locator-builders/
- NUEVO - el caso de los mensajes de registro faltantes está resuelto
- NUEVO - Soporte para Firefox 4

## 1.0.7

Sólo un par de cosas de nota en esta versión para los usuarios finales que es un poco tonto ya que es un mes atrasado, pero eso fue debido a algunos cambios en la compilación que tomaron un poco de trabajo para que funcionaran los parches. No obstante, debería estar bien ahora.

- NUEVO - ahora puedes arrastrar y soltar el comando en lugar de la danza de cuchara-pega que solías hacer (Jérémy Hérault)
- NUEVO - lo mismo con las pruebas en el panel de la suite de pruebas (Jérémy Hérault)
- NUEVO - un nuevo parámetro opcional al registrar el plugin se-ide para permitir la exportación de comandos. ver http://adam.goucher.ca/?p=1456 para más detalles (Adam Goucher)
- NUEVO - Locale sueca sv-SE ahora tiene traducciones (Olle Jonsson)
- BUG - Algunas personas estaban reportando una molesta ventana emergente al iniciar se-ide sin ningún plugin instalado (Adam oucher)

## 1.0.6

Lo importante de esta versión es que el mensaje de registro aterrador que se mostraba en 'abierto' está arreglado. Las otras cosas grandes son:

- BUG - El mensaje de registro aterrador que estaba ocurriendo cuando utilizaste 'open' ha corregido su causa subyacente (Adam Goucher, Jérémy Hérault)
- BUG - arreglado un problema de compilación con FF 3.6 y type-ahead para comandos (Jérémy Hérault)
- BUG - arreglado algunos problemas de exportación de PHP - vea http://jira.openqa.org/browse/SIDE-346 y http://jira.openqa.org/browse/SIDE-183 (Adam Goucher)
- BUG - hubo un problema de empaquetado alrededor de las extensiones de usuario (Adam Goucher)
- BUG - junto no pondrá 'name=' como el objetivo al grabar una ventana de selección (David Burns)
- BUG - para evitar confusión, al ver la fuente del formato, si se lee sólo el botón dice "ok" y si es editable, entonces es "save" (Jérémy Hérault)
- NUEVO - ahora puede establecer una preferencia sobre si desea que el registro esté encendido o apagado cuando inicie el lado (Adam Goucher)
- NUEVO - la información del plugin se lee desde install.rdf del plugin (la mayoría de la gente no le importa esto, pero es bastante genial desde una perspectiva geek)

## 1.0.5

Una cosa que no encaja realmente en la etiqueta BUG o NUEVA es que el código para Se-IDE está ahora en el repositorio principal en lugar de escondido en un lugar algo oculto.

- BUG - los formatos de usuario no aparecieron en la lista (Adam Goucher)
- BUG - restringido cómo iframes fueron cargados; por eso AMO estaba descontento (Adam Goucher)
- BUG - un montón de ajustes a los formatos existentes (Dave Hunt)
- BUG - un montón de correcciones / adiciones de traducción al francés (Jérémy Hérault)
- BUG - el botón de recargar las extensiones de usuario sólo se muestra si tienes la casilla de verificación de herramientas de desarrollador (Jérémy Hérault)
- BUG - etiquetar las teclas de acceso en el corredor de pruebas (Olle Jonsson)
- BUG - limpiado un montón de referencias de OpenQA a SeleniumHQ (Olle Jonsson)
- BUG - tenía un = en lugar de == (Olle Jonsson)
- BUG - añadir un puñado de ;'s para hacer cerrar jslint (Olle Jonsson)
- BUG - deshacerte de la "configuración de algo que sólo tiene un getter" mensaje en Firefox 3.6 (Dan Fabulich)
- NUEVA - Auto alojamiento de actualizaciones para evitar retrasos en AMO (Adam Goucher)
- NUEVO - la versión de se-ide está ahora en la barra de título (Adam Goucher)
- NUEVA - agregó algunos iconos específicos de Se-IDE aquí y allá (Adam Goucher, Dave Hunt)
- NUEVA - las preferencias ahora también pueden ser Bool's (Adam Goucher)
- NUEVO - añadido addPlugin(id) a la API del plugin (Adam Goucher)
- NUEVO - añadido un nuevo panel a la pantalla de opciones alrededor de los plugins. No hace mucho más que listar los plugins que se registraron a través de addPlugin, pero debería hacer más por 1.0.6 (Adam Goucher)

## 1.0.4

Selenium IDE 1.0.4 marca un resurgimiento en el proyecto con versiones previstas para mediados de cada mes. Aquí están los cambios que han ocurrido entre las versiones 1.0.2 y 1.0.4 de Selenium IDE. (No preguntes qué pasó con la versión 1.0.3)

- BUG - Se ha aumentado la versión compatible de Firefox para incluir la serie 3.6 (Santiago Suarez Ordonez)
- BUG - Eliminado el formateador de Ruby que fue marcado como 'obsoleto' (Adam Goucher)
- NUEVO - Formateador de Ruby actualizado para utilizar la gema selenium-cliente ( http://selenium-client.rubyforge.org/ ) (Adam Goucher)
- NUEVA - Posibilidad de añadir extensiones de usuario personalizadas para extender Selenium API a Selenium IDE (Adam Goucher)
- NUEVA - Posibilidad de añadir formatos personalizados para extender qué idiomas están disponibles para los usuarios a través de plugins para Selenium IDE (Adam Goucher)
- NUEVO - Ahora puede cargar cambios en las extensiones de usuario sin tener que reiniciar Selenium IDE (Jérémy Hérault)
- NUEVO - formato RSpec

### Agradecimientos

La versión 1.0.4 no habría ocurrido sin la siguiente asistencia

- El patrocinio de Adam Goucher para trabajar en él
- Jérémy Hérault y el equipo de SERLI para su plugin de Helium (que fue la prueba de que una API podría / debe ser desarrollada para Se-I
- Dave Hunt por sus comentarios sobre las versiones anteriores

Para problemas con esta versión o características que te gustaría ver en futuras versiones, por favor inicia sesión en el rastreador de problemas de Google Code (https://github. om/SeleniumHQ/selenium/issues) usando la etiqueta _ide_ para que no se pierdan.

-adam
