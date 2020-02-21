---
title: Método getClientConnectionID (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84367995aa5820bc6078b5e62bc830b0e58c4b0a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953174"
---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>Método getClientConnectionID (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtiene el identificador de conexión del intento de conexión más reciente, independientemente de que dicho intento fuera correcto o erróneo.  
  
## <a name="syntax"></a>Sintaxis  
  
``` 
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 GUID de 16 bytes que representa el identificador de conexión del intento de conexión más reciente. O NULL si hay un error después de que se inicie la solicitud de conexión y el protocolo de enlace previo al inicio de sesión.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Para más información sobre el acceso a la información de diagnóstico en el registro de eventos extendidos, consulte [Acceso a información de diagnóstico en el registro de eventos extendidos](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
 En el siguiente ejemplo se muestra cómo obtener el identificador de conexión:  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 En el siguiente ejemplo se muestra otra forma de obtener el identificador de conexión:  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("...");  
ds.setPassword("...");  
ds.setServerName("...");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID** funciona independientemente de la versión del servidor a la que se conecte, pero los registros de eventos extendidos y la entrada en los errores de búfer de anillo de conectividad no estarán presentes en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 R2 y versiones anteriores.  
  
 Puede buscar el identificador de conexión en el registro de eventos extendidos para comprobar si el error se encontraba en el servidor si está habilitado el evento extendido para el registro del identificador de conexión. También puede buscar el identificador de conexión en el búfer de anillo de conexión ([Solución de problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](https://go.microsoft.com/fwlink/?LinkId=207752)) para determinados errores de conexión. Si el identificador de conexión no se encuentra en el búfer de anillo de conexión, se puede suponer que hay un error de red.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
