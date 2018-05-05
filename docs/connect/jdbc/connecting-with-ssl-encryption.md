---
title: Conectar con el cifrado SSL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49c6aaf771bb5335b8ba649869a4a8cf13894e82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-ssl-encryption"></a>Conectar con el cifrado SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Los ejemplos en este tema describen cómo utilizar propiedades de cadena de conexión que permiten a las aplicaciones utilizar el cifrado de Capa de sockets seguros (SSL) en una aplicación Java. Para obtener más información sobre estos nueva conexión de cadena como propiedades **cifrar**, **trustServerCertificate**, **trustStore**,  **trustStorePassword**, y **hostNameInCertificate**, consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Cuando el **cifrar** propiedad está establecida en **true** y **trustServerCertificate** propiedad está establecida en **true**, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no se validará el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL. Esto se suele ser necesario para permitir conexiones en entornos de prueba, como dónde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia tiene solo un certificado autofirmado.  
  
 En el ejemplo de código siguiente se muestra cómo establecer el **trustServerCertificate** propiedad en una cadena de conexión:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Cuando el **cifrar** propiedad está establecida en **true** y **trustServerCertificate** propiedad está establecida en **false**, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] validará el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para validar el certificado de servidor, se debe proporcionar material de confianza en tiempo de conexión mediante **trustStore** y **trustStorePassword** propiedades de conexión explícitamente, o mediante confianza predeterminado de la subyacente Máquina Virtual Java (JVM) del almacén de forma implícita.  
  
 El **trustStore** propiedad especifica la ruta de acceso (incluido el nombre de archivo) en el archivo trustStore del certificado, que contiene la lista de certificados que el cliente confíe. El **trustStorePassword** propiedad especifica la contraseña utilizada para comprobar la integridad de los datos trustStore. Para obtener más información sobre cómo usar el almacén de confianza predeterminado de JVM, vea el [configuración del cliente para el cifrado SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
 En el ejemplo de código siguiente se muestra cómo establecer el **trustStore** y **trustStorePassword** propiedades en una cadena de conexión:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 El controlador JDBC proporciona una propiedad adicional, **hostNameInCertificate**, que especifica el nombre de host del servidor. El valor de esta propiedad debe coincidir con la propiedad de asunto del certificado.  
  
 En el ejemplo de código siguiente se muestra cómo utilizar el **hostNameInCertificate** propiedad en una cadena de conexión:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  Como alternativa, puede establecer el valor de propiedades de conexión mediante el uso adecuado **establecedor** métodos proporcionados por el [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) clase.  
  
 Si el **cifrar** propiedad está establecida en **true** y **trustServerCertificate** propiedad está establecida en **false** y si el nombre de servidor en el cadena de conexión no coincide con el nombre del servidor en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] certificado SSL, se emitirá el siguiente error: el controlador no pudo establecer una conexión segura a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante el cifrado de capa de Sockets seguros (SSL). Error: "java.security.cert.CertificateException: No se pudo validar el nombre del servidor en un certificado durante la inicialización de SSL (Capa de sockets seguros)."  
  
## <a name="see-also"></a>Vea también  
 [Está utilizando cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
