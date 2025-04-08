---
title: Respaldar Selenium con WebDriver
linkTitle: Emulaciones
weight: 3
description: |
  Las versiones Java y .NET de Selenium 2 proporcionaron implementaciones de la API original de Selenium
---

(Alocado anteriormente: https://github.com/SeleniumHQ/selenium/wiki/Selenium-Emulation)

## Respaldar Selenium con WebDriver

Las versiones Java y .NET de WebDriver proporcionan implementaciones de la API Selenium existente. En Java, se utiliza así:

```
// Puede utilizar cualquier implementación de WebDriver . Firefox se utiliza aquí como ejemplo
controlador WebDriver = new FirefoxDriver();

// Una "base url", utilizada por selenium para resolver URLs relativas
String baseUrl = "http://www. oogle.com";

// Crear la implementación de Selenium
Selenium selenium = new WebDriverBackedSelenium(driver, baseUrl);

// Realizar acciones con selenium
selenium. pen("http://www.google.com");
selenium.type("name=q", "cheese");
selenium.click("name=btnG");

// Y recuperar la implementación de WebDriver subyacente. Esto se referirá a la instancia
// misma de WebDriver que la variable "driver" arriba.
controlador WebDriver driverInstance = ((WebDriverBackedSelenium) selenium).getUnderlyingWebDriver();
```

## Pros

- Permite a WebDriver y Selenium vivir lado a lado.
- Proporciona un mecanismo sencillo para una migración administrada de la API Selenium existente a WebDriver.
- No requiere que el servidor RC de Selenium sea ejecutado

## Contra

- No implementa todos los métodos
    - ¡Pero nos encantarían los comentarios!
- También emula el Núcleo de Selenium
    - Por lo tanto, el uso más avanzado de Selenium (es decir, el uso de "browserbot" u otros métodos incorporados de Javascript de Selenium Core) puede necesitar trabajo
- Algunos métodos pueden ser más lentos debido a las diferencias subyacentes en la implementación
- No soporta "extensiones de usuario" de Selenium (_i.e._, user-extensions.js)

### Notas

Después de crear una instancia `WebDriverBackedSelenium` con un controlador dado, uno no tiene que llamar a `start()` - ya que la creación del controlador ya comenzó la sesión. Al final de la prueba, `stop()` debe llamarse **en su lugar** del método `quit()` del Motivador.

Esto es más similar al comportamiento de WebDriver - al crear una instancia de Drivers inicia una sesión, sin embargo tiene que ser terminada explícitamente con una llamada a `quit()`.

## Respaldar Selenium con RemoteWebDriver

A partir de la versión 2.19, `WebDriverBackedSelenium` puede ser usada desde cualquier idioma soportado por WebDriver y Selenium.

Por ejemplo, en Python:

```
driver = RemoteWebDriver(desired_capabilities = DesiredCapabilities.FIREFOX)
selenium = DefaultSelenium('localhost', '4444', '*webdriver', 'http://www.google.com')
selenium.start(driver = driver)
```

Proporcionado que usted mantiene una referencia a los objetos originales WebDriver y Selenium que usted creó, usted puede usar incluso las dos APIs de forma intercambiable.  La magia es el nombre del navegador "\*webdriver" pasado a la instancia de Selenium y que pasas la instancia de WebDriver cuando llamas a `start()`.

En idiomas donde DefaultSelenium no tiene `start(driver)`, usted puede conectar los objetos WebDriver y Selenium juntos, suministrando el ID de sesión WebDriver al objeto Selenium.

Por ejemplo, en C#:

```

RemoteWebDriver driver = new RemoteWebDriver(DesiredCapabilities.Firefox());
string sessionId = (string) driver.Capabilities.GetCapability("webdriver.remote.sessionid");
DefaultSelenium selenium = new DefaultSelenium("localhost", 4444, "*webdriver", "http://www.google.com");
selenium.Start("webdriver.remote.sessionid=" + sessionId);
```

## Colaborando WebDriver con Selenium

WebDriver no es compatible con tantos navegadores como Selenium , así que para proporcionar ese soporte mientras todavía se utiliza la API del controlador web, puedes hacer uso del `SeleneseCommandExecutor` Se hace así:

```
Capacidades capacidades = new DesiredCapabilities()
capabilities.setBrowserName("safari");
Ejecutor de CommandExecutor = new SeleneseCommandExecutor("http:localhost:4444/", "http://www.google.com/", capacidades);
controlador WebDriver = new RemoteWebDriver(executor, capacidades);
```

Actualmente hay algunas limitaciones importantes con este enfoque, principalmente que `findElements` no funciona como se esperaba. Además, debido a que estamos usando Selenium Core para la pesada carga de conducir el navegador, usted está limitado por el sandbox Javascript.
