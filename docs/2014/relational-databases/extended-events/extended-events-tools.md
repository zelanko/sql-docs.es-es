---
title: Extended eventos herramientas | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e26bc62f0e6b81b7b4ac8e1361d0a1ac31513ef6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63137051"
---
# <a name="extended-events-tools"></a>Herramientas de eventos extendidos
  Puede utilizar las siguientes herramientas para crear y administrar sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events:  
  
-   Instrucciones de lenguaje de definición de datos (DDL). Estas instrucciones le permiten crear y modificar una sesión de eventos extendidos.  
  
-   Vistas de administración dinámica, vistas de catálogo y tablas del sistema. Estos elementos le permiten obtener datos y metadatos de sesión mediante el uso de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] . Las tablas del sistema le ayudan a determinar los equivalentes de eventos extendidos existentes para columnas y clases de eventos de Seguimiento de SQL.  
  
-   El nodo **Eventos extendidos** del Explorador de objetos. Le permite iniciar, detener o eliminar una sesión, o importar y exportar plantillas de sesión.  
  
-   El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Es una herramienta eficaz que puede usar para crear, modificar y administrar sesiones de eventos extendidos. Para obtener más información, vea [Usar el proveedor de PowerShell para eventos extendidos](use-the-powershell-provider-for-extended-events.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  Le permite crear y ejecutar los ejemplos de código que se proporcionan en los temas de eventos extendidos. Para obtener más información, vea [Explorador de objetos](../../ssms/object/object-explorer.md).  
  
 Además de las sesiones que cree, existe una sesión de estado del sistema predeterminada en el servidor. La sesión recopila datos del sistema que se pueden utilizar para ayudar a solucionar problemas de rendimiento. Para obtener más información, vea [Usar la sesión system_health](use-the-ssms-xe-profiler.md).  
  
## <a name="ddl-statements"></a>Instrucciones DDL  
 Utilice las instrucciones DDL siguientes para crear, cambiar y quitar una sesión de eventos extendidos.  
  
|Name|Descripción|  
|----------|-----------------|  
|[CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)|Crea un objeto de sesión de eventos extendidos que identifica el origen de los eventos, los destinos de la sesión de eventos y los parámetros de la sesión de eventos.|  
|[ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)|Inicia o detiene una sesión de eventos, o cambia la configuración de una sesión de eventos.|  
|[DROP EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-session-transact-sql)|Quita una sesión de eventos.|  
  
## <a name="catalog-views"></a>Vistas de catálogo  
 Utilice las vistas de catálogo siguientes para obtener los metadatos que se crean al crear una sesión de eventos.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[sys.server_event_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql)|Enumera todas las definiciones de sesión de eventos.|  
|[sys.server_event_session_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql)|Devuelve una fila por cada acción en cada evento de una sesión de eventos.|  
|[sys.server_event_session_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql)|Devuelve una fila para cada evento de una sesión de eventos.|  
|[sys.server_event_session_fields &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql)|Devuelve una fila para cada columna personalizable que se estableció explícitamente en los eventos y destinos.|  
|[sys.server_event_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql)|Devuelve una fila para cada destino de evento de una sesión de eventos.|  
  
## <a name="dynamic-management-views"></a>Vistas de administración dinámica  
 Las vistas de administración dinámica siguientes se utilizan para obtener metadatos y datos de la sesión. Los metadatos se obtienen de las vistas de catálogo. Los datos de la sesión se crean cuando se inicia y ejecuta una sesión de eventos.  
  
> [!NOTE]  
>  Estas vistas no contienen datos de sesión hasta que se inicia una sesión.  
  
|Name|Descripción|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql)|Devuelve información sobre los grupos de distribuidores de la sesión.|  
|[sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)|Devuelve una fila por cada objeto expuesto por un paquete de eventos.|  
|[sys.dm_xe_object_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql)|Devuelve la información del esquema para todos los objetos.|  
|[sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)|Enumera todos los paquetes registrados en el motor de eventos extendidos.|  
|[sys.dm_xe_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql)|Devuelve información sobre una sesión de eventos extendidos activa.|  
|[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)|Devuelve información sobre los destinos de la sesión.|  
|[sys.dm_xe_session_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql)|Devuelve información sobre los eventos de la sesión.|  
|[sys.dm_xe_session_event_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql)|Devuelve información sobre las acciones de la sesión de eventos.|  
|[sys.dm_xe_map_values &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql)|Proporciona una asignación de claves numéricas internas a texto legible.|  
|[sys.dm_xe_session_object_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql)|Muestra los valores de configuración de los objetos enlazados a una sesión.|  
  
## <a name="system-tables"></a>Tablas del sistema  
 Las tablas del sistema siguientes se utilizan para obtener información sobre los equivalentes de eventos extendidos para columnas y clases de eventos de Seguimiento de SQL.  
  
|Name|Descripción|  
|----------|-----------------|  
|[trace_xe_event_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/extended-events-tables-trace-xe-event-map)|Contiene una fila para cada evento de eventos extendidos que está asignado a una clase de eventos de Seguimiento de SQL.|  
|[trace_xe_action_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/extended-events-tables-trace-xe-action-map)|Contiene una fila para cada acción de eventos extendidos que se asigna a un identificador de columna de Seguimiento de SQL.|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../views/views.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)   
 [Tablas de eventos extendidos de SQL Server &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/system-tables-transact-sql)   
 [Usar la sesión system_health](use-the-ssms-xe-profiler.md)   
 [Usar el proveedor de PowerShell para eventos extendidos](use-the-powershell-provider-for-extended-events.md)  
  
  
