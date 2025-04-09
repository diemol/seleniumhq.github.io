---
title: External datastore
linkTitle: External datastore
weight: 5
---

## Tabla de contenidos

- [Introduction](#introduction)
- [Setup](#setup)
- [Mapa de sesión respaldado por la base de datos](#database-backed-session-map)
 - [Steps](#steps)
- [Mapa de sesión respaldado por Redis](#redis-backed-session-map)
 - [Steps](#steps)

## Introducción

Selenium Grid le permite persistir información relacionada con la ejecución actual de sesiones en una tienda de datos externa.
El almacén de datos externo podría estar respaldado por su sistema de caché de base de datos (o) favorito.

## Configurar

- [Coursier](https://get-coursier.io/docs/cli-installation) - Como resolución de dependencias, para que podamos descargar artefactos de laberinto sobre la marcha y ponerlos a disposición en nuestro classpath
- [Docker](https://docs.docker.com/engine/install/) - Para administrar nuestros contenedores docker PostGreSQL/Redis.

## Mapa de sesiones respaldado por base de datos

Por el bien de esta ilustración, vamos a trabajar con la base de datos PostGreSQL.

Vamos a girar una base de datos PostGreSQL como un contenedor docker usando un archivo docker compuesto.

### Pasos

Puede omitir este paso si ya tiene una instancia de base de datos de PostGreSQL disponible a su disposición.

- Crea un archivo sql llamado `init.sql` con el contenido siguiente:

```sql
CREATE TABLE SI NO EXISTS sessions_map(
    session_ids varchar(256),
    texto session_caps,
    session_uri varchar(256),
    texto session_stereotype
    session_start varchar(256)

```

- En el mismo directorio que el `init.sql`, crea un archivo llamado `docker-compose.yml` con su contenido a continuación:

```yaml
version: '3.8'
servicios:
  db:
    image: postgres:9. -bullseye
    reiniciar: always
    environment:
      - POSTGRES_USER=seluser
      - POSTGRES_PASSWORD=seluser
      - POSTGRES_DB=selenium_sessions
    puertos:
      - "5432:5432"
    volumes:
    - . init.sql:/docker-entrypoint-initdb.d/init.sql
```

Ahora podemos iniciar nuestro contenedor de base de datos ejecutando:

```bash
docker-compose arriba -d
```

_Nuestro nombre de base de datos es `selenium_sessions` con su nombre de usuario y contraseña establecidos a `seluser`_

Si está trabajando con una instancia de PostGreSQL DB en ejecución, entonces sólo necesita crear una base de datos llamada `selenium_sessions` y la tabla `sessions_map` usando la mencionada sentencia SQL.

- Crea un archivo de configuración Selenium Grid llamado `sessions.toml` con el contenido siguiente:

```toml
[sessions]
implementation = "org.openqa.selenium.grid.sessionmap.jdbc.JdbcBackedSessionMap"
jdbc-url = "jdbc:postgresql://localhost:5432/selenium_sessions"
jdbc-user = "seluser"
jdbc-password = "seluser"
```

_Nota:_ Si planeas usar una instancia existente de PostGreSQL DB, entonces reemplaza `localhost:5432` con el host actual y el número de puerto de tu instancia.

- A continuación hay un script de shell simple (llamémoslo `distributed.sh`) que usaremos para abrir nuestra cuadrícula distribuida.

```bash
SE_VERSION=<current_selenium_version>
JAR_NAME=selenium-server-${SE_VERSION}. ar
PUBLISH="--publish-events tcp://localhost:4442"
SUBSCRIBE="--subscribe-events tcp://localhost:4443"
SESSIONS="--sessions http://localhost:5556"
SESSIONS_QUEUE="--sessionqueue http://localhost:5559"
echo 'Empezar bus de eventos'
java -jar $JAR_NAME event-bus $PUBLISH $SUBSCRIBE --port 5557 &
echo 'Comenzando Nueva Quita de sesión'
java -jar $JAR_NAME sessionqueue --port 5559 &
echo 'Iniciar Sesiones Map'
java -jar $JAR_NAME \
--ext $ eleniumhq.selenium:selenium-session-map-jdbc:${SE_VERSION} org.postgresql:postgresql:42.3.1) \
sesiones $PUBLISH $SUBSCRIBE --port 5556 --config sessions. oml &
echo 'Starting Distributor'
java -jar $JAR_NAME  distribuidor $PUBLISH $SUBSCRIBE $SESSIONS $SESSIONS_QUEUE --port 5553 --bind-bus false &
echo 'Starting Router'
java -jar $JAR_NAME router $SESSIONS --distributor http://localhost:5553 $SESSIONS_QUEUE --port 4444 &
echo 'Starting Node'
java -jar $JAR_NAME node $PUBLISH $SUBSCRIBE&
```

- En este punto, el directorio actual debe contener los siguientes archivos:
 - `docker-compose.yml`
 - `init.sql`
 - `sessions.toml`
 - `distributed.sh`

- Ahora puedes generar la cuadrícula ejecutando el script de shell `distributed.sh` y ejecutando rápidamente una prueba. Notará que la cuadrícula almacena ahora información de sesión en la base de datos PostGreSQL.

En la línea que genera un `SessionMap` en una máquina:

```bash
export SE_VERSION=<current_selenium_version>
java -jar selenium-server-${SE_VERSION}.jar \
--ext $(coursier fetch -p org.seleniumhq.selenium:selenium-session-map-jdbc:${SE_VERSION} org. ostgresql:postgresql:42.3.1) \
sesiones --publish-events tcp://localhost:4442 \
--subscribe-events tcp://localhost:4443 \
--port 5556 --config sessions.toml 
```

- Los nombres de variables del script anterior han sido reemplazados por sus valores reales para la claridad.
- Recuerda sustituir `localhost` por el nombre de host real de la máquina donde se está ejecutando tu `Event-Bus`.
- Los argumentos que se pasan a `coursier` son básicamente la GAV (Group Artifact Version) coordenadas de Maven de:
 - [selenium-session-map-jdbc](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-session-map-jdbc) which is needed to help us store sessions information in database
 - [postgresql](https://mvnrepository.com/artifact/org.postgresql/postgresql) que es necesario para ayudarnos a hablar sobre la base de datos PostGreSQL.
- `sessions.toml` es el archivo de configuración que creamos anteriormente.

## Mapa de sesiones respaldado por Redis

Nos desviaremos de un contenedor docker de caché de Redis usando un archivo docker compuesto.

### Pasos

Puedes omitir este paso si ya tienes una instancia de caché de Redis disponible a tu disposición.

- Crea un archivo llamado `docker-compose.yml` con su contenido a continuación:

```yaml
version: '3.8'
servicios:
  redis:
    image: redis:bullseye
    reiniciar: siempre
    puertos:
      - "6379:6379"
```

Ahora podemos iniciar nuestro contenedor Redis ejecutando:

```bash
docker-compose arriba -d
```

- Crea un archivo de configuración Selenium Grid llamado `sessions.toml` con el contenido siguiente:

```toml
[sessions]
scheme = "redis"
implementation = "org.openqa.selenium.grid.sessionmap.redis.RedisBackedSessionMap"
hostname = "localhost"
port = 6379
```

_Nota:_ Si planeas usar una instancia de caché de Redis existente, luego reemplaza `localhost` y `6379` con el número de host y puerto de tu instancia.

- A continuación hay un script de shell simple (llamémoslo `distributed.sh`) que usaremos para abrir nuestra cuadrícula distribuida.

```bash
SE_VERSION=<current_selenium_version>
JAR_NAME=selenium-server-${SE_VERSION}.jar
PUBLISH="--publish-events tcp://localhost:4442"
SUBSCRIBE="--subscribe-events tcp://localhost:4443"
SESSIONS="--sessions http://localhost:5556"
SESSIONS_QUEUE="--sessionqueue http://localhost:5559"
echo 'Starting Event Bus'
java -jar $JAR_NAME event-bus $PUBLISH $SUBSCRIBE --port 5557 &
echo 'Starting New Session Queue'
java -jar $JAR_NAME sessionqueue --port 5559 &
echo 'Starting Session Map'
java -jar $JAR_NAME \
--ext $(coursier fetch -p org.seleniumhq.selenium:selenium-session-map-redis:${SE_VERSION}) \
sessions $PUBLISH $SUBSCRIBE --port 5556 --config sessions.toml &
echo 'Starting Distributor'
java -jar $JAR_NAME  distributor $PUBLISH $SUBSCRIBE $SESSIONS $SESSIONS_QUEUE --port 5553 --bind-bus false &
echo 'Starting Router'
java -jar $JAR_NAME router $SESSIONS --distributor http://localhost:5553 $SESSIONS_QUEUE --port 4444 &
echo 'Starting Node'
java -jar $JAR_NAME node $PUBLISH $SUBSCRIBE &
```

- En este punto, el directorio actual debe contener los siguientes archivos:
 - `docker-compose.yml`
 - `sessions.toml`
 - `distributed.sh`

- Ahora puedes generar la cuadrícula ejecutando el script de shell `distributed.sh` y ejecutando rápidamente una prueba. Notará que la cuadrícula almacena ahora información de sesión en la instancia de Redis. Puede usar un GUI Redis como [TablePlus](https://tableplus.com/) para verlos (Asegúrate de que has configurado un punto de depuración en tu prueba, porque los valores se eliminarán tan pronto como la prueba se ejecute para finalizar).

En la línea que genera un `SessionMap` en una máquina:

```bash
export SE_VERSION=<current_selenium_version>
java -jar selenium-server-${SE_VERSION}.jar \
--ext $(coursier fetch -p org.seleniumhq. elenium:selenium-session-map-redis:${SE_VERSION}) \
sessions --publish-events tcp://localhost:4442 \
--subscribe-events tcp://localhost:4443 \
--port 5556 --config sessions.toml 
```

- Los nombres de variables del script anterior han sido reemplazados por sus valores reales para la claridad.
- Recuerda sustituir `localhost` por el nombre de host real de la máquina donde se está ejecutando tu `Event-Bus`.
- Los argumentos que se pasan a `coursier` son básicamente la GAV (Group Artifact Version) coordenadas de Maven de:
 - [selenium-session-map-redis](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-session-map-redis) which is needed to help us store sessions information in Redis Cache.
- `sessions.toml` es el archivo de configuración que creamos anteriormente.

