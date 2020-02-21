---
title: Obtener acceso a información de diagnóstico en el registro de eventos extendidos | Microsoft Docs
description: Seguimiento de OLE DB Driver for SQL Server y acceso a información de diagnóstico en el registro de eventos extendidos
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 72be95d424875b1c7bc64c129eb98a6b1c4804ea
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989189"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Obtener acceso a información de diagnóstico en el registro de eventos extendidos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], el controlador OLE DB para SQL Server y el seguimiento de acceso a datos ([Seguimiento de acceso a datos](https://go.microsoft.com/fwlink/?LinkId=125805)) se han actualizado para facilitar la obtención de información de diagnóstico sobre los errores de conexión de la información desde el búfer de anillo de conectividad y de información sobre el rendimiento de la aplicación a partir del registro de eventos extendidos.  
  
 Para obtener información sobre la lectura del registro de eventos extendidos, vea [Ver datos de sesión de evento](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md). 

  
> [!NOTE]  
>  Esta función está dirigida únicamente a la solución de problemas y al diagnóstico, además es posible que no sea adecuada para fines de auditoría o seguridad.  
  
## <a name="remarks"></a>Observaciones  
 Para las operaciones de conexión, OLE DB Driver for SQL Server enviará un identificador de conexión de cliente. Si se produce un error en la conexión, puede tener acceso al búfer de anillo de conectividad ([Solución de problemas de conectividad en SQL Server 2008 con el búfer de anillo de conectividad](https://go.microsoft.com/fwlink/?LinkId=207752)) y buscar el campo **ClientConnectionID** para obtener información de diagnóstico sobre el error de conexión. Los identificadores de conexión del cliente se registran en el búfer de anillo únicamente si se produce un error. (Si se produce un error en una conexión antes de enviar el paquete de inicio de sesión previo, no se generará un identificador de conexión del cliente). El identificador de conexión del cliente es un GUID de 16 bytes. También puede buscar el identificador de conexión del cliente en el destino de salida de eventos extendidos si se agrega la acción **client_connection_id** a los eventos de una sesión de eventos extendidos. Puede habilitar el seguimiento de acceso a datos, volver a ejecutar el comando de conexión y observar el campo **ClientConnectionID** en el seguimiento de acceso a datos de una operación que no se ha realizado correctamente si necesita asistencia adicional de diagnóstico.  
   
  
 OLE DB Driver for SQL Server también envía un identificador de actividad específico de subproceso. El identificador de actividad se captura en las sesiones de eventos extendidos si las sesiones se inician con la opción TRACK_CAUSAILITY habilitada. En el caso de problemas de rendimiento con una conexión activa, puede obtener el identificador de actividad del seguimiento de acceso a datos del cliente (campo **ActivityID**) y, después, buscar el identificador de actividad en la salida de eventos extendidos. El identificador de actividad en los eventos extendidos es un GUID de 16 bytes (no es el mismo que el GUID para el identificador de conexión del cliente) anexado a un número de secuencia de cuatro bytes. El número de secuencia representa el orden de una solicitud en un subproceso e indica el orden relativo del lote, así como las instrucciones RPC para el subproceso. **ActivityID** se envía opcionalmente para las instrucciones por lotes de SQL y las solicitudes RPC cuando el seguimiento de acceso a datos se habilita y el bit décimo octavo de la palabra de configuración del seguimiento de acceso a datos se establece en ON.  
  
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
 El contenido del archivo de control de OLE DB Driver for SQL Server (ctrl.guid) es:  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>Archivo MOF  
 El contenido del archivo mof de OLE DB Driver for SQL Server es:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Control de errores](../../oledb/ole-db-errors/errors.md)  
  
  
