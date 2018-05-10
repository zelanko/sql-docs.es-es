---
title: Sys.dm_pdw_hadoop_operations (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 846bf96e44af99a00a1429b5280206bfbeb87601
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>Sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila por cada trabajo asignar/reducir es aplicar en Hadoop como parte de la ejecución una [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] consulta en una tabla externa de Hadoop. Cada trabajo asignar/reducir representa uno de los predicados de la consulta. Solo se utiliza cuando la aplicación del predicado está habilitada para las consultas en tablas externas de Hadoop.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador para esta operación Hadoop externa.|Igual que el Id. de [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice del paso de consulta que hace referencia a esta operación de Hadoop.|Igual que step_index en [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Describe el tipo de operación externa.|'Operación Hadoop externo'|  
|operation_name|**nvarchar(4000)**|Id. de trabajo para un trabajo asignar/reducir. Se devuelve hadoop después [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] envía el trabajo.||  
|map_progress|**float**|El porcentaje de datos de entrada que se ha consumido hasta ahora por el trabajo de asignación.|Número entre y, incluso, 0 y 100 de punto flotante.|  
|reduce_progress|**int**|El porcentaje del trabajo reduce que ha finalizado...|Número entre y, incluso, 0 y 100 de punto flotante.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
