---
title: sys.pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 067a39c807b546bc8364bab05d0423f86407a625
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047228"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre la copia de seguridad en curso y finalizada y en las operaciones de restauración [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]y acerca de la copia de seguridad en curso y completada, restauración y las operaciones de carga en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. La información se conserva entre reinicios del sistema.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador único para una copia de seguridad específica, restauración o de ejecución de carga.<br /><br /> Clave para esta vista.||  
|NAME|**nvarchar(255)**|NULL para la carga. Nombre opcional para la copia de seguridad o restauración.||  
|submit_time|**datetime**|Tiempo que se envió la solicitud.||  
|start_time|**datetime**|Tiempo de la operación iniciada.||  
|end_time|**datetime**|Hora completado, error o se canceló la operación.||  
|total_elapsed_time|**int**|Tiempo total transcurrido entre start_time y la hora actual, o entre start_time y end_time para completado, cancelados o fallidos ejecuciones.|Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido al desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a 24,8 días.|  
|operation_type|**nvarchar(16)**|El tipo de carga.|'BACKUP', 'LOAD', 'RESTORE'|  
|mode|**nvarchar(16)**|El modo en el tipo de ejecución.|Para obtener más operation_type = **copia de seguridad**<br />**DIFERENCIAL**<br />**FULL**<br /><br /> Para obtener más operation_type = **carga**<br />**ANEXAR**<br />**VOLVER A CARGAR**<br />**UPSERT**<br /><br /> Para obtener más operation_type = **restaurar**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|Nombre de la base de datos que es el contexto de esta operación||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|Id. de usuario que solicita la operación.||  
|session_id|**nvarchar(32)**|Identificador de la sesión realiza la operación.|Consulte session_id en [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar(32)**|Identificador de la solicitud que realiza la operación. Para las cargas, ésta es la solicitud última o actual asociada con esta carga...|Vea request_id en [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar(16)**|Estado de la ejecución.|'CANCELAR', 'COMPLETADO', 'ERROR', 'QUEUED', 'EJECUTANDO'|  
|Progreso|**int**|Porcentaje completado.|de 0 a 100|  
|comando|**nvarchar(4000)**|Texto del comando enviado por el usuario.|Se truncará si hay más de 4.000 caracteres (contando espacios).|  
|rows_processed|**bigint**|Número de filas procesadas como parte de esta operación.||  
|rows_rejected|**bigint**|Número de filas rechazadas como parte de esta operación.||  
|rows_inserted|**bigint**|Número de filas insertadas en las tablas de base de datos como parte de esta operación.||  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
