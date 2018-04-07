---
title: Obtener acceso a información de diagnóstico en el registro de eventos extendidos | Documentos de Microsoft
description: Seguimiento de controlador de OLE DB para SQL Server y obtener acceso a información de diagnóstico en el registro de eventos extendidos
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.openlocfilehash: ea81e8bc007b9afd526901bcd60827238f5356e4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Obtener acceso a información de diagnóstico en el registro de eventos extendidos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], controlador de OLE DB para SQL Server y datos de seguimiento de acceso ([seguimiento de acceso a datos](http://go.microsoft.com/fwlink/?LinkId=125805)) se han actualizado para que sea más fácil obtener información de diagnóstico sobre errores de conexión desde el búfer de anillo de conectividad y la información de rendimiento de aplicación desde el registro de eventos extendidos.  
  
 Para obtener información acerca de cómo leer el registro de eventos extendidos, vea [View Event Session Data](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md). 

  
> [!NOTE]  
>  Esta función está dirigida únicamente a la solución de problemas y al diagnóstico, además es posible que no sea adecuada para fines de auditoría o seguridad.  
  
## <a name="remarks"></a>Comentarios  
 Para las operaciones de conexión, el controlador OLE DB para SQL Server enviará un cliente de identificador de conexión. Si se produce un error en la conexión, puede tener acceso al búfer de anillo de conectividad ([solucionar problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](http://go.microsoft.com/fwlink/?LinkId=207752)) y busque la **ClientConnectionID** campo y obtener información de diagnóstico sobre el error de conexión. Los identificadores de conexión del cliente se registran en el búfer de anillo únicamente si se produce un error. (Si se produce un error en una conexión antes de enviar el paquete de inicio de sesión previo, no se generará un identificador de conexión del cliente.) El identificador de conexión del cliente es un GUID de 16 bytes. También puede encontrar el cliente de destino, de la salida de identificador de conexión en los eventos extendidos si la **client_connection_id** acción se agrega a los eventos en una sesión de eventos extendidos. Puede habilitar el seguimiento de acceso de datos y vuelva a ejecutar el comando de conexión y observar la **ClientConnectionID** campo en el seguimiento de acceso de datos para una operación con errores, si necesita más ayuda de diagnóstico.  
   
  
 Controlador de OLE DB para SQL Server también envía un identificador de actividad específico del subproceso. El identificador de actividad se captura en las sesiones de eventos extendidos si las sesiones se inician con la opción TRACK_CAUSAILITY habilitada. Para problemas de rendimiento con una conexión activa, puede obtener el identificador de actividad de seguimiento de acceso a datos del cliente (**ActivityID** campo) y, a continuación, busque el identificador de actividad en la salida de eventos extendidos. El identificador de actividad en los eventos extendidos es un GUID de 16 bytes (no es el mismo que el GUID para el identificador de conexión del cliente) anexado a un número de secuencia de cuatro bytes. El número de secuencia representa el orden de una solicitud en un subproceso e indica el orden relativo del lote, así como las instrucciones RPC para el subproceso. El **ActivityID** envía opcionalmente para instrucciones SQL por lotes y solicitudes RPC cuando se habilita el seguimiento de acceso de datos en y se activa el bit 18 en el seguimiento palabra de configuración de acceso de datos.  
  
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
 El contenido del controlador OLE DB para el archivo de control de SQL Server (ctrl.guid) es:  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>Archivo MOF  
 El contenido del controlador OLE DB para el archivo mof de SQL Server es:  
  
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
//  MSOLEDBSQL.1  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59D-D3E8-9684-AEAC-B214EFD91B31}"),  
 DisplayName("MSOLEDBSQL.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace : Bid2Etw_MSOLEDBSQL_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextA : Bid2Etw_MSOLEDBSQL_1_Trace  
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
 Description("MSOLEDBSQL.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextW : Bid2Etw_MSOLEDBSQL_1_Trace  
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
 [Control de errores](../../oledb/ole-db-errors/errors.md)  
  
  
