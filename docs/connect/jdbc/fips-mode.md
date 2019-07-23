---
title: Modo FIPS en JDBC | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 482e820d17860b67f46d47f4bb8523e833d0cf5a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252212"
---
# <a name="fips-mode"></a>Modo FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC driver for SQL Server admite la ejecución en JVM configurado para que sea *compatible con FIPS 140*.

#### <a name="prerequisites"></a>Prerequisites

- JVM configurado por FIPS
- Certificado SSL adecuado
- Archivos de directivas adecuados
- Parámetros de configuración adecuados

## <a name="fips-configured-jvm"></a>JVM configurado por FIPS

Por lo general, las aplicaciones `java.security` pueden configurar el archivo para usar los proveedores de cifrado compatibles con FIPS. Consulte la documentación específica de la JVM para saber cómo configurar la compatibilidad con FIPS 140.

Para ver los módulos aprobados para la configuración de FIPS, consulte [los módulos validados en el programa de validación de módulos criptográficos](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

Los proveedores pueden tener algunos pasos adicionales para configurar una JVM con FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificado SSL adecuado
Para conectarse a SQL Server en modo FIPS, se requiere un certificado SSL válido. Instálelo en el almacén de claves de Java en el equipo cliente (JVM), donde está habilitado FIPS.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importación de un certificado SSL en Java KeyStore
En el caso de FIPS, lo más probable es que necesite importar el certificado (. CERT) en PKCS o en un formato específico del proveedor.
Use el siguiente fragmento de código para importar el certificado SSL y almacenarlo en un directorio de trabajo con el formato de almacén de claves adecuado. _La\_contraseña\_del almacén de confianza_ es su contraseña para Java keystore.

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

En el ejemplo siguiente se importa un certificado SSL de Azure en formato PKCS12 con el proveedor BouncyCastle. El certificado se importa en el directorio de trabajo _denominado\_MyTrustStore PKCS12_ mediante el siguiente fragmento de código:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>Archivos de directivas adecuados
En algunos proveedores de FIPS, se necesitan jar de directiva sin restricciones. En tales casos, para Sun/Oracle, descargue los archivos de directivas de la extensión de criptografía de Java (JCE) sin límite de seguridad para [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parámetros de configuración adecuados
Para ejecutar el controlador JDBC en modo compatible con FIPS, configure las propiedades de conexión como se muestra en la tabla siguiente. 

#### <a name="properties"></a>Propiedades 

|Propiedad|Tipo|Valor predeterminado|Descripción|Notas|
|---|---|---|---|---|
|encrypt|booleano ["true / false"]|"false"|Para la propiedad de cifrado JVM habilitada para FIPS debe ser **true**||
|TrustServerCertificate|booleano ["true / false"]|"false"|En el caso de FIPS, el usuario debe validar la cadena de certificados, por lo que el usuario debe usar el valor **"false"** para esta propiedad. ||
|trustStore|String|null|La ruta de acceso del archivo de almacén de claves de Java donde importó el certificado. Si instala un certificado en el sistema, no es necesario pasar nada. El controlador usa archivos cacerts o jssecacerts.||
|trustStorePassword|String|null|Contraseña que se usa para comprobar la integridad de los datos trustStore.||
|fips|booleano ["true / false"]|"false"|Para JVM habilitado para FIPS, esta propiedad debe ser **true** .|Agregado en 6.1.4 (versión de lanzamiento estable)||
|fipsProvider|String|null|Proveedor FIPS configurado en JVM. Por ejemplo, BCFIPS o SunPKCS11-NSS |Agregado en 6.1.2 (versión de lanzamiento estable), en desuso en 6.4.0. Consulte los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|JKS|En modo FIPS, establezca el tipo de almacén de confianza PKCS12 o tipo definido por el proveedor de FIPS |Agregado en 6.1.2 (versión de lanzamiento estable)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
