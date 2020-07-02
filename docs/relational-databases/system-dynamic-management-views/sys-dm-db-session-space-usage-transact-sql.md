---
title: Sys. dm_db_session_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_session_space_usage_TSQL
- dm_db_session_space_usage
- sys.dm_db_session_space_usage
- sys.dm_db_session_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_session_space_usage dynamic management view
ms.assetid: a67a6045-8e14-460a-9fe3-912b846c08c1
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6802bf985e446f9c81a38be7a99a47eeebe6d73c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738747"
---
# <a name="sysdm_db_session_space_usage-transact-sql"></a>sys.dm_db_session_space_usage (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Devuelve el número de páginas asignadas y desasignadas por cada sesión en la base de datos.  
  
> [!NOTE]  
>  Esta vista solo es aplicable a la [base de datos Tempdb](../../relational-databases/databases/tempdb-database.md).  
  
> [!NOTE]  
>  Para llamar a este método desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use el nombre **Sys. dm_pdw_nodes_db_session_space_usage**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|Id. de sesión.<br /><br /> **session_id** asigna a **session_id** en [Sys. dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).|  
|**database_id**|**smallint**|Id. de la base de datos.|  
|**user_objects_alloc_page_count**|**bigint**|Número de páginas reservadas o asignadas por esta sesión para objetos de usuario.|  
|**user_objects_dealloc_page_count**|**bigint**|Número de páginas desasignadas y que ya no están reservadas por esta sesión para objetos de usuario.|  
|**internal_objects_alloc_page_count**|**bigint**|Número de páginas reservadas o asignadas por esta sesión para objetos internos.|  
|**internal_objects_dealloc_page_count**|**bigint**|Número de páginas desasignadas y que ya no están reservadas por esta sesión para objetos internos.|  
|**user_objects_deferred_dealloc_page_count**|**bigint**|Número de páginas que se han marcado para la desasignación diferida.<br /><br /> **Nota:** Introducido en Service Packs para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="remarks"></a>Comentarios  
 Páginas IAM no incluidas en ninguno de los recuentos de asignación y desasignación comunicados por esta vista.  
  
 Los recuentos de páginas se inicializan a cero (0) en el inicio de una sesión. Los recuentos realizan el seguimiento del número total de páginas que se han asignado o desasignado para tareas que ya se han completado en la sesión. Los recuentos se actualizan solo cuando una tarea finaliza; no reflejan las tareas en ejecución.  
  
 Una sesión puede tener varias solicitudes activas simultáneamente. Una solicitud puede iniciar varios subprocesos, tareas, si está en una consulta paralela.  
  
 Para obtener más información sobre las sesiones, las solicitudes y las tareas, vea [Sys. dm_exec_sessions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md), [sys. dm_exec_requests &#40;transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)y [Sys. dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).  
  
## <a name="user-objects"></a>Objetos de usuario  
 Los objetos siguientes se incluyen en los contadores de páginas de objetos de usuario:  
  
-   Índices y tablas definidos por el usuario  
  
-   Índices y tablas del sistema  
  
-   Índices y tablas temporales globales  
  
-   Índices y tablas temporales locales  
  
-   Variables de tabla  
  
-   Tablas devueltas en las funciones con valores de tabla.  
  
## <a name="internal-objects"></a>Objetos internos  
 Los objetos internos solo están en **tempdb**. Los objetos siguientes se incluyen en los contadores de páginas de objetos internos:  
  
-   Tablas de trabajo para operaciones de cola o cursor y almacenamiento de objetos grandes (LOB) temporales  
  
-   Archivos de trabajo para operaciones como la combinación hash  
  
-   Ordenaciones  
  
## <a name="physical-joins"></a>Combinaciones físicas  
 ![Combinaciones físicas de sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/media/join-dm-db-session-space-usage-1.gif "Combinaciones físicas de sys.dm_db_session_space_usage")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|A|Relación|  
|----------|--------|------------------|  
|dm_db_session_space_usage.session_id|dm_exec_sessions.session_id|Uno a uno|  
  
## <a name="see-also"></a>Consulte también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Sys. dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [Sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Sys. dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [Sys. dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



