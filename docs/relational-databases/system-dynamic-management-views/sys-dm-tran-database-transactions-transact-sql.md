---
title: Sys.dm_tran_database_transactions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_database_transactions
- sys.dm_tran_database_transactions_TSQL
- dm_tran_database_transactions_TSQL
- sys.dm_tran_database_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_database_transactions dynamic management view
ms.assetid: 82a44295-4cbc-4a5b-891a-8ebaf307b8f5
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 192c5637932c5137c26e00ad380584b83a541e09
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39544625"
---
# <a name="sysdmtrandatabasetransactions-transact-sql"></a>sys.dm_tran_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información sobre transacciones en el nivel de base de datos.  
  
> [!NOTE]  
>  Para llamar a esta DMV de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_tran_database_transactions**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|Identificador de la transacción en el nivel de instancia, no en el de base de datos. Es exclusivo solo en todas las bases de datos de una instancia, pero no es exclusivo en todas las instancias del servidor.|  
|database_id|**int**|Id. de la base de datos asociado a la transacción.|  
|database_transaction_begin_time|**datetime**|Hora en la que la base de datos se implica en la transacción. Concretamente, es la hora del primer registro en la base de datos para la transacción.|  
|database_transaction_type|**int**|1 = Transacciones de lectura/escritura<br /><br /> 2 = Transacción de solo lectura<br /><br /> 3 = Transacción de sistema|  
|database_transaction_state|**int**|1 = La transacción no se ha inicializado.<br /><br /> 3 = La transacción se ha inicializado, pero no se han generado registros.<br /><br /> 4 = La transacción ha generado registros.<br /><br /> 5 = La transacción se ha preparado.<br /><br /> 10 = La transacción se ha confirmado.<br /><br /> 11 = La transacción se ha revertido.<br /><br /> 12 = La transacción se está confirmando. (La entrada de registro se está generando, pero no está materializada o persistente.)|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de registros generados en la base de datos para la transacción.|  
|database_transaction_replicate_record_count|**int**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de registros generados en la base de datos para la transacción que se replica.|  
|database_transaction_log_bytes_used|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de bytes usados hasta ahora en el registro de la base de datos para la transacción.|  
|database_transaction_log_bytes_reserved|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de bytes reservados para uso en el registro de la base de datos para la transacción.|  
|database_transaction_log_bytes_used_system|**int**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de bytes usados hasta ahora en el registro de la base de datos para transacciones del sistema en nombre de la transacción.|  
|database_transaction_log_bytes_reserved_system|**int**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de bytes reservados para uso en el registro de la base de datos para transacciones del sistema en nombre de la transacción.|  
|database_transaction_begin_lsn|**numeric(25,0)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de secuencia de registro (LSN) del registro inicial para la transacción en el registro de la base de datos.|  
|database_transaction_last_lsn|**numeric(25,0)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del registro más reciente registrado para la transacción en el registro de la base de datos.|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del punto de retorno más reciente para la transacción en el registro de la base de datos.|  
|database_transaction_commit_lsn|**numeric(25,0)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del registro de confirmación para la transacción en el registro de la base de datos.|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN que se ha revertido más recientemente. Si no ha tenido lugar, el valor será MaxLSN.|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN del siguiente registro que se deshará.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="see-also"></a>Vea también  
 [sys.dm_tran_active_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [sys.dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


