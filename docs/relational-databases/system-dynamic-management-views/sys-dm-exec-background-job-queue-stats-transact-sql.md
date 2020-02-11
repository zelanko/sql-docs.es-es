---
title: Sys. dm_exec_background_job_queue_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue_stats
- sys.dm_exec_background_job_queue_stats
- dm_exec_background_job_queue_stats_TSQL
- sys.dm_exec_background_job_queue_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue_stats dynamic management view
ms.assetid: 27f62ab5-46c4-417e-814d-8d6437034d1c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4707c652b8d47505cceba0be76c53eff2824b728
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68263948"
---
# <a name="sysdm_exec_background_job_queue_stats-transact-sql"></a>sys.dm_exec_background_job_queue_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila que proporciona estadísticas acumuladas para cada trabajo del procesador de consultas enviado para ejecución asincrónica (en segundo plano).  
  
> [!NOTE]  
>  Para llamar a este [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] método [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]desde o, use el nombre **Sys. dm_pdw_nodes_exec_background_job_queue_stats**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**queue_max_len**|**int**|Longitud máxima de la cola.|  
|**enqueued_count**|**int**|Número de solicitudes registradas correctamente en la cola.|  
|**started_count**|**int**|Número de solicitudes que han iniciado la ejecución.|  
|**ended_count**|**int**|Número de solicitudes a las que se ha dado servicio como correctas o erróneas.|  
|**failed_lock_count**|**int**|Número de solicitudes que han generado errores a causa de contención de bloqueos o interbloqueos.|  
|**failed_other_count**|**int**|Número de solicitudes que han generado errores a causa de otras razones.|  
|**failed_giveup_count**|**int**|Número de solicitudes que han generado errores porque se ha alcanzado el límite de reintentos.|  
|**enqueue_failed_full_count**|**int**|Número de intentos de poner en cola erróneos porque la cola está llena.|  
|**enqueue_failed_duplicate_count**|**int**|Número de intentos de poner en cola duplicados.|  
|**elapsed_avg_ms**|**int**|Tiempo promedio transcurrido por solicitud en milisegundos.|  
|**elapsed_max_ms**|**int**|Tiempo transcurrido de la solicitud más grande en milisegundos.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="remarks"></a>Observaciones  
 Esta vista devuelve información solo para los trabajos de estadísticas de actualización asincrónica. Para obtener más información sobre las estadísticas de actualización asincrónica, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="examples"></a>Ejemplos  
  
### <a name="a-determining-the-percentage-of-failed-background-jobs"></a>A. Determinar el porcentaje de trabajos en segundo plano que no han podido completarse  
 En el ejemplo siguiente se devuelve el porcentaje de trabajos en segundo plano que no han podido completarse para todas las consultas ejecutadas.  
  
```  
SELECT   
        CASE ended_count WHEN 0   
                THEN 'No jobs ended'   
                ELSE CAST((failed_lock_count + failed_giveup_count + failed_other_count) / CAST(ended_count AS float) * 100 AS varchar(20))   
        END AS [Percent Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
### <a name="b-determining-the-percentage-of-failed-enqueue-attempts"></a>B. Determinar el porcentaje de intentos de poner en cola que no han tenido éxito  
 En el ejemplo siguiente se devuelve el porcentaje de intentos de poner en cola que no han tenido éxito para todas las consultas ejecutadas.  
  
```  
SELECT   
        CASE enqueued_count WHEN 0   
                THEN 'No jobs posted'   
                ELSE CAST((enqueue_failed_full_count + enqueue_failed_duplicate_count) / CAST(enqueued_count + enqueue_failed_full_count + enqueue_failed_duplicate_count AS float) * 100 AS varchar(20))   
        END AS [Percent Enqueue Failed]  
FROM sys.dm_exec_background_job_queue_stats;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con la ejecución &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


