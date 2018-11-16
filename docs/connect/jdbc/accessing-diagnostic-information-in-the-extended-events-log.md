---
title: Obtener acceso a información de diagnóstico en el registro de eventos extendidos | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef5c7aee0daef073ff22494162d8024201b2f97c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600832"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Obtener acceso a información de diagnóstico en el registro de eventos extendidos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], el seguimiento ([Hacer un seguimiento del funcionamiento del controlador](../../connect/jdbc/tracing-driver-operation.md)) se ha actualizado para facilitar la correlación de eventos de cliente con la información de diagnóstico, como los errores de conexión, a partir del búfer en anillo de conectividad del servidor y la información de rendimiento de aplicación en el registro de eventos extendidos. Para obtener información sobre la lectura del registro de eventos extendidos, vea [Ver datos de sesión de evento](https://msdn.microsoft.com/library/hh710068(SQL.110).aspx).  
  
## <a name="details"></a>Detalles  
 Para las operaciones de conexión, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enviará un identificador de conexión de cliente. Si se produce un error en la conexión, puede tener acceso al búfer de anillo de conectividad ([Solución de problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](https://go.microsoft.com/fwlink/?LinkId=207752)) y buscar el campo **ClientConnectionID** para obtener información de diagnóstico sobre el error de conexión. Los identificadores de conexión del cliente se registran en el búfer de anillo únicamente si se produce un error. (Si se produce un error en una conexión antes de enviar el paquete de inicio de sesión previo, no se generará un identificador de conexión del cliente.) El identificador de conexión del cliente es un GUID de 16 bytes. También puede buscar el identificador de conexión del cliente en la salida de destino de eventos extendidos si se agrega la acción **client_connection_id** a los eventos de una sesión de eventos extendidos. Si necesita más ayuda de diagnóstico del controlador cliente, puede habilitar el seguimiento, volver a ejecutar el comando de conexión y observar el campo **ClientConnectionID** en el seguimiento.  
  
 El cliente puede obtener Id. de conexión mediante programación usando [ISQLServerConnection, interfaz](../../connect/jdbc/reference/isqlserverconnection-interface.md). El identificador de conexión también estará presente en cualquier excepción relacionada con la conexión.  
  
 Cuando se produzca un error de conexión, el identificador de conexión de cliente en la información de seguimiento de diagnósticos integrados (BID) del servidor y en el búfer en anillo de conectividad puede ayudar a correlacionar las conexiones de cliente con las conexiones en el servidor. Para más información sobre los seguimientos de BID en el servidor, vea [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Seguimiento de acceso de datos). Tenga en cuenta que el artículo de seguimiento de acceso de datos también incluye información sobre el seguimiento de acceso de datos que no se aplica a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; vea [Hacer un seguimiento del funcionamiento del controlador](../../connect/jdbc/tracing-driver-operation.md) para obtener información sobre cómo realizar un seguimiento de acceso de datos mediante [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 El controlador JDBC también envía un identificador de actividad específico de subproceso. El identificador de actividad se captura en las sesiones de eventos extendidos si las sesiones se inician con la opción TRACK_CAUSAILITY habilitada. En el caso de problemas de rendimiento con una conexión activa, puede obtener el identificador de actividad del seguimiento del cliente (campo ActivityID) y, a continuación, buscar el identificador de actividad en la salida de eventos extendidos. El identificador de actividad en los eventos extendidos es un GUID de 16 bytes (no es el mismo GUID que el identificador de conexión de cliente) anexado con un número de secuencia de cuatro bytes. El número de secuencia representa el orden de una solicitud en un subproceso. El campo ActivityId se envía para las instrucciones por lotes SQL y las solicitudes RPC. Para habilitar el envío de ActivityId al servidor, primero debe especificar el siguiente par clave-valor en el archivo Logging.Properties:  
  
```
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 Cualquier otro valor distinto de `on` (distingue mayúsculas de minúsculas) deshabilitará el envío de ActivityId.  
  
 Para obtener más información, vea [Hacer un seguimiento del funcionamiento del controlador](../../connect/jdbc/tracing-driver-operation.md). Esta marca de seguimiento se utiliza con los registradores de objetos JDBC correspondientes para decidir si se realiza el seguimiento y enviar ActivityId en el controlador JDBC. Además de actualizar el archivo Logging.Properties, el registrador com.microsoft.sqlserver.jdbc debe estar habilitado en FINER o superior. Si quiere enviar ActivityId al servidor para las solicitudes efectuadas por una determinada clase, se debe habilitar el registrador de clase correspondiente en FINER o FINEST. Por ejemplo, si la clase es SQLServerStatement, habilite el registrador com.microsoft.sqlserver.jdbc.SQLServerStatement.  
  
 El ejemplo siguiente usa [!INCLUDE[tsql](../../includes/tsql-md.md)] para iniciar una sesión de eventos extendidos que se almacenará en un búfer en anillo y registrará el identificador de actividad enviado por un cliente en operaciones RPC y por lotes:  
  
```sql
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>Ver también  
 [Diagnosticar problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
