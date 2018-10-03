---
title: Obtener acceso a información de diagnóstico en el registro de eventos extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: aaa180c2-5e1a-4534-a125-507c647186ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba5a8d97583dd2ea8938b2fdb4b74dce94c4f047
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142635"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Obtener acceso a información de diagnóstico en el registro de eventos extendidos
  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seguimiento de acceso a datos y Native Client ([seguimiento de acceso a datos](http://go.microsoft.com/fwlink/?LinkId=125805)) se han actualizado para que sea más fácil obtener información de diagnóstico acerca de errores de conexión desde el anillo de conectividad información de rendimiento de búfer y aplicación del registro de eventos extendidos.  
  
 Para obtener información sobre la lectura del registro de eventos extendidos, vea [Ver datos de sesión de evento](../../../database-engine/view-event-session-data.md).  
  
> [!NOTE]  
>  Esta función está dirigida únicamente a la solución de problemas y al diagnóstico, además es posible que no sea adecuada para fines de auditoría o seguridad.  
  
## <a name="remarks"></a>Comentarios  
 Para las operaciones de conexión, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enviará un identificador de conexión de cliente. Si se produce un error en la conexión, puede tener acceso al búfer de anillo de conectividad ([solucionar problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](http://go.microsoft.com/fwlink/?LinkId=207752)) y busque el `ClientConnectionID` campo y obtener información de diagnóstico el Error de conexión. Los identificadores de conexión del cliente se registran en el búfer de anillo únicamente si se produce un error. (Si se produce un error en una conexión antes de enviar el paquete de inicio de sesión previo, no se generará un identificador de conexión del cliente.) El identificador de conexión del cliente es un GUID de 16 bytes. Asimismo, puede buscar el identificador de conexión del cliente en el destino de salida de eventos extendidos, si se agrega la acción `client_connection_id` a los eventos de una sesión de eventos extendidos. Puede habilitar el seguimiento de acceso a datos, volver a ejecutar el comando de conexión y observar el campo de `ClientConnectionID` en el seguimiento de acceso a datos de una operación que no se realizó correctamente, si necesita asistencia adicional de diagnóstico.  
  
 Si está utilizando ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y una conexión se realiza correctamente, el cliente puede obtener Id. de conexión mediante el uso de la `SQL_COPT_SS_CLIENT_CONNECTION_ID` con el atributo [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client también envía un identificador de actividad específico para cada subproceso. El identificador de actividad se captura en las sesiones de eventos extendidos si las sesiones se inician con la opción TRACK_CAUSAILITY habilitada. Con respecto a los problemas de rendimiento con una conexión activa, puede obtener el identificador de actividad a partir del seguimiento de acceso a datos del cliente (campo `ActivityID`) y, posteriormente, buscar el identificador de actividad en la salida de eventos extendidos. El identificador de actividad en los eventos extendidos es un GUID de 16 bytes (no es el mismo que el GUID para el identificador de conexión del cliente) anexado a un número de secuencia de cuatro bytes. El número de secuencia representa el orden de una solicitud en un subproceso e indica el orden relativo del lote, así como las instrucciones RPC para el subproceso. `ActivityID` se envía opcionalmente para las instrucciones por lotes de SQL y solicitudes RPC cuando el seguimiento de acceso a datos se habilita y el bit décimo octavo de la palabra de configuración del seguimiento de acceso a datos se establece en ON.  
  
 A continuación, se aporta un ejemplo que utiliza [!INCLUDE[tsql](../../../includes/tsql-md.md)] para iniciar una sesión de eventos extendidos que se va a almacenar en un búfer de anillo y que registrará el identificador de actividad que se envía desde un cliente en operaciones de RPC y por lotes.  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
  
```  
  
## <a name="control-file"></a>Archivo de control  
 En [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], el contenido del archivo de control de SQL Server Native Client (ctrl.guid.snac11) es:  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x00000000  0   MSDADIAG.ETW  
{2DA81B52-908E-7DB6-EF81-76856BB47C4F}  0xFFFFFFFF  0   SQLNCLI11.1  
```  
  
## <a name="mof-file"></a>Archivo MOF  
 En [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], el contenido del archivo MOF de SQL Server Native Client es:  
  
```  
#pragma classflags("forceupdate")  
#pragma namespace ("\\\\.\\Root\\WMI")  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSDADIAG.ETW  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F3-3CC6-0B9C-6651-9649CCE5C752}"),  
 DisplayName("msdadiag"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace : Bid2Etw_MSDADIAG_ETW  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextA : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextW : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  SQLNCLI11.1  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B52-908E-7DB6-EF81-76856BB47C4F}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B53-908E-7DB6-EF81-76856BB47C4F}"),  
 DisplayName("SQLNCLI11.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace : Bid2Etw_SQLNCLI11_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextA : Bid2Etw_SQLNCLI11_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextW : Bid2Etw_SQLNCLI11_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
```  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
