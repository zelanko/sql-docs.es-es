---
title: Sys. dm_db_xtp_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e6370f4cbfcbc38478e562c3b74ff24ffde962f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68026835"
---
# <a name="sysdm_db_xtp_index_stats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Contiene las estadísticas recopiladas desde el último reinicio de la base de datos.  
  
 Para obtener más información, vea [OLTP en memoria &#40;la optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) y [directrices para usar índices en las tablas optimizadas para memoria](https://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b).  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**BIGINT**|Id. del objeto al que pertenece este índice.|  
|xtp_object_id|**BIGINT**|IDENTIFICADOR interno correspondiente a la versión actual del objeto.<br /><br /> Nota: se aplica [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]a.|  
|index_id|**BIGINT**|Id. del índice. El index_id es exclusivo solo dentro del objeto.|  
|scans_started|**BIGINT**|Número de recorridos de índice OLTP en memoria realizados. Cada selección, inserción, actualización o eliminación requiere un recorrido de índice.|  
|scans_retried|**BIGINT**|Número de recorridos de índice que tuvieron que reintentarse.|  
|rows_returned|**BIGINT**|Número de filas devueltas acumulado desde que se creó la tabla o desde el inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rows_touched|**BIGINT**|Número acumulado de filas a las que se tuvo acceso desde que se creó la tabla o desde el inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rows_expiring|**BIGINT**|Exclusivamente para uso interno.|  
|rows_expired|**BIGINT**|Exclusivamente para uso interno.|  
|rows_expired_removed|**BIGINT**|Exclusivamente para uso interno.|  
|phantom_scans_started|**BIGINT**|Exclusivamente para uso interno.|  
|phatom_scans_retries|**BIGINT**|Exclusivamente para uso interno.|  
|phantom_rows_touched|**BIGINT**|Exclusivamente para uso interno.|  
|phantom_expiring_rows_encountered|**BIGINT**|Exclusivamente para uso interno.|  
|phantom_expired_rows_encountered|**BIGINT**|Exclusivamente para uso interno.|  
|phantom_expired_removed_rows_encountered|**BIGINT**|Exclusivamente para uso interno.|  
|phantom_expired_rows_removed|**BIGINT**|Exclusivamente para uso interno.|  
|object_address|**varbinary(8**|Exclusivamente para uso interno.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE en la base de datos actual.  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de tablas optimizadas para memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
