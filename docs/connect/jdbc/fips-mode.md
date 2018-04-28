---
title: El modo FIPS | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.workload: Inactive
ms.openlocfilehash: bc357dc09c8357db8c9a5de24d6644029f31dd14
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="fips-mode"></a>Modo FIPS
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El controlador JDBC de Microsoft para SQL Server admite *el modo compatible con FIPS 140*. Para Oracle / Sun JVM, hacen referencia a la [FIPS 140 modo compatible para SunJSSE](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) sección suministrado por Oracle para configurar FIPS habilitada JVM. 

**Requisitos previos**:
* FIPS configurado JVM
* Certificado SSL correspondiente.
* Archivos de directivas apropiados. 
* Parámetros de configuración adecuado. 


## <a name="fips-configured-jvm"></a>FIPS configurado JVM

Para ver los módulos aprobados para la configuración de FIPS, consulte el [validar FIPS 140-1 y los módulos criptográficos de FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm). 

Los proveedores pueden tener algunos pasos adicionales para configurar la JVM con FIPS.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>Asegúrese de que su JVM está en modo FIPS
Con el fin de garantizar que la JVM es FIPS habilitada, ejecute el siguiente fragmento: 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>Certificado SSL adecuada
Para conectar SQL Server en el modo FIPS, se requiere un certificado SSL válido. Instalar o importar en el almacén de claves de Java en el equipo cliente (JVM) donde está habilitada la FIPS. Si no importar o instalar el certificado adecuado, podría no podrá conectarse a SQL Server ya no se puede realizar una conexión segura.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importar el certificado SSL en el almacén de claves de Java
Para FIPS, más probable es que debe importar el certificado (.cert) a cualquier PKCS o en un formato específico del proveedor. Utilice el siguiente fragmento de código para importar el certificado SSL y almacenarlo en un directorio de trabajo con el formato de almacén de claves adecuado. _TRUST_STORE_PASSWORD_ es la contraseña para el almacén de claves de Java. 

````
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

````


En el ejemplo siguiente se importa un certificado SSL de Azure en formato PKCS12 con BouncyCastle proveedor. El certificado se importa en el directorio de trabajo denominado _MyTrustStore_PKCS12_ utilizando el siguiente fragmento:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>Archivos de directiva apropiada
Algunos proveedores de FIPS, se necesita JAR sin restricciones de directiva. En tales casos, para Sun / Oracle, descargar los Java Cryptography Extension (JCE) Unlimited intensidad jurisdicción archivos de directivas para [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parámetros de configuración adecuado
Para ejecutar el controlador JDBC en modo compatible con FIPS, configurar propiedades de conexión tal y como se muestra en la tabla siguiente. 

**Propiedades de**: 

|Propiedad|Tipo|Predeterminado|Description|Notas|
|---|---|---|---|---|
|encrypt|valor booleano ["true / false"]|"false"|Si está habilitado el FIPS JVM cifrar propiedad debe ser **true**||
|TrustServerCertificate|valor booleano ["true / false"]|"false"|Para FIPS, el usuario debe validar la cadena de certificados, por lo que el usuario debe utilizar **"false"** valor de esta propiedad. ||
|trustStore|String|null|La ruta de acceso de archivo de almacén de claves de Java que importó el certificado. Si se instala el certificado en el sistema, entonces no es necesario pasar nada. Controlador utiliza cacerts o jssecacerts archivos.||
|trustStorePassword|String|null|Contraseña que se usa para comprobar la integridad de los datos trustStore.||
|FIPS|valor booleano ["true / false"]|"false"|Para fips habilitado JVM esta propiedad debe ser **true**|Agregado en 6.1.4 (estable versión 6.2.2)||
|fipsProvider|String|null|Proveedor FIPS configurado en JVM. Por ejemplo, BCFIPS o SunPKCS11-NSS |Agregado en 6.1.2 (estable versión 6.2.2), en desuso en 6.4.0 - ver los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|ALMACÉN JKS|Para el tipo de almacén de confianza de certificados mediante FIPS modo conjunto PKCS12 o tipo definido por proveedor FIPS |Agregado en 6.1.2 (estable versión 6.2.2)||



  
