---
title: sys.dm_pdw_dms_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9e79803a1c06a78f67a37a6a669af1c5ab4683f5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021577"
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] vista del sistema que contiene información sobre todas las medidas de servicio de movimiento de datos (DMS) para realizar operaciones externas.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta que usa este trabajador DMS.<br /><br /> request_id step_index y dms_step_index forman la clave para esta vista.|Igual que request_id en [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Paso de consulta que se está invocando a este trabajo DMS.<br /><br /> request_id step_index y dms_step_index forman la clave para esta vista.|Igual que step_index en [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Paso actual en el plan DMS.<br /><br /> request_id step_index y dms_step_index forman la clave para esta vista.|Igual que dms___step_index en [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Nodo que se está ejecutando el trabajo DMS.|Igual que node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|Tipo|**nvarchar(60)**|Tipo de operación externa que este nodo se está ejecutando.<br /><br /> DIVIDIR el archivo es una operación en un archivo externo de Hadoop que se ha dividido en varios caídas más pequeños.|'DIVISIÓN DE ARCHIVO'|  
|work_id|**int**|El archivo de dividir el identificador.|Mayor o igual que 0.<br /><br /> Único para cada nodo de proceso.|  
|input_name|**nvarchar(60)**|Nombre para el que se está leyendo de la entrada de cadena.|Para un archivo de Hadoop, esto es el nombre de archivo de Hadoop.|  
|read_location|**bigint**|Desplazamiento de la ubicación de lectura.||  
|estimated_bytes_processed|**bigint**|Número de bytes procesados por este trabajador.|Mayor o igual que 0.|  
|length|**bigint**|Número de bytes en el archivo de división.<br /><br /> Para Hadoop, esto es el tamaño del bloque de HDFS.|Definido por el usuario. El valor predeterminado es 64 MB.|  
|status|**nvarchar(32)**|Estado del trabajo.|Pendiente, en proceso, terminado, error, anulado|  
|start_time|**datetime**|Hora en que empezó la ejecución de este trabajador.|Mayor o igual a la hora de inicio de este trabajo pertenece el paso de consulta. See [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Hora a la que finalizó la ejecución, no se pudo o se ha cancelado.|NULL para los trabajadores en curso o en cola. En caso contrario, es mayor que start_time.|  
|total_elapsed_time|**int**|Tiempo total empleado en ejecución, en milisegundos.|Mayor o igual que 0.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a 24,8 días.|  
  
 Para obtener información sobre el número máximo de filas retenidas por esta vista, consulte [valores máximos de la vista del sistema](https://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
