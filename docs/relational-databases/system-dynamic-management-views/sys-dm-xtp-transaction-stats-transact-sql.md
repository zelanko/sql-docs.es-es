---
title: Sys.dm_xtp_transaction_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xtp_transaction_stats_TSQL
- dm_xtp_transaction_stats
- sys.dm_xtp_transaction_stats_TSQL
- sys.dm_xtp_transaction_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_transaction_stats dynamic management view
ms.assetid: 9389f48d-0de5-47bd-9821-4db8f04504e4
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 82cd1561509dd25ebe7f7dcbcfe6914417dc527f
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467381"
---
# <a name="sysdmxtptransactionstats-transact-sql"></a>sys.dm_xtp_transaction_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Notifica las estadísticas de las transacciones que se han ejecutado desde que el servidor se inició.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|total_count|**bigint**|El número total de transacciones que se han ejecutado en el motor de base de datos de OLTP en memoria.|  
|read_only_count|**bigint**|Número de transacciones de solo lectura.|  
|total_aborts|**bigint**|El número total de transacciones que se anularon, bien mediante intervención del usuario o del sistema.|  
|user_aborts|**bigint**|Número de interrupciones iniciadas por el sistema. Por ejemplo, debido a conflictos de escritura, errores de validación o errores de dependencia.|  
|validation_failures|**bigint**|Número de veces que una transacción se ha anulado debido a un error de validación.|  
|dependencies_taken|**bigint**|Exclusivamente para uso interno.|  
|dependencies_failed|**bigint**|Número de veces que una transacción se anula debido a que una transacción de la que dependía se anula.|  
|savepoint_create|**bigint**|El número de puntos de retorno creados. Se crea un nuevo punto de retorno para cada bloque atomic.|  
|savepoint_rollbacks|**bigint**|El número de reversiones a un punto de retorno anterior.|  
|savepoint_refreshes|**bigint**|Exclusivamente para uso interno.|  
|log_bytes_written|**bigint**|Número total de bytes escritos en las entradas del registro de OLTP en memoria.|  
|log_IO_count|**bigint**|Número total de transacciones que requieren E/S del registro. Solo se tienen en cuenta las transacciones en tablas perdurables.|  
|phantom_scans_started|**bigint**|Exclusivamente para uso interno.|  
|phatom_scans_retries|**bigint**|Exclusivamente para uso interno.|  
|phantom_rows_touched|**bigint**|Exclusivamente para uso interno.|  
|phantom_rows_expiring|**bigint**|Exclusivamente para uso interno.|  
|phantom_rows_expired|**bigint**|Exclusivamente para uso interno.|  
|phantom_rows_expired_removed|**bigint**|Exclusivamente para uso interno.|  
|scans_started|**bigint**|Exclusivamente para uso interno.|  
|scans_retried|**bigint**|Exclusivamente para uso interno.|  
|rows_returned|**bigint**|Exclusivamente para uso interno.|  
|rows_touched|**bigint**|Exclusivamente para uso interno.|  
|rows_expiring|**bigint**|Exclusivamente para uso interno.|  
|rows_expired|**bigint**|Exclusivamente para uso interno.|  
|rows_expired_removed|**bigint**|Exclusivamente para uso interno.|  
|rows_inserted|**bigint**|Exclusivamente para uso interno.|  
|rows_updated|**bigint**|Exclusivamente para uso interno.|  
|rows_deleted|**bigint**|Exclusivamente para uso interno.|  
|write_conflicts|**bigint**|Exclusivamente para uso interno.|  
|unique_constraint_violations|**bigint**|Número total de infracciones de la restricción UNIQUE.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de tablas optimizadas en memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
