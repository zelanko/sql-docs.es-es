---
title: Sys.dm_exec_external_operations (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_OPERATIONS_TSQL
- DM_EXEC_EXTERNAL_OPERATIONS
- SYS.DM_EXEC_EXTERNAL_OPERATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_external_operations management view
- dm_exec_external_operations management view
ms.assetid: d268217a-85b8-4b7f-9cd1-87865eba2be1
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 63089c5147587c76e70b4e4f00db9dd5e041eef2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39548975"
---
# <a name="sysdmexecexternaloperations-transact-sql"></a>Sys.dm_exec_external_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Captura información sobre las operaciones externas de PolyBase.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Identificador de consulta único asociado con la consulta de PolyBase|Vea el Id. de [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Índice del paso de consulta|Vea step_index en [sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|tipo de operation_|**nvarchar(128)**|Describe una operación de Hadoop o en otra operación externa|'Operación externa de Hadoop'|  
|nombre de operation_|**nvarchar(4000)**|Indica cómo el estado de trabajo como un porcentaje (cuánto es la entrada consumida)|0-1: multiplicado por el factor de 100 (completado)|  
|progreso map_|**float**|Indica cómo el estado de una reducción del trabajo en porcentaje, si existe|0-1: multiplicado por el factor de 100 (completado)|  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas con las vistas de administración dinámica de PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
