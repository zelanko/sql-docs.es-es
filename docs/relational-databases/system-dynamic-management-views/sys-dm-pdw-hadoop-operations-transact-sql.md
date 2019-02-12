---
title: sys.dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 11c8cc0797bafff6cc8c38bffb55023be00003a9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023967"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada trabajo asignar/reducir que se transferirá a Hadoop como parte de la ejecución un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] consulta en una tabla externa de Hadoop. Cada trabajo asignar/reducir representa uno de los predicados de la consulta. Sólo se utiliza cuando la aplicación del predicado está habilitada para las consultas en tablas externas de Hadoop.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador para esta operación externa de Hadoop.|Igual que el Id. de [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice del paso de consulta que hace referencia a esta operación de Hadoop.|Igual que step_index en [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Describe el tipo de operación externa.|'Operación externa de Hadoop'|  
|operation_name|**nvarchar(4000)**|El Id. de trabajo para un trabajo asignar/reducir. Se devuelve mediante Hadoop después [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] envía el trabajo.||  
|map_progress|**float**|El porcentaje de datos de entrada del trabajo de asignación se ha consumido hasta ahora.|Número entre y, incluso, 0 y 100 de punto flotante.|  
|reduce_progress|**int**|El porcentaje del trabajo de reducción que se ha completado...|Número entre y, incluso, 0 y 100 de punto flotante.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
