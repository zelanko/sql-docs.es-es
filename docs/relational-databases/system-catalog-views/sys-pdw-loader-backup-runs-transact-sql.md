---
title: Sys.pdw_loader_backup_runs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ebdadbeeba70444eda300f44480e49fa9992d29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>Sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de la copia de seguridad en curso y completada y las operaciones de restauración en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]y copia de seguridad en curso y completada, restauración así como operaciones de carga en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. La información se conserva entre reinicios del sistema.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador único de una copia de seguridad específica, restaurar o de ejecución.<br /><br /> Clave para esta vista.||  
|name|**nvarchar(255)**|NULL para la carga. Nombre opcional para copia de seguridad o restauración.||  
|submit_time|**datetime**|Hora que se envió la solicitud.||  
|start_time|**datetime**|Tiempo de la operación iniciada.||  
|end_time|**datetime**|Hora de la operación completado, error o se canceló.||  
|total_elapsed_time|**int**|Tiempo total transcurrido entre start_time y hora actual, o entre start_time y end_time para completado, cancelados o ha fallado ejecuciones.|Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido a desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|operation_type|**nvarchar(16)**|El tipo de carga.|'COPIA DE SEGURIDAD', 'CARGA', 'RESTORE'|  
|mode|**nvarchar(16)**|El modo en el tipo de ejecución.|Para operation_type = **copia de seguridad**<br />**DIFERENCIAL**<br />**FULL**<br /><br /> Para operation_type = **carga**<br />**ANEXAR**<br />**VOLVER A CARGAR**<br />**UPSERT**<br /><br /> Para operation_type = **restaurar**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|Nombre de la base de datos que es el contexto de esta operación||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|Id. del usuario que solicita la operación.||  
|session_id|**nvarchar (32)**|Identificador de la sesión que se realiza la operación.|Vea "session_ID" en [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar (32)**|Identificador de la solicitud que se realiza la operación. Para las cargas, ésta es la solicitud última o actual asociada con esta carga...|Vea request_id en [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar(16)**|Estado de la ejecución.|'CANCELAR', 'COMPLETADA', 'ERROR', 'QUEUED', 'EJECUTANDO'|  
|progreso|**int**|Porcentaje completado.|de 0 a 100|  
|comando|**nvarchar(4000)**|Texto completo del comando enviado por el usuario.|Se truncará si es superior a 4000 caracteres (contando espacios).|  
|rows_processed|**bigint**|Número de filas procesadas como parte de esta operación.||  
|rows_rejected|**bigint**|Número de filas rechazada como parte de esta operación.||  
|rows_inserted|**bigint**|Número de filas insertadas en las tablas de base de datos como parte de esta operación.||  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
