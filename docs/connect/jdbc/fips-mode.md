---
title: El modo FIPS | Documentos de Microsoft
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f344ad84588110372ccb369ae97642ef6c42f07
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="fips-mode"></a>Modo FIPS
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El controlador JDBC de Microsoft para SQL Server admite *el modo compatible con FIPS 140*. Para Oracle / Sun JVM, hacen referencia a la [FIPS 140 modo compatible para SunJSSE](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) sección suministrado por Oracle para configurar FIPS habilitada JVM. 

**Requisitos previos**:
* FIPS configurado JVM
* Certificado SSL correspondiente.
* Archivos de directivas apropiados. 
* Parámetros de configuración adecuado. 


## <a name="fips-configured-jvm"></a>FIPS había configurado JVM:

Para ver los módulos aprobados para la configuración de FIPS, consulte el [validar FIPS 140-1 y los módulos criptográficos de FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm). 

Los proveedores pueden tener algunos pasos adicionales para configurar la JVM con FIPS.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>Compruebe que la JVM se encuentra en el modo FIPS:
Con el fin de garantizar que la JVM es FIPS habilitada, ejecute el siguiente fragmento: 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>Certificado SSL adecuado:
Para conectar SQL Server en el modo FIPS, se requiere un certificado SSL válido. Instalar o importar en el almacén de claves de Java en el equipo cliente (JVM) donde está habilitada la FIPS. Si no importar o instalar el certificado adecuado, podría no podrá conectarse a SQL Server ya no se puede realizar una conexión segura.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importar el certificado SSL en el almacén de claves de Java:
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


En el siguiente ejemplo, estamos importando un certificado SSL de Azure en formato PKCS12 con BouncyCastle proveedor. El certificado se importa en el directorio de trabajo denominado _MyTrustStore_PKCS12_ utilizando el siguiente fragmento:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>Archivos de directivas apropiada: 
Algunos proveedores de FIPS, se necesita JAR sin restricciones de directiva. En tales casos, para Sun / Oracle, descargar los Java Cryptography Extension (JCE) Unlimited intensidad jurisdicción archivos de directivas para [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parámetros de configuración adecuada: 
Para ejecutar el controlador JDBC en modo compatible con FIPS, configurar propiedades de conexión tal y como se muestra en la tabla siguiente. 

**Propiedades de**: 

|Propiedad|Tipo|Predeterminado|Description|Notas|
|---|---|---|---|---|
|encrypt|valor booleano ["true / false"]|"false"|Si está habilitado el FIPS JVM cifrar propiedad debe ser **true**||
|TrustServerCertificate|valor booleano ["true / false"]|"false"|Para FIPS es necesario para validar la cadena de certificados, por lo que debemos usar **"false"** valor de esta propiedad. ||
|trustStore|String|null|La ruta de acceso de archivo de almacén de claves de Java que importó el certificado. Si se instala el certificado en el sistema, entonces no es necesario pasar nada. Controlador utiliza cacerts o jssecacerts archivos.||
|trustStorePassword|String|null|Contraseña que se usa para comprobar la integridad de los datos trustStore.||
|FIPS|valor booleano ["true / false"]|"false"|Para fips habilitado JVM esta propiedad debe ser **true**|6.1.4 agregado en||
|fipsProvider|String|null|Proveedor FIPS configurado en JVM. Por ejemplo, BCFIPS o SunPKCS11-NSS |6.1.2 agregado en|
|trustStoreType|String|ALMACÉN JKS|Para el tipo de almacén de confianza de certificados mediante FIPS modo conjunto PKCS12 o tipo definido por proveedor FIPS |6.1.2 agregado en||



  
