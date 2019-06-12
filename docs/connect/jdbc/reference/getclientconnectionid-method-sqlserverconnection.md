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
manager: jroth
ms.openlocfilehash: c8e6a69ed6300ba6eaaedadbc0b0e7c586738647
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763906"
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
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre el acceso a información de diagnóstico en el registro de eventos extendidos, vea [acceso a información de diagnóstico en el registro de eventos extendidos](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
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
  
 **getClientConnectionID** funciona independientemente de qué versión del servidor se conecta a, pero los registros de eventos extendidos y entrada en errores de búfer de anillo de conectividad no estará presentes en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 R2 y versiones anteriores.  
  
 Puede buscar el identificador de conexión en el registro de eventos extendidos para comprobar si el error se encontraba en el servidor si está habilitado el evento extendido para el registro del identificador de conexión. También puede buscar el identificador de conexión en el búfer de anillo de conexión ([Solución de problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](https://go.microsoft.com/fwlink/?LinkId=207752)) para determinados errores de conexión. Si el identificador de conexión no se encuentra en el búfer de anillo de conexión, se puede suponer que hay un error de red.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
