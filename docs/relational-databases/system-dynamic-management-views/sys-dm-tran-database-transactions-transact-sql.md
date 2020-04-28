---
title: Sys. dm_tran_database_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a01dc7df9a8269190ae1c1c3cf05de3adaecc662
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73982314"
---
# <a name="sysdm_tran_database_transactions-transact-sql"></a>sys.dm_tran_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información sobre transacciones en el nivel de base de datos.  
  
> [!NOTE]  
>  Para llamar a esta DMV [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] desde [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]o, use el nombre **Sys. dm_pdw_nodes_tran_database_transactions**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|Identificador de la transacción en el nivel de instancia, no en el de base de datos. Es exclusivo solo en todas las bases de datos de una instancia, pero no es exclusivo en todas las instancias del servidor.|  
|database_id|**int**|Id. de la base de datos asociado a la transacción.|  
|database_transaction_begin_time|**datetime**|Hora en la que la base de datos se implica en la transacción. Concretamente, es la hora del primer registro en la base de datos para la transacción.|  
|database_transaction_type|**int**|1 = Transacciones de lectura/escritura<br /><br /> 2 = Transacción de solo lectura<br /><br /> 3 = Transacción de sistema|  
|database_transaction_state|**int**|1 = La transacción no se ha inicializado.<br /><br /> 3 = La transacción se ha inicializado, pero no se han generado registros.<br /><br /> 4 = La transacción ha generado registros.<br /><br /> 5 = La transacción se ha preparado.<br /><br /> 10 = La transacción se ha confirmado.<br /><br /> 11 = La transacción se ha revertido.<br /><br /> 12 = La transacción se está confirmando. (La entrada de registro se está generando, pero no se ha materializado ni conservado).|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de registros generados en la base de datos para la transacción.|  
|database_transaction_replicate_record_count|**int**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de entradas de registro generadas en la base de datos para la transacción replicada.|  
|database_transaction_log_bytes_used|**bigint**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de bytes usados hasta ahora en el registro de la base de datos para la transacción.|  
|database_transaction_log_bytes_reserved|**bigint**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de bytes reservados para uso en el registro de la base de datos para la transacción.|  
|database_transaction_log_bytes_used_system|**int**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de bytes usados hasta ahora en el registro de la base de datos para transacciones del sistema en nombre de la transacción.|  
|database_transaction_log_bytes_reserved_system|**int**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de bytes reservados para uso en el registro de la base de datos para transacciones del sistema en nombre de la transacción.|  
|database_transaction_begin_lsn|**numeric(25,0)**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> Número de secuencia de registro (LSN) del registro inicial para la transacción en el registro de la base de datos.|  
|database_transaction_last_lsn|**numeric(25,0)**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> LSN del registro más reciente registrado para la transacción en el registro de la base de datos.|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> LSN del punto de retorno más reciente para la transacción en el registro de la base de datos.|  
|database_transaction_commit_lsn|**numeric(25,0)**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> LSN del registro de confirmación para la transacción en el registro de la base de datos.|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> LSN que se ha revertido más recientemente. Si no se realiza ninguna reversión, el valor es MaxLSN.|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**Válido para** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.<br /><br /> LSN del siguiente registro que se deshará.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="see-also"></a>Consulte también  
 [Sys. dm_tran_active_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [Sys. dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


