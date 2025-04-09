---
title: Herramienta de Build Buck
linkTitle: Pato
weight: 4
description: |
  Buck es una herramienta de construcción de Facebook con la que estábamos trabajando para reemplazar a Crazy fun. Lo hemos sustituido por [Bazel](https://bazel.build/).
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Buck) \
Puedes leer la documentación de la [Herramienta de Construcción Loco Fun]({{< ref "crazy_fun_build. d" >}}).

## Construyendo Selenium con Pato

Lo más fácil de hacer es ejecutar "./go". El proceso de compilación descargará la versión correcta de Buck para ti siempre y cuando no haya un archivo `.nobuckcheck` en la raíz del proyecto. La descarga termina en `buck-out/crazy-fun/HASH/buck. ex` donde `HASH` es el valor de la versión actual del paquete (dada en el archivo `.buckversion` en la raíz del proyecto.

Si quieres construir y ejecutar nuestro fork de Buck, entonces:

```
git clone https://github.com/SeleniumHQ/buck. it
cd buck && ant
export PATH=`pwd`/bin:$PATH
cd ~/src/selenium 
buck build chrome firefox htmlunit remote leg-rc
buck test --all
```

## Actualizando el `buck.pex`

Si necesita actualizar la versión de Buck que se ha descargado:

- Echa un vistazo al código fuente de Buck y construye el PEX: `buck build --show-output buck`
- Figura el hash git de la versión que acabas de construir. Normalmente eso será el CABO del maestro. Ponga ese hash completo en el `.buckversion` del proyecto principal de selenio.
- Ponga el hash md5 del PEX en el archivo `.buckhash` en el proyecto principal de selenium.
- Crear una nueva versión de SeleniumHQ Buck fork en GitHub. El nombre es `buck-release-$VERSION`, donde $VERSION es lo que esté en `.buckversion` en el proyecto principal de selenium.
- Sube el PEX a la versión, y haz pública la liberación.
- Comprometer los cambios en el proyecto principal de selenium y empujarlos.
