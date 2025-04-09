---
title: Historial de Plataformas cuadriculadas
linkTitle: Plataformas cuadrícula
weight: 10
description: |
  Información para trabajar con nombres de plataforma en la cuadrícula 2.
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Grid-Platforms) \
Puedes leer más acerca de [Grid 2]({{< ref "grid_2.md" >}})

## Plataformas cuadrícula de Selenium

Esta sección describe la opción PLATFORM utilizada para configurar los nodos cuadrícula de Selenium y el objeto [[DesiredCapabilities](DesiredCapabilities)].

### Historial de plataformas

Al solicitar una nueva sesión WebDriver desde la Grid, el usuario puede especificar el [[DesiredCapabilities](DesiredCapabilities)] del navegador remoto. Cosas como el nombre del navegador, la versión y la plataforma están entre la lista de opciones que pueden ser especificadas por la prueba. Especificando deseado.

El siguiente código demuestra la DesiredCapability de Internet Explorer, versión 9, en la plataforma Windows XP:

```
	[[DesiredCapabilities]] capability = DesiredCapabilities.internetExplorer();
	capability.setVersion("8");
	capability.setPlatform(Platform.XP);
	controlador WebDriver = new RemoteWebDriver(new URL("http://localhost:4444/wd/hub"), capacidad); capacidad);
```

La solicitud de una nueva sesión con la DesiredCapability especificada es enviada al Grid Hub, que buscará a través de todos los nodos registrados para ver si alguno de ellos coincide con la especificación dada por la prueba. Si ningún nodo coincide con la especificación, se devolverá una CapabilidadNotPresentOnTheGridException.

Es una idea errónea común que el PLATFORM determina la capacidad de elegir el Sistema Operativo en el que se creará la nueva sesión. En esta situación, la plataforma y el sistema operativo no son los mismos, por lo tanto, especificar la plataforma a "Windows 2003 Server" no le permitirá elegir entre un servidor Windows XP, Vista, y 2003. Este concepto erróneo puede nacer de plataformas como Mac OSX y Linux, donde el nombre de la plataforma coincide con el nombre del sistema operativo.

En el caso de Selenium Grid, la plataforma se refiere a las interacciones subyacentes entre los Atoms Driver y el navegador web. Sistemas operativos basados en Mac OSX y Linux (Centos, Ubuntu, Debian, etc.) tienen una comunicación relativamente estable con los navegadores web como Firefox y Chrome. Así, los nombres de la plataforma son fáciles de entender, como se ve en el ejemplo siguiente:

```
   capability.setPlatform(Platform.MAC); //Set platform to OSX
   capability.setPlatform(Platform.LINUX); // Establecer plataforma a sistemas basados en Linux
```

El anterior al lanzamiento de Vista, Windows based Operating Systems sólo tenía una plataforma, mostrada aquí:

```
	capaciability.setPlatform(Platform.WINDOWS); //Set platform to Windows
```

Sin embargo, con la introducción de UAC en Windows Vista, se hicieron cambios importantes en las interacciones subyacentes entre WebDriver y Internet Explorer. Para solucionar las restricciones UAC se añadió una nueva plataforma a los nodos con sistemas operativos basados en Windows:

```
	capaciability.setPlatform(Platform.VISTA); //Establecer plataforma a VISTA
```

Con el lanzamiento de Windows 8, otra revisión importante ocurrió en cómo el WebDriver se comunica con Internet Explorer, por lo tanto se añadió una nueva plataforma para los nodos basados en Windows 8:

```
	capaciability.setPlatform(Platform.WIN8); //Establecer plataforma a Windows 8
```

La historia similar ocurrió con la introducción de Windows 8.1, en este ejemplo la plataforma se establece en Windows 8.1:

```
	capaciability.setPlatform(Platform.WIN8_1); //Establecer plataforma a Windows 8.1
```

### Plataformas de sistema operativas

La siguiente lista muestra algunos de los sistemas operativos, y de qué plataforma forman parte:

**MAC\*\*\*\*Todos los sistemas operativos OSX** LINUX
Centos
Ubuntu
**UNIX****Solaris****BSD** XP
Windows Server 2003
Windows XP
Windows NT
**VISTA****Windows Vista****Windows 2008 Server\*\*\*\*Windows 7** WIN8
Windows 2012 Server
Windows 8
**WIN8\_1\*\*\*\*Windows 8.1**

### Familias

Diferentes plataformas se agrupan en "Familias" de plataforma. Por ejemplo, las plataformas Win8 y XP forman parte de la familia WINDOWS. Del mismo modo, ANDROID y LINUX forman parte de la familia UNIX.

### Elegir la plataforma y la familia de las plataformas

Al configurar una plataforma en el objeto [[DesiredCapabilities](DesiredCapabilities)], podemos establecer una plataforma individual o una familia de plataformas. Por ejemplo:

```
  	capaciability.setPlatform(Platform.VISTA); //Will devuelve un nodo con Windows Vista o 2008 Server o Windows 7 Operating System.
  	capaciability.setPlatform(Plataforma. P); //Will return a node with Windows XP or 2003 Server or Windows 2000 Professional Operating System.   
  	capaciability.setPlatform(Platform.WINDOWS); //Devolverá un nodo con CUALQUIER sistema operativo de Windows
```

### Más información

Para más información sobre las últimas plataformas, por favor vea este archivo:

org.openqa.selenium.Platform.java
