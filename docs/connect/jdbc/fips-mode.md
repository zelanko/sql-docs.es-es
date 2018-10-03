---
title: El modo FIPS | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.openlocfilehash: cc13455e6f56950d6988909b53aa7664c7fd77f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723833"
---
# <a name="fips-mode"></a>Modo FIPS
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver para SQL Server admite *el modo compatible con FIPS 140*. Para Oracle / Sun JVM, consulte el [140 el modo compatible con FIPS para SunJSSE](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) sección suministrado por Oracle para configurar FIPS JVM habilitada. 

**Requisitos previos**:
* FIPS configurado JVM
* Certificado SSL correspondiente.
* Archivos de la directiva adecuada. 
* Parámetros de configuración adecuado. 


## <a name="fips-configured-jvm"></a>FIPS configurado JVM

Para ver los módulos aprobados para la configuración de FIPS, consulte el [validados de FIPS 140-1 y los módulos criptográficos de FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm). 

Los proveedores pueden tener algunos pasos adicionales para configurar la JVM con FIPS.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>Asegúrese de que máquina virtual de Java está en modo FIPS
Para asegurar la que máquina virtual de Java está habilitado para FIPS, ejecute el siguiente fragmento de código: 

```java
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
```

## <a name="appropriate-ssl-certificate"></a>Certificado SSL correspondiente
Para conectar SQL Server en el modo FIPS, se requiere un certificado SSL válido. Instalar o importarlo en el Store de clave de Java en el equipo cliente (JVM) que FIPS está habilitado.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importar el certificado SSL en el almacén de claves de Java
Para FIPS, probablemente deberá importar el certificado (.cert) a cualquier PKCS o en un formato específico del proveedor. Use el siguiente fragmento de código para importar el certificado SSL y almacenarla en un directorio de trabajo con el formato de almacén de claves adecuado. _TRUST_STORE_PASSWORD_ es la contraseña para el almacén de claves de Java. 

```java
    public void saveGenericKeyStore(String provider, String trustStoreType, String certName, String certPath) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, NoSuchProviderException, IOException {
        KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
        FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
        ks.load(null, null);
        ks.setCertificateEntry(certName, getCertificate(certPath));
        ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
        os.flush();
        os.close();
    }

    private Certificate getCertificate(String pathName) throws FileNotFoundException, CertificateException {
        FileInputStream fis = new FileInputStream(pathName);
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        return cf.generateCertificate(fis);
    }

```


El ejemplo siguiente se importa un certificado SSL de Azure en formato PKCS12 con BouncyCastle proveedor. El certificado se importa en el directorio de trabajo denominado _MyTrustStore_PKCS12_ mediante el siguiente fragmento:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>Archivos de directiva apropiada
Algunos proveedores de FIPS, se necesita archivos JAR de directiva sin restricciones. En tales casos, de Sun / Oracle, descargue el Java Cryptography Extension (JCE) Unlimited intensidad jurisdicción archivos de directiva de [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parámetros de configuración adecuado
Para ejecutar el controlador JDBC en modo compatible con FIPS, configure las propiedades de conexión como se muestra en la tabla siguiente. 

**Propiedades**: 

|Propiedad|Tipo|Valor predeterminado|Descripción|Notas|
|---|---|---|---|---|
|encrypt|booleano ["true / false"]|"false"|Para habilitar FIPS JVM cifrar la propiedad debe ser **true**||
|TrustServerCertificate|booleano ["true / false"]|"false"|Para FIPS, el usuario debe validar la cadena de certificados, por lo que el usuario debe usar **"false"** valor para esta propiedad. ||
|trustStore|String|null|La ruta de acceso de archivo de Java Keystore donde se ha importado el certificado. Si se instala el certificado en el sistema y, a continuación, no es necesario pasarle cualquier cosa. Controlador utiliza cacerts o jssecacerts archivos.||
|trustStorePassword|String|null|Contraseña que se usa para comprobar la integridad de los datos trustStore.||
|fips|booleano ["true / false"]|"false"|Para FIPS JVM habilitada esta propiedad debe ser **true**|Agregado en 6.1.4 (estable versión 6.2.2)||
|fipsProvider|String|null|Proveedor FIPS configurado en JVM. Por ejemplo, BCFIPS o SunPKCS11 NSS |Agregado en 6.1.2 (estable versión 6.2.2), en desuso en 6.4.0 - ver los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|JKS|Para FIPS establece el modo tipo de almacén de confianza PKCS12 o tipo definido por el proveedor FIPS |Agregado en 6.1.2 (estable versión 6.2.2)||



  
