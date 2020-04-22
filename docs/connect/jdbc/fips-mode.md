---
title: Modo FIPS en JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83ce3690d194b8b06fc79d58c2d7bc7efa996619
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293385"
---
# <a name="fips-mode"></a>Modo FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver para SQL Server admite la ejecución en JVM configuradas para ser *compatibles con FIPS 140*.

#### <a name="prerequisites"></a>Prerrequisitos

- JVM configurada por FIPS
- Certificado TLS/SSL adecuado
- Archivos de directivas adecuados
- Parámetros de configuración adecuados

## <a name="fips-configured-jvm"></a>JVM configurada por FIPS

En general, las aplicaciones pueden configurar el archivo `java.security` para usar proveedores criptográficos compatibles con FIPS. Consulte la documentación específica de su JVM para saber cómo configurar la compatibilidad con FIPS 140.

Para ver los módulos aprobados para la configuración de FIPS, consulte [Validated Modules in the Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules) (Módulos validados en el programa de validación del módulo criptográfico).

Los proveedores pueden contar con algunos pasos adicionales para configurar una JVM con FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificado SSL adecuado
Para conectarse a SQL Server en modo FIPS, es necesario un certificado TLS/SSL válido. Instálelo o impórtelo en el almacén de claves de Java de la máquina cliente (JVM) donde FIPS está habilitado.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importación del certificado SSL en el almacén de claves de Java
En el caso de FIPS, lo más probable es que tenga que importar el certificado (.cert) en PKCS o un formato específico del proveedor.
Use el siguiente fragmento para importar el certificado TLS/SSL y almacenarlo en un directorio de trabajo con el formato KeyStore. _TRUST\_STORE\_PASSWORD_ es su contraseña para el almacén de claves de Java.

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

En el ejemplo siguiente se importa un certificado TLS/SSL de Azure en formato PKCS12 con el proveedor BouncyCastle. El certificado se importa en el directorio de trabajo denominado _MyTrustStore\_PKCS12_ mediante el siguiente fragmento:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>Archivos de directivas adecuados
En el caso de algunos proveedores de FIPS, son necesarios archivos JAR de directivas sin restricciones. En estos casos,para Sun/Oracle, descargue los archivos de Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy para [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parámetros de configuración adecuados
Para ejecutar el controlador JDBC en modo compatible con FIPS, configure las propiedades de conexión como se muestra en la siguiente tabla. 

#### <a name="properties"></a>Propiedades 

|Propiedad|Tipo|Valor predeterminado|Descripción|Notas|
|---|---|---|---|---|
|encrypt|booleano ["true / false"]|"false"|En el caso de JVM habilitada para FIPS, la propiedad de cifrado debe ser **true**.||
|TrustServerCertificate|booleano ["true / false"]|"false"|En el caso de FIPS, el usuario debe validar la cadena de certificados, de modo que debe usar el valor **"false"** para esta propiedad. ||
|trustStore|String|null|La ruta de acceso del archivo del almacén de claves de Java donde importó su certificado. Si instala un certificado en el sistema, no es necesario pasar nada. El controlador usa archivos cacerts o jssecacerts.||
|trustStorePassword|String|null|Contraseña que se usa para comprobar la integridad de los datos trustStore.||
|fips|booleano ["true / false"]|"false"|En el caso de JVM habilitada para FIPS, esta propiedad debe ser **true**.|Se agrega en 6.1.4 (versión estable 6.2.2)||
|fipsProvider|String|null|Proveedor FIPS configurado en JVM. Por ejemplo, BCFIPS o SunPKCS11-NSS. |Se agrega en 6.1.2 (versión estable 6.2.2), en desuso en 6.4.0; consulte los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|JKS|En el caso del modo FIPS, establezca el tipo de almacén de confianza PKCS12 o el tipo definido por el proveedor FIPS. |Se agrega en 6.1.2 (versión estable 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
