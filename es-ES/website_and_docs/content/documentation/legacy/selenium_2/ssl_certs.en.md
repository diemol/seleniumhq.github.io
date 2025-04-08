---
title: Certificados SSL no confiables
linkTitle: Certificados SSL
weight: 12
description: |
  Detalles sobre cómo Selenium 2 aceptó certificados SSL no confiables
---

Esta documentación previamente ubicada [en la wiki](https://github.com/SeleniumHQ/selenium/wiki/Untrusted-SSL-Certificates)

## Introducción

Esta página detalla cómo WebDriver es capaz de aceptar certificados SSL no confiables, permitiendo a los usuarios probar sitios de confianza en un entorno de prueba, donde los certificados válidos generalmente no existen. Esta función está activada por defecto para todos los navegadores compatibles (actualmente Firefox).

## Firefox

### Fuera de la solución

Firefox tiene una interfaz para reemplazar certificados no válidos, llamada nsICertOverrideService. Implementar esta interfaz como un proxy al servicio original - **a menos que** certificados no confiables están permitidos. En ese caso, cuando se le pregunte por un certificado (una llamada a hasMatchingOverride para un certificado no válido) - indique que es de confianza.

### Detalles de implementación

Implementar la idea es más sencillo - badCertListener.js es un módulo independiente que, al cargar, registra una fábrica para devolver una instancia del servicio. La función interesante es hasMatchingOverride:

```
WdCertOverrideService.prototype.hasMatchingOverride = function(
    aHostName, aPort, aCert, aOverrideBits, aIsTemporary)
```

Los aOverrideBits y aIsTemporary son argumentos de salida. Aquí es donde las cosas se vuelven un poco complicadas:
Hay tres posibles bits de anulación:

```
  ERROR_UNTRUSTED: 1,
  ERROR_MISMATCH: 2,
  ERROR_TIME: 4
```

Es imposible ponerlos a todos, ya que Firefox espera una coincidencia perfecta entre los delitos generados por el certificado y el valor de retorno de la función: (security/manager/ssl/src/SSLServerCertVerification. p:302):

```
  if (overrideService)
  {
    PRBool haveOverride;
    PRBool isTemporaryOverride; // no nos importa
  
    nsrv = overrideService->HasMatchingOverride(hostString, puerto,
                                                ix509, 
                                                sobrescribir,
                                                &isTemporaryOverride, 
                                                &haveoverride);
    if (NS_SUCCEEDED(nsrv) && haveOverride) 
    {
      // elimina los errores que ya están sobreescritos
      remaining_display_errors -= overrideBits;
    }
  }

  if (! emaining_display_errors) {
    // todos los errores están cubiertos por reglas de anulación, así que vamos a aceptar el cert
    return SECSuccess;
}
```

El mapeo exacto de violación al código de error se puede ver fácilmente en security/manager/pki/resources/content/exceptionDialog.js (en la fuente de Firefox):

```
  var flags = 0;
  if(gSSLStatus.isUntrusted)
    flags |= overrideService.ERROR_UNTRUSTED;
  if(gSSLStatus.isDomainMismatch)
    flags |= overrideService.ERROR_MISMATCH;
  if(gSSLStatus.isNotValidAtThisTime)
    flags |= overrideService.ERROR_TIME;
```

El estado SSL se puede obtener de `"@mozilla. rg/security/recentbadcerts; "` normalmente - Sin embargo, el certificado (y su estado) se añaden a este servicio sólo **después** de la llamada a `hasMatchingOverride`, así que no hay una forma fácil de averiguar el SSLStatus del certificado. En su lugar, las comprobaciones deben ejecutarse manualmente.

Se llevan a cabo dos controles:

- Calling `nsIX509Cert.verifyForUsage`
- Comparando hostname con `nsIX509Cert.commonName`. Si estos no son iguales, `ERROR_MISMATCH` está establecido.

La segunda comprobación indica si debe establecerse `ERROR_MISMATCH`.
La primera comprobación debe indicar si deben establecerse `ERROR_UNTRUSTED` y `ERROR_TIME`. Desafortunadamente, no funciona de forma fiable cuando el certificado caducó **y** es de un emisor no confiable. Cuando el certificado ha caducado, el código de retorno sería `CERT_EXPIRED` incluso si no es fiable. Por esta razón, el FirefoxDriver asume que los certificados no serán confiados - **siempre** establece el bit `ERROR_UNTRUSTED` - los otros dos se establecerán sólo si se cumplen las condiciones para ellos.

Esto podría plantear un problema para alguien que esté probando un sitio con un certificado válido que no coincida con el nombre de host desde el que se sirve (e. , pruebe el entorno que sirve certificados de producción). Se añadió una característica adicional para `FirefoxProfile`: `FirefoxProfile.setAssumeUntrustedCertificateIssuer`. Llamar a esta función con `false` desactivará el bit `ERROR_UNTRUSTED` y permitirá a un usuario trabajar en tal situación.

## HTMLUnit

Aún no se ha probado.

## IE

Aún no implementado.

## Chromo

Aún no implementado.
