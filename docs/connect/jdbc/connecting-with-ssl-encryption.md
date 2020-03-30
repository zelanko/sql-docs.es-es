---
title: Conexión con cifrado | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cff4228404690147d97a44f6f5dd43b1a180153c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "71713295"
---
# <a name="connecting-with-encryption"></a>Conexión con cifrado
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En los ejemplos de este artículo se describe cómo usar propiedades de cadena de conexión que permiten a las aplicaciones usar el cifrado de seguridad de la capa de transporte (TLS) en una aplicación Java. Para más información sobre estas nuevas propiedades de cadena de conexión, como **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** y **hostNameInCertificate**, vea [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Cuando la propiedad **encrypt** se establece en **true** y la propiedad **trustServerCertificate** se establece en **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no validará el certificado TLS de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto suele ser necesario para permitir conexiones en entornos de prueba, por ejemplo, cuando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo tiene un certificado autofirmado.  
  
 En el ejemplo de código siguiente se muestra cómo establecer la propiedad **trustServerCertificate** en una cadena de conexión:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Cuando la propiedad **encrypt** se establece en **true** y la propiedad **trustServerCertificate** se establece en **false**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] validará el certificado TLS de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Validar el certificado de servidor es una parte del protocolo de enlace de TLS y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para validar el certificado de servidor, se debe suministrar material de confianza en el momento de la conexión, ya sea mediante el uso explícito de las propiedades de conexión **trustStore** y **trustStorePassword**, o mediante el uso implícito del almacén de confianza predeterminado de la máquina virtual Java (JVM) subyacente.  
  
 La propiedad **trustStore** especifica la ruta de acceso (incluido el nombre de archivo) del archivo trustStore de certificado, que contiene la lista de certificados en los que el cliente confía. La propiedad **trustStorePassword** especifica la contraseña que se usa para comprobar la integridad de los datos de trustStore. Para obtener más información sobre cómo utilizar el almacén de confianza predeterminado de la JVM, consulte [Configuración del cliente para el cifrado](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
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
  
 Si la propiedad **Encrypt** está establecida en **true** y la propiedad **trustServerCertificate** está establecida en **false** y el nombre del servidor de la cadena de conexión no coincide con el nombre del servidor en el certificado TLS, se mostrará el siguiente error: `The driver couldn't establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "java.security.cert.CertificateException: Failed to validate the server name in a certificate during Secure Sockets Layer (SSL) initialization."`. A partir de la versión 7.2, el controlador admite la coincidencia de patrones comodín en la etiqueta situada más a la izquierda del nombre del servidor en el certificado TLS.

## <a name="see-also"></a>Consulte también

 [Uso de cifrado](../../connect/jdbc/using-ssl-encryption.md) [Protección de las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)