---
description: Sys. dm_exec_external_operations (Transact-SQL)
title: Sys. dm_exec_external_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bbae0f3fda0b96df4f27c7f6464d03d296dc7c0
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283596"
---
# <a name="sysdm_exec_external_operations-transact-sql"></a>Sys. dm_exec_external_operations (Transact-SQL)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  Captura información acerca de las operaciones externas de polybase.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Identificador de consulta único asociado a la consulta de polybase|Vea ID en [Sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Índice del paso de consulta|Vea step_index en [Sys. dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|tipo de operation_|**nvarchar(128)**|Describe una operación de Hadoop u otra operación externa|' Operación de Hadoop externa '|  
|nombre del operation_|**nvarchar(4000)**|Indica cómo se usa el estado de trabajo en porcentaje (cuánto es la entrada consumida)|0-1: multiplicado por factor 100 (completado)|  
|progreso de map_|**float**|Indica cómo se muestra el estado de un trabajo de reducción en porcentaje, si lo hay.|0-1: multiplicado por factor 100 (completado)|  
  
## <a name="see-also"></a>Consulte también  
 [Solución de problemas de polybase con vistas de administración dinámica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
