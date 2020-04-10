---
title: Seguridad de la aplicación | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 650a298b9cc67b24c33f3da370a8a1b6de6ac63b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922669"
---
# <a name="application-security"></a>Seguridad de la aplicación
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando sea usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es importante tomar precauciones para garantizar la seguridad de la aplicación. Las siguientes secciones proporcionan información sobre los pasos que puede realizar para contribuir a la seguridad de su aplicación.  
  
## <a name="using-java-policy-permissions"></a>Usar permisos de directiva de Java  
 Cuando sea usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es importante especificar los permisos de directiva de Java que el controlador JDBC necesita. Java Runtime Environment (JRE) proporciona un amplio modelo de seguridad que puede usar en el tiempo de ejecución para determinar si un subproceso tiene acceso a un recurso. Los archivos de directiva de seguridad pueden controlar este acceso. Los archivos de directivas del contenedor están administrados por el encargado de la implementación y el administrador del sistema, pero los permisos que se enumeran en este tema son aquellos que afectan al funcionamiento del controlador JDBC.  
  
 Un permiso típico de los archivos de directivas tiene este aspecto:  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 La siguiente base de códigos debería estar limitada a la base de códigos del controlador JDBC para asegurarse de que se concede la cantidad mínima de privilegios.  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  El código "file:/install_dir/lib/-" hace referencia al directorio de instalación del controlador JDBC.  
  
## <a name="protecting-server-communication"></a>Protección de las comunicaciones con el servidor  
 Cuando se usa el controlador JDBC para comunicarse con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede proteger el canal de comunicaciones mediante el protocolo de seguridad de Internet (IPSec), Capa de sockets seguros (SSL) o ambos.  
  
 La compatibilidad con SSL se puede utilizar para proporcionar un nivel adicional de protección además de IPSEC. Para más información sobre cómo usar SSL, consulte [Usar el cifrado SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Consulte también  
 [Protección de las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
