---
title: Internacionales de Internet Explorer Driver
linkTitle: Internacionales
weight: 2
description: |
  Información más detallada sobre el conductor IE.
---

## Código del cliente en el controlador

Utilizamos el protocolo W3C WebDriver para comunicarnos con una instancia local de un servidor HTTP. Esto simplifica en gran medida la aplicación del código específico del idioma, y minimiza el número de puntos de entrada en la DLL de C++ que debe llamarse usando una tecnología de interoperación de código nativo como [JNA](https://jna.dev.java.net/), [ctypes](http://docs.python.org/library/ctypes.html), [pinvoke](http://msdn.microsoft.com/en-us/library/aa446536.aspx) o [DL](http://www.ruby-doc.org/stdlib/libdoc/dl/rdoc/index.html).

### Gestión de memoria

El controlador IE utiliza la Biblioteca de Plantillas Activas (ATL) para aprovechar su implementación de punteros inteligentes a objetos COM. Esto facilita mucho el recuento de referencias y la limpieza de objetos COM.

## ¿Por qué necesitamos cambiar los ajustes del modo protegido?

IE 7 en Windows Vista introdujo el concepto de Modo Protegido, que permite cierta protección al sistema operativo de Windows subyacente durante la navegación. El problema es que cuando se manipula una instancia de IE a través de COM, y navega a una página que causaría una transición hacia o fuera del modo protegido, IE requiere que se cree otra sesión del navegador. Esto dejará huérfano el objeto COM de la sesión anterior, sin permitirle controlarlo por más tiempo.

En IE 7, esto se manifestará normalmente como una nueva ventana del navegador de nivel superior; en IE 8, un nuevo IExplore. el proceso xe será creado, pero normalmente no siempre) Adjuntarlo perfectamente a la ventana de fotogramas de nivel superior de IE existente. Cualquier framework de automatización del navegador que maneje IE externamente (a diferencia de usar un control WebBrowser) se topará con estos problemas.

Para solucionar este problema, decimos que para trabajar con IE, todas las zonas deben tener el mismo modo protegido. Mientras esté encendido para todas las zonas, o apagado para todas las zonas, podemos prevenir las transisciones a diferentes zonas de Modo Protegido que invalidarían nuestro objeto de navegador. También permite a los usuarios continuar ejecutándose con UAC encendido, y para ejecutarse de forma segura en el navegador si ponen "encendido" el modo de protección para todas las zonas.

En versiones anteriores del controlador IE, si la configuración del modo protegido del usuario no se ha establecido correctamente lanzaríamos IE, y el proceso simplemente se cerraría hasta que se agotara el tiempo de espera de la solicitud HTTP. Esto era subóptimo, ya que no indicaba lo que había que establecer. Erring en el lado de la precaución, no modificamos la configuración del modo protegido del usuario. Versiones actuales, sin embargo compruebe que los ajustes del Modo Protegido están configurados correctamente, y devolverá una respuesta de error si no lo están.

## Entrada de teclado y ratón

Archivos de llave: [interactions.cpp](https://github.com/SeleniumHQ/selenium/blob/master/cpp/webdriver-interactions/interactions.cpp)

Hay dos maneras de simular la entrada del teclado y del ratón. La primera manera, que se utiliza en partes del webdriver, es sintetizar eventos en el DOM. Esto tiene un número de dibujos, ya que cada navegador (y la versión de un navegador) tiene sus propias peculiaridades únicas; modelar cada una de estas es una tarea exigente, e imposible de obtener por completo correctamente (por ejemplo, es difícil decir que `window. election` debe ser y esta es una propiedad de sólo lectura en algunos navegadores) El enfoque alternativo es sintetizar el teclado y la entrada del ratón en el nivel del SO idealmente sin robar el foco del usuario (quien tiende a estar haciendo otras cosas en su computadora mientras se ejecutan las pruebas de controlador web de larga duración)

El código para hacer esto está en [interactions.cpp](https://github.com/SeleniumHQ/selenium/blob/master/cpp/webdriver-interactions/interactions.cpp) La clave a tener en cuenta aquí es que usamos PostMessages para subir los eventos de la ventana a la cola de mensajes de la instancia de IE. Escribir, en particular, es interesante: sólo enviamos los mensajes "keydown" y "keyup". El evento "keypress" es creado si es necesario por el procesamiento interno de eventos de IE. Debido a que el evento de pulsación de tecla no siempre se genera (por ejemplo, no todos los caracteres son imprimibles, y si la burbuja de eventos por defecto es cancelada, los oyentes no ven el evento de la prensa de tecla) enviamos un evento de "sonda" después de la tecla. Una vez que vemos que esto ha sido procesado, sabemos que el evento de la prensa clave está en la lista de eventos a procesar, y que es seguro enviar el evento de llave. Si esto no se hace, es posible que los acontecimientos se disparen en el orden equivocado, lo que sin duda es poco óptimo.

# Trabajando en InternetExplorerDriver

Actualmente hay pruebas que se ejecutarán para InternetExplorerDriver en todos los idiomas (Java, C#, Python y Ruby), para que pueda probar sus cambios en el código nativo, sin importar en qué idioma esté cómodo trabajando desde el lado del cliente. Para trabajar en el código C++, necesitarás Visual Studio 2010 Professional o superior. Desafortunadamente, el código C++ del conductor utiliza ATL para aliviar el dolor de trabajar con objetos COM, y ATL no se suministra con Visual C++ 2010 Express Edition.  Si está usando Eclipse, el proceso para realizar y probar modificaciones es:

1. Editar el código C++ en VS.
2. Construye el código para asegurar que compila
3. Haz una reconstrucción completa cuando estés listo para ejecutar una prueba. Esto causará que la DLL creada sea copiada al lugar correcto para permitir su uso en Eclipse
4. Cargar Eclipse (o algún otro IDE, como Idea)
5. Edita el `SingleTestSuite` para que sea `usingDriver(IE)`
6. Crear una configuración de ejecución JUnit que utilice el proyecto "webdriver-internet-explorer". Si no hace esto, la prueba no funcionará en absoluto, y habrá un mensaje de error algo críptico en la consola.

Una vez finalizada la configuración básica, puede empezar a trabajar en el código bastante rápido. Puede adjuntar al proceso que ejecuta su código usando Visual Studio (desde el menú Depurar, seleccione Adjuntar a Procesos...).
