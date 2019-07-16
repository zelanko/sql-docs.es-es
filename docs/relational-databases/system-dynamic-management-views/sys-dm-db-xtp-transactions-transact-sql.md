---
title: sys.dm_db_xtp_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_transactions
- sys.dm_db_xtp_transactions_TSQL
- dm_db_xtp_transactions
- dm_db_xtp_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_transactions dynamic management view
ms.assetid: 5c1a0a7a-e851-4b6f-8dfd-c9655fbf5a51
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc5f12e50c1e7a7d639acdbf9a244406ce9366c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097935"
---
# <a name="sysdmdbxtptransactions-transact-sql"></a>sys.dm_db_xtp_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Notifica las transacciones activas en el motor de base de datos de OLTP en memoria.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
    
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|xtp_transaction_id|**bigint**|Identificador interno para esta transacción en el administrador de transacciones de XTP.|  
|transaction_id|**bigint**|El identificador de la transacción. Se combina con el identificador de transacción en las otras DMV relacionadas con la transacción, como sys.dm_tran_active_transactions.<br /><br /> 0 para las transacciones solo de XTP, como las transacciones iniciadas por procedimientos almacenados compilados de forma nativa.|  
|session_id|**smallint**|Identificador de la sesión que ejecuta esta transacción. Se combina con sys.dm_exec_sessions.|  
|begin_tsn|**bigint**|Número de serie de transacciones de inicio de la transacción.|  
|end_tsn|**bigint**|Número de serie de transacción de fin de la transacción.|  
|state|**int**|Estado de la transacción:<br /><br /> 0=ACTIVA<br /><br /> 1=CONFIRMADA<br /><br /> 2=CANCELADA<br /><br /> 3=VALIDANDO|  
|state_desc|**nvarchar**|Descripción del estado de la transacción.|  
|resultado|**int**|El resultado de esta transacción. Los posibles valores son los siguientes.<br /><br /> 0 - EN CURSO<br /><br /> 1 - CORRECTO<br /><br /> 2 - ERROR<br /><br /> 3 - CONFIRMAR DEPENDENCIA<br /><br /> 4 - ERROR EN LA VALIDACIÓN (RR)<br /><br /> 5 - ERROR EN LA VALIDACIÓN (SR)<br /><br /> 6 - REVERTIR|  
|result_desc|**nvarchar**|El resultado de esta transacción. Los posibles valores son los siguientes.<br /><br /> EN CURSO<br /><br /> CORRECTA<br /><br /> error<br /><br /> CONFIRMAR DEPENDENCIA<br /><br /> ERROR EN LA VALIDACIÓN (RR)<br /><br /> ERROR EN LA VALIDACIÓN (SR)<br /><br /> ROLLBACK|  
|last_error|**int**|Exclusivamente para uso interno|  
|is_speculative|**bit**|Exclusivamente para uso interno|  
|is_prepared|**bit**|Exclusivamente para uso interno|  
|is_delayed_durability|**bit**|Exclusivamente para uso interno|  
|memory_address|**varbinary**|Exclusivamente para uso interno|  
|database_address|**varbinary**|Exclusivamente para uso interno|  
|thread_id|**int**|Exclusivamente para uso interno|  
|read_set_row_count|**int**|Exclusivamente para uso interno|  
|write_set_row_count|**int**|Exclusivamente para uso interno|  
|scan_set_count|**int**|Exclusivamente para uso interno|  
|savepoint_garbage_count|**int**|Exclusivamente para uso interno|  
|log_bytes_required|**bigint**|Exclusivamente para uso interno|  
|count_of_allocations|**int**|Exclusivamente para uso interno|  
|allocated_bytes|**int**|Exclusivamente para uso interno|  
|reserved_bytes|**int**|Exclusivamente para uso interno|  
|commit_dependency_count|**int**|Exclusivamente para uso interno|  
|commit_dependency_total_attempt_count|**int**|Exclusivamente para uso interno|  
|scan_area|**int**|Exclusivamente para uso interno|  
|scan_area_desc|**nvarchar**|Exclusivamente para uso interno|  
|scan_location|**int**|Exclusivamente para uso interno.|  
|dependent_1_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_2_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_3_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_4_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_5_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_6_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_7_address|**varbinary(8)**|Exclusivamente para uso interno|  
|dependent_8_address|**varbinary(8)**|Exclusivamente para uso interno|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de tabla optimizado para memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
