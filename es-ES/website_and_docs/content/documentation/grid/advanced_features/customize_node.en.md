---
title: Personalizar un nodo
linkTitle: Personalizar Nodo
weight: 4
---

## Cómo personalizar un nodo

Hay momentos en los que nos gustaría que un Nodo se adaptara a nuestras necesidades.

Por ejemplo, podemos hacer alguna configuración adicional antes de que una sesión comience a ejecutarse y algo de limpieza después de que una sesión se ejecute a finalizar.

Se pueden seguir los siguientes pasos para esto:

- Crea una clase que extiende `org.openqa.selenium.grid.node.Node`
- Añadir un método estático (este será nuestro método de fábrica) a la clase recién creada cuya firma se ve así:

  `public static Node create(Config config)`. Aquí:

  - `Node` es de tipo `org.openqa.selenium.grid.node.Node`
  - `Config` es de tipo `org.openqa.selenium.grid.config.Config`
- Dentro de este método de fábrica, incluya lógica para crear su nueva clase.
- Para conectar con esta nueva lógica personalizada en el hub, iniciar el nodo y pasar el nombre de la clase anterior completamente calificada al argumento `--node-implementation`

Veamos un ejemplo de todo esto:

### Nodo personalizado como jar de uber

1. Crea un proyecto de ejemplo usando tu herramienta de construcción favorita (**Maven**|**Gradle**).
2. Añada la dependencia de abajo a su proyecto de ejemplo.
  - [org.seleniumhq.selenium/selenium-grid](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-grid)
3. Añade tu nodo personalizado al proyecto.
4. Construye un [uber jar](https://imagej.net/develop/uber-jars) para poder iniciar el nodo usando el comando `java -jar`.
5. Ahora inicie el nodo usando el comando:

```bash
java -jar custom_node-server.jar node \
--node-implementation org.seleniumhq.samples.DecoratedLoggingNode
```

**Nota:** Si estás usando Maven como una herramienta de compilación, por favor prefiere usar [maven-shade-plugin](https://maven.apache.org/plugins/maven-shade-plugin) en lugar de [maven-assembly-plugin](https://maven.apache.org/plugins/maven-assembly-plugin) porque el plugin de montaje parece tener problemas para poder combinar múltiples archivos de Interfaz de Proveedores de Servicio (`META-INF/services`)

### Nodo personalizado como jar regular

1. Crea un proyecto de ejemplo usando tu herramienta de construcción favorita (**Maven**|**Gradle**).
2. Añada la dependencia de abajo a su proyecto de ejemplo.
  - [org.seleniumhq.selenium/selenium-grid](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-grid)
3. Añade tu nodo personalizado al proyecto.
4. Construye un frasco de tu proyecto usando tu herramienta de construcción.
5. Ahora inicie el nodo usando el comando:

```bash
java -jar selenium-server-4.6.0.jar \
--ext custom_node-1.0-SNAPSHOT.jar node \
--node-implementation org.seleniumhq.samples.DecoratedLoggingNode
```

A continuación hay una muestra que simplemente imprime algunos mensajes en la consola cuando hay una actividad de interés (sesión creada, eliminada, un comando webdriver ejecutado, etc. ) en el Nodo.

<details><summary>Ejemplo de nodo personalizado</summary>

```java
package org.seleniumhq.samples;

import java.io.IOException;
import java.net.URI;
import java.util.UUID;
import java.util.function.Supplier;
import org.openqa.selenium.Capabilities;
import org.openqa.selenium.NoSuchSessionException;
import org.openqa.selenium.WebDriverException;
import org.openqa.selenium.grid.config.Config;
import org.openqa.selenium.grid.data.CreateSessionRequest;
import org.openqa.selenium.grid.data.CreateSessionResponse;
import org.openqa.selenium.grid.data.NodeId;
import org.openqa.selenium.grid.data.NodeStatus;
import org.openqa.selenium.grid.data.Session;
import org.openqa.selenium.grid.log.LoggingOptions;
import org.openqa.selenium.grid.node.HealthCheck;
import org.openqa.selenium.grid.node.Node;
import org.openqa.selenium.grid.node.local.LocalNodeFactory;
import org.openqa.selenium.grid.security.Secret;
import org.openqa.selenium.grid.security.SecretOptions;
import org.openqa.selenium.grid.server.BaseServerOptions;
import org.openqa.selenium.internal.Either;
import org.openqa.selenium.io.TemporaryFilesystem;
import org.openqa.selenium.remote.SessionId;
import org.openqa.selenium.remote.http.HttpRequest;
import org.openqa.selenium.remote.http.HttpResponse;
import org.openqa.selenium.remote.tracing.Tracer;

public class DecoratedLoggingNode extends Node {

  private Node node;

  protected DecoratedLoggingNode(Tracer tracer, NodeId nodeId, URI uri, Secret registrationSecret, Duration sessionTimeout) {
    super(tracer, nodeId, uri, registrationSecret, sessionTimeout);
  }

  public static Node create(Config config) {
    LoggingOptions loggingOptions = new LoggingOptions(config);
    BaseServerOptions serverOptions = new BaseServerOptions(config);
    URI uri = serverOptions.getExternalUri();
    SecretOptions secretOptions = new SecretOptions(config);
    NodeOptions nodeOptions = new NodeOptions(config);
    Duration sessionTimeout = nodeOptions.getSessionTimeout();

    // Refer to the foot notes for additional context on this line.
    Node node = LocalNodeFactory.create(config);

    DecoratedLoggingNode wrapper = new DecoratedLoggingNode(loggingOptions.getTracer(),
        node.getId(),
        uri,
        secretOptions.getRegistrationSecret(),
        sessionTimeout);
    wrapper.node = node;
    return wrapper;
  }

  @Override
  public Either<WebDriverException, CreateSessionResponse> newSession(
      CreateSessionRequest sessionRequest) {
    return perform(() -> node.newSession(sessionRequest), "newSession");
  }

  @Override
  public HttpResponse executeWebDriverCommand(HttpRequest req) {
    return perform(() -> node.executeWebDriverCommand(req), "executeWebDriverCommand");
  }

  @Override
  public Session getSession(SessionId id) throws NoSuchSessionException {
    return perform(() -> node.getSession(id), "getSession");
  }

  @Override
  public HttpResponse uploadFile(HttpRequest req, SessionId id) {
    return perform(() -> node.uploadFile(req, id), "uploadFile");
  }

  @Override
  public HttpResponse downloadFile(HttpRequest req, SessionId id) {
    return perform(() -> node.downloadFile(req, id), "downloadFile");
  }

  @Override
  public TemporaryFilesystem getDownloadsFilesystem(UUID uuid) {
    return perform(() -> {
      try {
        return node.getDownloadsFilesystem(uuid);
      } catch (IOException e) {
        throw new RuntimeException(e);
      }
    }, "downloadsFilesystem");
  }

  @Override
  public TemporaryFilesystem getUploadsFilesystem(SessionId id) throws IOException {
    return perform(() -> {
      try {
        return node.getUploadsFilesystem(id);
      } catch (IOException e) {
        throw new RuntimeException(e);
      }
    }, "uploadsFilesystem");

  }

  @Override
  public void stop(SessionId id) throws NoSuchSessionException {
    perform(() -> node.stop(id), "stop");
  }

  @Override
  public boolean isSessionOwner(SessionId id) {
    return perform(() -> node.isSessionOwner(id), "isSessionOwner");
  }

  @Override
  public boolean isSupporting(Capabilities capabilities) {
    return perform(() -> node.isSupporting(capabilities), "isSupporting");
  }

  @Override
  public NodeStatus getStatus() {
    return perform(() -> node.getStatus(), "getStatus");
  }

  @Override
  public HealthCheck getHealthCheck() {
    return perform(() -> node.getHealthCheck(), "getHealthCheck");
  }

  @Override
  public void drain() {
    perform(() -> node.drain(), "drain");
  }

  @Override
  public boolean isReady() {
    return perform(() -> node.isReady(), "isReady");
  }

  private void perform(Runnable function, String operation) {
    try {
      System.err.printf("[COMMENTATOR] Before %s()%n", operation);
      function.run();
    } finally {
      System.err.printf("[COMMENTATOR] After %s()%n", operation);
    }
  }

  private <T> T perform(Supplier<T> function, String operation) {
    try {
      System.err.printf("[COMMENTATOR] Before %s()%n", operation);
      return function.get();
    } finally {
      System.err.printf("[COMMENTATOR] After %s()%n", operation);
    }
  }
}
```

</details>

**_Notas de Pienzo:_**

En el ejemplo anterior, la línea `Node node = LocalNodeFactory.create(config);` crea explícitamente un `LocalNode`.

Básicamente hay 2 tipos de _implementaciones de cara al usuario_ de `org.openqa.selenium.grid.node.Node` disponibles.

Estas clases son buenos puntos de partida para aprender cómo construir un nodo personalizado y también para aprender los internos de un Nodo.

- `org.openqa.selenium.grid.node.local.LocalNode` - Se utiliza para representar un nodo de larga ejecución y es la implementación por defecto que se conecta cuando se inicia un `node`.
  - Se puede crear llamando `LocalNodeFactory.create(config);`, donde:
    - `LocalNodeFactory` pertenece a `org.openqa.selenium.grid.node.local`
    - `Config` pertenece a `org.openqa.selenium.grid.config`
- `org.openqa.selenium.grid.node.k8s.OneShotNode` - Esta es una implementación de referencia especial en la que el nodo se cierra gracamente después de atender una sesión de prueba. Esta clase no está disponible actualmente como parte de ningún artefacto de laberinto prefabricado.
  - Puedes referirte al código fuente [here](https://github.com/SeleniumHQ/selenium/blob/trunk/java/src/org/openqa/selenium/grid/node/k8s/OneShotNode.java) para entender sus internos.
  - Para construirlo localmente, refiérase a [here](https://github.com/SeleniumHQ/selenium/blob/trunk/deploys/k8s/README.md).
  - Se puede crear llamando a `OneShotNode.create(config)`, donde:
    - `OneShotNode` pertenece a `org.openqa.selenium.grid.node.k8s`
    - `Config` pertenece a `org.openqa.selenium.grid.config`
