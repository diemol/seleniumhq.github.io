---
title: Mezclas sobre cómo llegaron las cosas
linkTitle: Historial
weight: 14
description: |
  Detalles sobre todo de interés para los desarrolladores de Selenium sobre cómo y por qué se crearon ciertas partes del proyecto
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/History)

## Introducción

Se trata de un trabajo en curso.  Siéntete libre de añadir cosas que sabes o recuerdas.

### ¿Cómo llegaron los tomos de automatización?

En 2012-04-04, jimevans preguntó en el canal #selenium IRC:

> "Lo que quería preguntarle sobre la historia de los átomos de automatización.  Parece que me acuerdo de que se formaron totalmente, como si fuera de la cabeza de Zeus, y estoy seguro de que no era así. ¿Puedes actualizar mi memoria sobre cómo ocurrió el concepto?"

simonstewart luego continuó para contarnos una pequeña historia bonita:

> Claro.  ¿Estamos sentados tranquilamente?  Entonces empezaré.  (Broma de Brit, ahí)

> Imaginen las líneas onduladas como la pantalla se disuelve y nos transportamos de vuelta a cuando el selenium y el webdriver eran diferentes proyectos.  Antes de fusionar los proyectos, había un montón de código congruente en el webdriver.  Congruente, pero no compartido.  El controlador de Firefox estaba en JS.  El controlador IE era principalmente C++.  El controlador Chrome era principalmente JS, pero JS diferente del controlador de Firefox. Y HtmlUnit fue único.

> Luego agregamos Selenium Core a la mezcla.  Sin embargo, más JS que básicamente hizo lo mismo.

> Dentro de Google, me estaba convirtiendo en la TL del equipo de automatización del navegador.  Y corrinar un marco propio en la mezcla.  El cual estaba escrito en JS, y una vez se había basado en el núcleo antes de que se extendiera por su propio camino.

> Por ejemplo: múltiples bases de código, muchos JS hacen más o menos la misma cosa.  Y muchos errores.  Extraños discordancias de comportamiento en casos extremos.

> `*Timón*`

> Así que pensé un poco. (Dangeroso, lo sé) La idea era extraer el "mejor de la raza" código de los tres marcos (núcleo, WebDriver y la herramienta Google).  Divínalos en código que podría ser compartido.  "La unidad más pequeña e indivisible de la automatización del navegador" .

> O "átomos" para corto.

> Estos pueden ser usados como la base del _everything_.  Comportamiento consistente entre navegadores.  y apis.  El otro punto importante era que el código JS en webdriver y núcleo se cultivaba orgánicamente.  Que es una forma educada de decir "preferiría no volver a editarlo".  Que es una forma educada de decir que era de dudosa calidad .  En lugares.

> Por lo tanto, la alta calidad era importante.  Y quería que el código se dividiera en módulos.  Porque editar un archivo LOC de 10k no es una idea brillante.

> Dentro de Google teníamos una biblioteca llamada Closure.  Que no sólo permite la modularización, sino la "desormalización" de los módulos en un solo archivo vía compilación.  Y sabía que estaba siendo de código abierto.  Así que empezamos a construir la biblioteca en el código de Google.  (Donde tuvimos acceso a la biblioteca no publicada, a las herramientas de revisión de código y a nuestra increíble infraestructura de pruebas).  Usando Closure Library.

> "dom.js" fue probablemente el primer archivo que voy a hablar.  (Podemos comprobarlo).  Greg Dennis y Jason Leyba se unieron a la diversión.  Y los átomos han ido creciendo cada vez más.

> Tecnológicamente, deberíamos estar llamando a cualquier cosa fuera de las moléculas "javascript/atomas".  Pero entonces no podemos decir que tengamos conductores atómicos.  y utilice imágenes de los años 50 para describirlas.

> `*alerta*`

jimevans respondió: "¿Controladores moleculares?"

Y simonstewart terminó con:

> De hecho, :) La idea es que los átomos son el nivel más bajo.  Y componemos los átomos para cumplir con los apis WebDriver o RC en "javascript/{selenium,webdriver}-atoms" de forma respectiva.  Y luego chupar a los dentro como sea necesario.

### Una historia de loca diversión

Simon Stewart :

> Por lo tanto, volvamos al principio mismo del proyecto<br>

<blockquote>Cuando fui yo, en mi propia<br>
(el proyecto del controlador web, es decir, no selenium en sí mismo)<br>
sabía que quería cubrir varios idiomas diferentes, y así quería una herramienta de construcción que pudiera funcionar con todos ellos<br>
Es decir, que no tenía una preferencia incorporada por una que hizo que trabajar con otros lenguajes dolorosos<br>
es java sesgada. Como se hace.<br>
nant y msbuild son . et sesgado<br>
rake, otoh, no soporta nada muy bien<br>
Pero, y esto es clave, cualquier script de rastrillo válido es también un programa de Rutin válido<br>
Es posible extender el rastrillo para construir <i>cualquier cosa</i><br>
So: rake fue<br>
El archivo inicial de rastrillo era bastante pequeño y manejable<br>
Pero a medida que creció el proyecto, lo mismo hizo el Rakefile<br>
Hasta que sólo había una persona que podía lidiar con él (yo), e incluso entonces fue bastante shaky<br>
Así que, en lugar de tener un proyecto que no se pudo construir, He extraído algunos métodos de ayuda para hacer algunos de los trabajos pesados<br>
lo que hacía que el Rakefile volviera a ser posible<br>
Pero ellos proyectan nada. consiguiendo. Mayor<br>
Y el Rakefile se hizo cada vez más difícil de grok<br>
En ese momento, yo estaba trabajando en Google, que tienen un maravilloso sistema de construcción<br>
el sistema de Google es declarativo y funciona en varios idiomas diferentes consistentemente<br>
Y, más importante, separa la compilación de un solo archivo en pequeños fragmentos<br>
Le pregunté a los chaps de OSS en Google si estaba bien abrir la gramática de la compilación, y le dieron la luz verde<br>
Así que creamos gramática en el código base de selenium<br>
Con un cambio menor (manejamos argumentos de diccionario)<br>
Pero esa gramática se sienta sobre el rake<br>
hasta ahora, después de todo este tiempo<br>
Y hay un problema<br>
Y eso es que el rastrillo es un solo hilo<br>
Así que nuestras construcciones están limitadas a ejecutar serialmente<br>
Podríamos usar tipos de "multitarea" para mejorar las cosas, pero cuando he intentado que las cosas se pusieron muy desordenadas, muy rápido<br>
Así que nuestro siguiente hurdle es esa diversión crazyfun. b es lento: necesitamos ir más rápido<br>
Lo cual implica una reescritura de crazyfun<br>
Estoy más cómodo en java<br>
Así que He sacado una nueva versión en java que maneja la compilación java y js<br>
Es significativamente más rápido<br>
Pero, y esto también es importante, es una espiga<br>
El código fue diseñado para ser desechable.<br>
Ahora que las cosas han quedado demostradas. Realmente me gustaría hacer una implementación limpia<br>
Pero estoy desgarrado<br>
Do I "finish" the new, muy rápido java de crazyfun lo suficiente como para reemplazar la versión ruby?<br></blockquote>

### Una historia de ejecutivos de conductores

<blockquote><br>
    evoca<br>
noob_einsteinsfo: correcto, tiempo de la historia, entonces. ¿Estamos sentados así? entonces comenzaremos.<br>
noob_einsteinsfo: back when i first started working on the project (circa 2010), the drivers for all of the browsers were built and maintained by the project.<br>
En ese momento, eso significaba IE, firefox, y cromo.<br>
todos esos controladores fueron empaquetados como parte del servidor independiente selenium y también fueron empaquetados con los diversos enlaces de idioma.<br>
this was a conscious decision, so that if one were running locally, there would be no need for the java runtime on the machine just to automate a given browser.<br>
había dos factores que condujeron al desarrollo de controladores de navegador como ejecutables separados.<br>
como un lado rápido, recuerda que la filosofía del controlador web es automatizar el navegador utilizando el mecanismo "mejor" para ese navegador en particular.<br>
for IE, that means using the COM interfaces; for firefox at the time, that meant using a browser extension; for chrome, it also meant a browser extension.<br>
de modo que el controlador IE se desarrolló como DLL en C++ que fue cargado por los enlaces de idioma, y se comunicó a través de cualquier mecanismo de código nativo proporcionado por el lenguaje (JNI para java, P/Invoke para . ET, tipos de cables para pitón, etc.).<br>
it also meant that the firefox driver was developed as a browser extension that was packaged inside the various language bindings, and extracted, and used in a profile in firefox.<br>
como he dicho, el controlador IE se implementó como una DLL, cargada y comunicada con el uso de diferentes mecanismos para diferentes enlaces de idioma.<br>
el problema es que cada uno de esos mecanismos específicos del lenguaje tenía diferentes semánticos de carga/descarga.<br>
ruby, por ejemplo, nunca llamaría a la API de windows de FreeLibrary después de cargar la DLL en la memoria, haciendo que múltiples instancias sean realmente desafiantes.<br>
*process* semantics, however, as in, starting, stopping, and managing the lifetime of a process on the OS, whatever the OS, are remarkably similar across all languages.<br>
so when the IE driver rewrite was completed in 2010, the development team (me) decided to make it a separate executable, so that the load/unload semantics could be consistent no matter what language bindings one was using.<br>
simultáneamente con esto, el equipo de cromo tomó la decisión de seguir el plomo de la ópera y proporcionar una implementación del controlador para el cromo.<br>
Una implementación que desarrollarían, mejorarían y continuarían avanzando, lo que aliviaría el proyecto del selenio de la carga de mantener un conductor cromado.<br>
<br>
    XgizmoX<br>
y ese controlador es parte del navegador?<br>
<br>
    evoca<br>
XgizmoX: no realmente, pero creo que puede haber algunos inteligentes incorporados en el cromo mismo que sabe cuando está siendo automatizado a través de Chromedriver. uno de los googlers sería una persona mejor para preguntarle por eso.<br>
de todos modos, conociendo lo diferente en librería compartida (.dll/.so/. ynlib) cargando semántica, el equipo de cromo (con mi aliento) decidió liberar su implementación de chromedriver como un ejecutable separado.<br>
avance rápido un par de años, y empieza a ver el esfuerzo de hacer del webdriver un estándar w3c.<br>
un grupo de trabajo con el w3c creó una especificación (aún en curso, pero acercándose a la conclusión con la primera versión), que codificó el comportamiento del controlador web, y cómo un navegador debe reaccionar a sus métodos. Además, estandarizó el protocolo utilizado para comunicarse entre los enlaces de idioma y un controlador para un navegador en particular.<br>
no puedo hacer énfasis en lo importante e innovador que fue esto.<br>
because the w3c and the webdriver working group within it are made up of representatives from the browser vendors themselves, it ensures that the solution will be supported directly by the browser vendors.<br>
mozilla creó su implementación webdriver (geckodriver) para firefox.<br>
the most efficient mechanism for distribution of that browser driver, while maintaining the proper semantics for the language bindings, was to ship as a separate executable.<br>
note, this is a gross oversimplification of the geckodriver architecture; the actual executable acts as a relatively thin shim, translating from the wire protocol of the spec to their internal marionette protocol<br>
but the point still stands.<br>
de todos modos, el paisaje está evolucionando actualmente con respecto a la implementación del controlador proporcionado por el navegador. microsoft has one for edge, apple has one for safari (10 and above), the chromium team (largely staffed by googlers) has one for chrome, and now mozilla has one for firefox.<br>
dada la utilidad limitada del controlador de firefox legado que avanza, dividirlo en un ejecutable separado se desperdiciaría esfuerzo.<br>
esto es particularmente así, ya que todos los bits de comunicación que normalmente son manejados por el ejecutable (escuchando y respondiendo a peticiones http desde los enlaces de idioma) son manejados enteramente por la extensión del navegador. \<br>
literalmente no hay necesidad de que el controlador de firefox heredado sea un ejecutable separado.<br>
Además, hacerlo independiente de un tiempo de ejecución de un lenguaje sería una porción significativa del trabajo<br>
(porque a . ET shop puede ser bastante reticente a ser requerido para instalar, digamos, el tiempo de ejecución de Java sólo para automatizar firefox)<br>
tan históricamente hablando, noob-einsteinsfo, esa es la razón general por la que ejecutivos separados se han convertido en la norma, y por qué ese paradigm no se extendió para incluir el controlador firefox legado.<br>
¿Tiene sentido?<br>
vale.<br>
ahora.<br>
sobre geckodriver.<br>
el cuento de geckodriver está íntimamente vinculado con el estado de la especificación principal del controlador web w3c.<br>
El nivel 1 de la especificación está casi hecho, aunque se necesitaron varios años de esfuerzo para llegar allí.<br>
it took a large effort from some very smart people (AutomatedTester among them) to mold the initial documentation of what the webdriver open source software (OSS) project did into proper specification language that could be interpreted and turned into actionable stuff by a browser vendor or other implementor.<br>
when beginning the geckodriver (nee marionette) project, mozilla decided to base their implementation on the spec, and only the spec, not following the OSS implementation.<br>
esto creó algo así como un problema con el huevo y el pollo, en que aunque el lenguaje de especificación no se completó, no se pudo implementar.<br>
sólo ha sido en los últimos seis meses o así que el lenguaje concerniente a las interacciones avanzadas con el usuario api (la clase Actions en java y . ET) se ha hecho lo suficientemente robusto como para implementar realmente.<br>
En consecuencia, ese es el mayor pedazo de funcionalidad que falta en geckodriver actualmente. no se pudo implementar a través de la especificación, por lo que no se ha implementado.<br>
sé que es una prioridad muy alta para AutomatedTester y su equipo para conseguir que la implementación se haga y esté disponible.<br>
en cuanto a por qué geckodriver es obligatorio, y la implementación predeterminada para automatizar firefox en 3. , eso también se reduce a algunas decisiones tomadas por mozilla.<br>
<br>
    TheSchaf<br>
así que supongo que no hay otra opción que usar la antigua FF siempre y cuando falten características requeridas<br>
WhereIsMySpoon<br>
TheSchaf: si necesitas estas características, sí<br>
o usar otro navegador<br>
TheSchaf<br>
bueno, moveTo y sendKeys debe ser bastante básico :p<br>
<br>
    jimevans<br>
TheSchaf: elemento. endKeys funciona bien. Es Actions.sendKeys que se rompería.<br>
in firefox version fortysomething (i misremember the exact version), there was a feature added that blocked browser extensions that hadn't been signed by the mozilla security team.<br>
recordar que el controlador firefox heredado fue construido como una extensión del navegador? bueno, con esa característica del navegador activada, el controlador antiguo no pudo ser cargado por el navegador.<br>
now, for several versions of firefox, it was possible to disable this feature of the browser, and allow unsigned extensions to continue to be loaded.<br>
y selenium hizo esto, gracias a la configuración utilizada en el perfil anónimo los enlaces creados al lanzar firefox.<br>
hasta que el firefox 48, en cuyo momento, ya no era posible desactivar la carga de extensiones sin firmar.<br>
En ese momento, geckodriver era la única manera de avanzar para eso.<br>
ahora, dos puntos más ligeros, entonces lo haré con el tiempo de la historia.<br>
first, by nature of what the legacy driver extension does, it's not possible to get it to pass the certification process of the mozilla security team.<br>
Preguntamos, fueron denegados, y se nos dijo que no sucedería nunca, el punto completo.<br>
y eso es perfectamente razonable, ya que lo que hace esa extensión es un agujero de seguridad lo suficientemente grande como para conducir toda una flota de lorrias.<br>
second, it turns out there may, in fact, be a way to privately sign the legacy extension so that it can be loaded and used privately by versions of firefox 48 and higher.<br>
that's still a less-than-ideal approach, because there's no way that our merry band of open source developers can know how to automate firefox better than the development teams at mozilla, who create the browser in the first place.<br>
i totally get the frustration that geckodriver doesn't have the full feature parity of the legacy implementation, especially when it feels like one is being forced to move to it.<br>
Enfurecerse por el proyecto del selenio sobre esa decisión está dirigiéndose a la ira en la dirección totalmente incorrecta.<br>
however, before going off and saying horrible things about mozilla's decisions, do know that mozilla has several people who are constantly engaged in the project, a few of them right here in this very channel (AutomatedTester, davehunt, to name two).<br>
Estoy seguro de que he analizado o malinterpretado algunos de los detalles históricos de estas cosas, y estoy feliz de ser corregido. Soy viejo, después de todo, y la memoria no es lo que solía ser.<br>
but that, my friends, is the (not so very) short history of why we have separate executables for drivers, and why geckodriver is the way forward, and why a move to it was necessary when the move was made even though some functionality was lacking.<br>
<br>
jimevans siente que se ha convertido en un histórico no oficial del proyecto webdriver<br>
<br>
<br>
</blockquote>

transcript: https://bot.me/freenode/selenium/2016-12-21/?msg=78265715&page=6

<h2>Un nombre informal de nuestros lanzamientos (por tema de canal en IRC)</h2>

- Selenium 2 beta 3 'la próxima generación de versión del navegador' ya está disponible - <a href='http://bit.ly/i9bkC2'>http://bit.ly/i9bkC2</a>

- Selenium 2 RC1 'la versión de cuadrícula' ahora disponible - <a href='http://bit.ly/jgZxW8'>http://bit.ly/jgZxW8</a>

- Selenium 2 RC2 el 'funciona mejor versión' ahora disponible - <a href='http://bit.ly/mJJX1z'>http://bit.ly/mJX1z</a>

- Selenium RC3 - "el siguiente es el lanzamiento "grande" - <a href='http://bit.ly/kpiACx'>http://bit.ly/kpiACx</a>

- Selenium 2.0 Final se desató sobre las masas desmirantes

- Selenium 2.1.0 ya está disponible (sí, incluso para usuarios en maven ahora)

- Selenium 2.2.0 ahora disponible (en nuget .. y sí, incluso maven)

- Selenium 2.3.0 disponible ahora. ¡Una nueva tradición!

- Selenium 2.4.0 está fuera -- cosas cambiadas, pero aún no hay ninguna entrada en el blog

- Selenium 2.5.0. mmm. bacón.

- Selenium 2.6.0 ya está disponible. Cambie y ahorre un 15% o más en el seguro de automóvil

- Enlaces de Ruby para Selenium 2.7.0 primero de la puerta (en twitter a cualquier ritmo). Jari es una máquina...

- Selenium 2.8.0 está saliendo ahora -- el bacon del día sigue siendo el bacon

- tristemente nos faltan registros IRC...

- Selenium 2.22: El mes de lanzamiento semanal es finalmente aquí!

- Selenium 2.23: "¡Ahora con genial!" Espera. ¿Qué? ¡Ahora?!

- Selenium 2.24: Ahora con más, erm, las cosas?

- Selenium 2.25: Seguimiento agradable

- ¡2.26 está fuera!

- Selenium 2.27 ha sido lanzado con correcciones para Firefox 17. ¡Consíguelo mientras está caliente!

- (no hubo una actualización del tema 2.28) code.google.com/p/selenium espejado en github.com/seleniumHQ/selenium - ¡estamos en git ahora!

- 2.29.0 ya no está! ¡Primer lanzamiento de git con soporte FF18!

- ¡BOOM! 2.31 es lanzado con soporte para eventos nativos para Firefox 19 incluso.

- "correlación no implica causa" 2.32.0 liberada con el soporte de Firefox 20.

- ¡el gobierno de los EE.UU. está abierto de nuevo! Celebremos con 2.36 recientemente lanzado, con soporte FF24

- 2.40 es mucho automatizado, así que corrige este tipo de awe

- 2.41 - la última versión "soportada" de ie6

-

- 2.45.0 - publicado con soporte FF36

- 2.46.0 - publicado con soporte FF38

- 2.47.0 - publicado con soporte Edge

- 2.48.0 - publicado con soporte para Marionette en todos los idiomas

- 2.49.0 Publicado - con soporte FF 43

- 2.50.0 Lanzado - "¡Son todos los casos de borde sangriento!" - D.W-H

- 2.51.0 Lanzado - "¡Son todos los casos de borde sangriento!" - D.W-H

- 2.52.0 Lanzado - ¡Ahora puedes desactivar "todos los casos de borde sangriento!"

- 2.53.0 El RC FINAL RELEASE

- 3.0 ¡La versión navideña! FF48 ahora requiere GeckoDriver

- 3.6 La versión "Not Released On A Friday"
