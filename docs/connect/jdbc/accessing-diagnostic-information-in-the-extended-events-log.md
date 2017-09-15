---
title: "Obtener acceso a información de diagnóstico en el registro de eventos extendidos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6dfbd857905f0c0f444c44a9c9eb9813cc32ab2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Obtener acceso a información de diagnóstico en el registro de eventos extendidos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En el [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], el seguimiento ([el funcionamiento del controlador de seguimiento](../../connect/jdbc/tracing-driver-operation.md)) se ha actualizado para facilitar más fácil correlacionar eventos de cliente con información de diagnóstico, como errores de conexión, de anillo de conectividad del servidor información de rendimiento de búfer y aplicación en el registro de eventos extendidos. Para obtener información acerca de cómo leer el registro de eventos extendidos, vea [View Event Session Data](http://msdn.microsoft.com/library/hh710068(SQL.110).aspx).  
  
## <a name="details"></a>Detalles  
 Para las operaciones de conexión, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enviará un cliente de identificador de conexión. Si se produce un error en la conexión, puede tener acceso al búfer de anillo de conectividad ([solucionar problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](http://go.microsoft.com/fwlink/?LinkId=207752)) y busque la **ClientConnectionID** campo y obtener información de diagnóstico sobre el error de conexión. Los identificadores de conexión del cliente se registran en el búfer de anillo únicamente si se produce un error. (Si se produce un error en una conexión antes de enviar el paquete de inicio de sesión previo, no se generará un identificador de conexión del cliente.) El identificador de conexión del cliente es un GUID de 16 bytes. También puede encontrar la conexión de cliente del identificador en el resultado de destino de eventos extendidos, si la **client_connection_id** acción se agrega a los eventos en una sesión de eventos extendidos. Puede habilitar el seguimiento y vuelva a ejecutar el comando de conexión y observar la **ClientConnectionID** campo en el seguimiento, si necesita más ayuda de diagnóstico de controlador de cliente.  
  
 Puede obtener el cliente de identificador de conexión mediante programación usando [ISQLServerConnection, interfaz](../../connect/jdbc/reference/isqlserverconnection-interface.md). El identificador de conexión también estará presente en cualquier excepción relacionada con la conexión.  
  
 Cuando se produzca un error de conexión, el identificador de conexión de cliente en la información de seguimiento de BID del servidor y en el búfer de anillo de conectividad puede ayudar a correlacionar las conexiones de cliente con las conexiones en el servidor. Para obtener más información acerca de BID realiza un seguimiento en el servidor, consulte [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805). Tenga en cuenta que el artículo de seguimiento de acceso de datos también contiene información acerca de cómo realizar un seguimiento de acceso a datos, que no se aplica a la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; vea [el funcionamiento del controlador de seguimiento](../../connect/jdbc/tracing-driver-operation.md) para obtener información sobre cómo hacer un seguimiento de acceso a datos mediante el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 El controlador JDBC también envía un identificador de actividad específico de subproceso. El identificador de actividad se captura en las sesiones de eventos extendidos si las sesiones se inician con la opción TRACK_CAUSAILITY habilitada. En el caso de problemas de rendimiento con una conexión activa, puede obtener el identificador de actividad del seguimiento del cliente (campo ActivityID) y, a continuación, buscar el identificador de actividad en la salida de eventos extendidos. El identificador de actividad en los eventos extendidos es un GUID de 16 bytes (no es el mismo GUID que el identificador de conexión de cliente) anexado con un número de secuencia de cuatro bytes. El número de secuencia representa el orden de una solicitud en un subproceso. El campo ActivityId se envía para las instrucciones por lotes SQL y las solicitudes RPC. Para habilitar el envío de ActivityId al servidor, primero debe especificar el siguiente par clave-valor en el archivo Logging.Properties:  
  
```  
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 Cualquier valor distinto de `on` (distingue mayúsculas de minúsculas) deshabilitará el envío de ActivityId.  
  
 Para obtener más información, consulte [funcionamiento del controlador de seguimiento](../../connect/jdbc/tracing-driver-operation.md). Esta marca de seguimiento se utiliza con los registradores de objetos JDBC correspondientes para decidir si se realiza el seguimiento y enviar ActivityId en el controlador JDBC. Además de actualizar el archivo Logging.Properties, el registrador com.microsoft.sqlserver.jdbc debe estar habilitado en FINER o superior. Si desea enviar ActivityId al servidor para las solicitudes efectuadas por una determinada clase, se debe habilitar el registrador de clase correspondiente en FINER o FINEST. Por ejemplo, si la clase es SQLServerStatement, habilite el registrador com.microsoft.sqlserver.jdbc.SQLServerStatement.  
  
 El siguiente es un ejemplo que utiliza [!INCLUDE[tsql](../../includes/tsql_md.md)] iniciar una sesión de eventos extendidos que se almacenarán en un búfer de anillo y registrará el Id. de actividad enviado desde un cliente en operaciones RPC y por lotes:  
  
```  
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>Vea también  
 [Diagnosticar problemas con el controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
