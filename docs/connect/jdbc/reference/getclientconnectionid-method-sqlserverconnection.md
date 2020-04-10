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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 461a3a0e217fb2ad973830eaffc86ff048830b83
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907641"
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
  
  
