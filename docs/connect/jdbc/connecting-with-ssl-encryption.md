---
title: Conectar con el cifrado SSL | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14f33ac9e6ab8d17954039f4ae0fca1f11e46af5
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737136"
---
# <a name="connecting-with-ssl-encryption"></a>Conectar con el cifrado SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En los ejemplos de este artículo se describe cómo usar propiedades de cadena de conexión que permiten a las aplicaciones usar el cifrado de Capa de sockets seguros (SSL) en una aplicación Java. Para más información sobre estas nuevas propiedades de cadena de conexión, como **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** y **hostNameInCertificate**, vea [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Cuando la propiedad **encrypt** se establece en **true** y la propiedad **trustServerCertificate** se establece en **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no validará el certificado SSL de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto suele ser necesario para permitir conexiones en entornos de prueba, por ejemplo, cuando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo tiene un certificado autofirmado.  
  
 En el ejemplo de código siguiente se muestra cómo establecer la propiedad **trustServerCertificate** en una cadena de conexión:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Cuando la propiedad **encrypt** se establece en **true** y la propiedad **trustServerCertificate** se establece en **false**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] validará el certificado SSL de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para validar el certificado de servidor, se debe suministrar material de confianza en el momento de la conexión, ya sea mediante el uso explícito de las propiedades de conexión **trustStore** y **trustStorePassword**, o mediante el uso implícito del almacén de confianza predeterminado de la máquina virtual Java (JVM) subyacente.  
  
 La propiedad **trustStore** especifica la ruta de acceso (incluido el nombre de archivo) del archivo trustStore de certificado, que contiene la lista de certificados en los que el cliente confía. La propiedad **trustStorePassword** especifica la contraseña que se usa para comprobar la integridad de los datos de trustStore. Para obtener más información sobre el uso de almacén de confianza predeterminado de JVM, vea el [configuración del cliente para el cifrado SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
 En el ejemplo de código siguiente se muestra cómo establecer las propiedades **trustStore** y **trustStorePassword** en una cadena de conexión:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC Driver proporciona una propiedad adicional, **hostNameInCertificate**, que especifica el nombre de host del servidor. El valor de esta propiedad debe coincidir con la propiedad de asunto del certificado.  
  
 En el ejemplo de código siguiente se muestra cómo usar la propiedad **hostNameInCertificate** en una cadena de conexión:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  También puede establecer el valor de las propiedades de conexión mediante los métodos **establecedores** adecuados que proporciona la clase [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Si el **cifrar** propiedad está establecida en **true** y **trustServerCertificate** propiedad está establecida en **false** y si el nombre de servidor en el cadena de conexión no coincide con el nombre del servidor en el certificado SSL, se emitirá el siguiente error: `The driver couldn't establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "java.security.cert.CertificateException: Failed to validate the server name in a certificate during Secure Sockets Layer (SSL) initialization."`. A partir de la versión 7.2, el controlador admite caracteres comodín de coincidencia en la etiqueta más a la izquierda del nombre del servidor en el certificado SSL.
## <a name="see-also"></a>Consulte también  
 [Usar el cifrado SSL](../../connect/jdbc/using-ssl-encryption.md)   
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
