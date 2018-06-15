---
title: Seguridad de la aplicación | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8226badb1031792badc1601cd12c2a0e2f13c9bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32827770"
---
# <a name="application-security"></a>Seguridad de aplicaciones
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es importante tomar precauciones para garantizar la seguridad de la aplicación. Las siguientes secciones proporcionan información sobre los pasos que puede realizar para contribuir a la seguridad de su aplicación.  
  
## <a name="using-java-policy-permissions"></a>Usar los permisos de la directiva de Java  
 Cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es importante especificar los permisos de directiva de Java necesarios que requiere el controlador JDBC. Java Runtime Environment (JRE) proporciona un amplio modelo de seguridad que puede usar en el tiempo de ejecución para determinar si un subproceso tiene acceso a un recurso. Los archivos de directiva de seguridad pueden controlar este acceso. Los archivos de directivas del contenedor están administrados por el encargado de la implementación y el administrador del sistema, pero los permisos que se enumeran en este tema son aquellos que afectan al funcionamiento del controlador JDBC.  
  
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
 Cuando usa el controlador JDBC para comunicarse con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos, puede proteger el canal de comunicación mediante seguridad de protocolo de Internet (IPSEC) o capa de Sockets seguros (SSL); o ambos.  
  
 La compatibilidad con SSL se puede utilizar para proporcionar un nivel adicional de protección además de IPSEC. Para obtener más información sobre el uso de SSL, consulte [utilizando cifrado SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Vea también  
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
