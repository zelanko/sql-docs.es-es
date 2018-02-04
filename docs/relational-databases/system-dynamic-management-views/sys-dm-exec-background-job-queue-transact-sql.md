---
title: sys.dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d80848491c46046ba260956fb02ce41e7becdd6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada trabajo del procesador de consultas que está programado para ejecución asincrónica (en segundo plano).  
  
> **NOTA** Para llamar a esta desde  **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]**  o  **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** , use el nombre **sys.dm_pdw_nodes_exec_background_job_queue**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|Hora en que se agregó el trabajo a la cola.|  
|**job_id**|**int**|Identificador del trabajo.|  
|**database_id**|**int**|Base de datos en que se va a ejecutar el trabajo.|  
|**object_id1**|**int**|El valor depende del tipo de trabajo. Para obtener más información, vea la sección Comentarios.|  
|**object_id2**|**int**|El valor depende del tipo de trabajo. Para obtener más información, vea la sección Comentarios.|  
|**object_id3**|**int**|El valor depende del tipo de trabajo. Para obtener más información, vea la sección Comentarios.|  
|**object_id4**|**int**|El valor depende del tipo de trabajo. Para obtener más información, vea la sección Comentarios.|  
|**error_code**|**int**|Código de error si el trabajo se ha vuelto a insertar debido a un error. NULL si se ha suspendido, no se ha seleccionado o se ha completado.|  
|**request_type**|**smallint**|Tipo de trabajo solicitado.|  
|**retry_count**|**smallint**|Número de veces que el trabajo se ha seleccionado de la cola y se ha vuelto a insertar porque faltaban recursos u otro motivo.|  
|**in_progress**|**smallint**|Indica si el trabajo ha empezado a ejecutarse.<br /><br /> 1 = Iniciado<br /><br /> 0 = En espera|  
|**session_id**|**smallint**|Identificador de la sesión.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere el permiso VIEW SERVER STATE en el servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el permiso VIEW DATABASE STATE en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.  
  
## <a name="remarks"></a>Comentarios  
 Esta vista devuelve información solo para los trabajos de estadísticas de actualización asincrónica. Para obtener más información acerca de las estadísticas de actualización asincrónica, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 Los valores de **object_id1** a través de **object_id4** dependen del tipo de la solicitud de trabajo. En la tabla siguiente se resume el significado de estas columnas para los diferentes tipos de trabajos.  
  
|Tipo de solicitud|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|Estadísticas de actualización asincrónicas|Id. de tabla o vista|Id. de estadística|No se utiliza|No se utiliza|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el número de trabajos asincrónicos activos en la cola en segundo plano para cada base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica &#40; relacionada con la ejecución Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Estadísticas](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



