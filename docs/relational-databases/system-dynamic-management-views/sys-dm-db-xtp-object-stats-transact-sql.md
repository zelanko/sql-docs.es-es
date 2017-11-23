---
title: Sys.dm_db_xtp_object_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_object_stats_TSQL
- sys.dm_db_xtp_object_stats
- dm_db_xtp_object_stats
- sys.dm_db_xtp_object_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_xtp_object_stats dynamic management view
ms.assetid: 07300b59-3cab-4d3e-8138-5ea8f584f88f
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b07eb152c42c2f9c991d99ff6e3256b62d1cef8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbxtpobjectstats-transact-sql"></a>sys.dm_db_xtp_object_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Indica el número de filas afectadas por operaciones en cada uno de los objetos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] desde el último reinicio de la base de datos. Las estadísticas se actualizan cuando se ejecuta la operación, independientemente de si la transacción se confirma o se revirtió.  
  
 sys.dm_db_xtp_object_stats puede ayudarle a identificar las tablas optimizadas para memoria que más cambian. Puede decidir quitar de la tabla los índices que no se usan o que usan con poca frecuencia, ya que cada índice afecta al rendimiento. Si hay índices hash, debe volver a evaluar periódicamente el número de depósitos. Para obtener más información, consulte [determinar el número correcto de depósitos para los índices Hash](http://msdn.microsoft.com/library/6d1ac280-87db-4bd8-ad43-54353647d8b5).  
  
 sys.dm_db_xtp_object_stats puede ayudarle a identificar qué tablas optimizadas para memoria incurren en conflictos de escritura contra escritura, lo que puede afectar al rendimiento de la aplicación. Por ejemplo, si tiene lógica de reintento de transacciones, puede que sea necesario ejecutar más de una vez la misma instrucción. También puede usar esta información para identificar las tablas (y por tanto la lógica de negocios) que necesitan un control de errores de escritura contra escritura.  
  
 La vista contiene una fila por cada tabla optimizada en memoria en la base de datos.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|Id. del objeto.|  
|row_insert_attempts|**bigint**|Número de filas insertadas en la tabla desde el último reinicio de la base de datos por las transacciones confirmadas y anuladas.|  
|row_update_attempts|**bigint**|Número de filas actualizadas en la tabla desde el último reinicio de la base de datos por las transacciones confirmadas y anuladas.|  
|row_delete_attempts|**bigint**|Número de filas eliminadas de la tabla desde el último reinicio de la base de datos por las transacciones confirmadas y anuladas.|  
|write_conflicts|**bigint**|Número de conflictos de escritura que se produjeron desde el último reinicio de la base de datos.|  
|unique_constraint_violations|**bigint**|Número de infracciones de la restricción UNIQUE que se han producido desde el último reinicio de la base de datos.|  
|object_address|**varbinary (8)**|Exclusivamente para uso interno.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW DATABASE STATE en la base de datos actual.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de la tabla optimizada en memoria &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
