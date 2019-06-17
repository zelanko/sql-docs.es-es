---
title: El modo FIPS en JDBC | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: craigg
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: kenvh
ms.openlocfilehash: d710bb6e83d6f9761f7926afac3280a2c33d2bec
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822232"
---
# <a name="fips-mode"></a>Modo FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver para SQL Server es compatible con el que se ejecuta en JVM configurado para ser *compatible con FIPS 140*.

#### <a name="prerequisites"></a>Prerequisites

- FIPS configurado JVM
- Certificado SSL correspondiente
- Archivos de directiva apropiada
- Parámetros de configuración adecuado

## <a name="fips-configured-jvm"></a>FIPS configurado JVM

Por lo general, las aplicaciones pueden configurar el `java.security` archivo utilizar proveedores de criptografía compatibles con FIPS. Consulte la documentación específica de la máquina virtual de Java para la configuración de cumplimiento de FIPS 140.

Para ver los módulos aprobados para la configuración de FIPS, consulte [módulos validados en el programa de validación del módulo criptográfico](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

Los proveedores pueden tener algunos pasos adicionales para configurar una JVM con FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificado SSL correspondiente
Para conectarse a SQL Server en el modo FIPS, se requiere un certificado SSL válido. Instalar o importarlo en el Store de clave de Java en el equipo cliente (JVM) que FIPS está habilitado.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importar el certificado SSL en el almacén de claves de Java
Para FIPS, probablemente deberá importar el certificado (.cert) en un formato específico del proveedor o PKCS.
Use el siguiente fragmento de código para importar el certificado SSL y almacenarla en un directorio de trabajo con el formato de almacén de claves adecuado. _CONFIANZA\_almacén\_contraseña_ es la contraseña para el almacén de claves de Java.

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

El ejemplo siguiente se importa un certificado SSL de Azure en formato PKCS12 con el proveedor BouncyCastle. El certificado se importa en el directorio de trabajo denominado _MyTrustStore\_PKCS12_ mediante el siguiente fragmento:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>Archivos de directiva apropiada
Algunos proveedores de FIPS, se necesita archivos JAR de directiva sin restricciones. En tales casos, de Sun / Oracle, descargue el Java Cryptography Extension (JCE) Unlimited intensidad jurisdicción archivos de directiva de [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parámetros de configuración adecuado
Para ejecutar el controlador JDBC en modo compatible con FIPS, configure las propiedades de conexión como se muestra en la tabla siguiente. 

#### <a name="properties"></a>Propiedades 

|Propiedad|Tipo|Valor predeterminado|Descripción|Notas|
|---|---|---|---|---|
|encrypt|booleano ["true / false"]|"false"|Para habilitar FIPS JVM cifrar la propiedad debe ser **true**||
|TrustServerCertificate|booleano ["true / false"]|"false"|Para FIPS, el usuario debe validar la cadena de certificados, por lo que el usuario debe usar **"false"** valor para esta propiedad. ||
|trustStore|String|null|La ruta de acceso de archivo de Java Keystore donde se ha importado el certificado. Si se instala el certificado en el sistema y, a continuación, no es necesario pasarle cualquier cosa. Controlador utiliza cacerts o jssecacerts archivos.||
|trustStorePassword|String|null|Contraseña que se usa para comprobar la integridad de los datos trustStore.||
|fips|booleano ["true / false"]|"false"|Para FIPS JVM habilitada esta propiedad debe ser **true**|Agregado en 6.1.4 (estable versión 6.2.2)||
|fipsProvider|String|null|Proveedor FIPS configurado en JVM. Por ejemplo, BCFIPS o SunPKCS11 NSS |Agregado en 6.1.2 (estable versión 6.2.2), en desuso en 6.4.0 - ver los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|JKS|Para FIPS establece el modo tipo de almacén de confianza PKCS12 o tipo definido por el proveedor FIPS |Agregado en 6.1.2 (estable versión 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
