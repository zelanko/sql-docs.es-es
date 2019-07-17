---
title: sys.dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09e760bac8e31ba9c78b9809a12f8d595b7ebd05
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263930"
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada trabajo del procesador de consultas que está programado para ejecución asincrónica (en segundo plano).  
  
> **NOTA** Al llamarlo desde **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** o **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** , use el nombre **sys.dm_pdw_nodes_exec_background_job_queue**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
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
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   
  
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
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



