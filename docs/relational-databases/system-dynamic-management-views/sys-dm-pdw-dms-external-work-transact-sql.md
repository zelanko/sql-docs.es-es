---
title: Sys.dm_pdw_dms_external_work (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
caps.latest.revision: "5"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7cb91301deb4eb609bc4e856411562266cdc99c8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>Sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]vista del sistema que contiene información sobre todas las medidas de servicio de movimiento de datos (DMS) para las operaciones externas.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar (32)**|Consulta que utiliza este trabajador DMS.<br /><br /> request_id, step_index y dms_step_index forman la clave para esta vista.|Igual que request_id en [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Paso de consulta que está invocando a este trabajador DMS.<br /><br /> request_id, step_index y dms_step_index forman la clave para esta vista.|Igual que step_index en [sys.dm_pdw_request_steps &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Paso actual en el plan DMS.<br /><br /> request_id, step_index y dms_step_index forman la clave para esta vista.|Igual que dms___step_index en [sys.dm_pdw_dms_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Nodo que se está ejecutando el trabajo DMS.|Igual que node_id en [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|Tipo|**nvarchar (60)**|Tipo de operación externa que este nodo está en ejecución.<br /><br /> DIVIDIR el archivo es una operación en un archivo externo de Hadoop que se ha dividido en varios corresponden a las fechas más pequeños.|'ARCHIVO DIVISIÓN'|  
|work_id|**int**|El archivo divide identificador.|Mayor o igual que 0.<br /><br /> Exclusivo para cada nodo de proceso.|  
|input_name|**nvarchar (60)**|Cadena de nombre para la entrada que se va a leer.|Para un archivo de Hadoop, este es el nombre de archivo de Hadoop.|  
|read_location|**bigint**|Desplazamiento de la ubicación de lectura.||  
|estimated_bytes_processed|**bigint**|Número de bytes procesados por este trabajador.|Mayor o igual que 0.|  
|length|**bigint**|Número de bytes en el archivo de división.<br /><br /> Para Hadoop, es el tamaño del bloque HDFS.|Definido por el usuario. El valor predeterminado es 64 MB.|  
|status|**nvarchar (32)**|Estado del trabajador.|Pendiente, procesamiento, realizar, no se pudo, anulado|  
|start_time|**datetime**|Hora en que empezó la ejecución de este trabajo.|Mayor o igual a la hora de inicio del paso de consulta al que pertenece este trabajador. Vea [sys.dm_pdw_request_steps &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Tiempo en el que finalizó la ejecución, no se pudo o se canceló.|NULL para los trabajos en curso o en cola. En caso contrario, es mayor que start_time.|  
|total_elapsed_time|**int**|Tiempo total empleado en ejecución, en milisegundos.|Mayor o igual que 0.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, consulte [valores máximos de vista de sistema](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
