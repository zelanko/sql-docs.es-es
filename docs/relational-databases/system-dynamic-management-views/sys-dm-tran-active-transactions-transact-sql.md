---
title: Sys. dm_tran_active_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_transactions
- sys.dm_tran_active_transactions_TSQL
- dm_tran_active_transactions_TSQL
- dm_tran_active_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_transactions dynamic management view
ms.assetid: 154ad6ae-5455-4ed2-b014-e443abe2c6ee
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb72493ddf4e3dbc9b481c97e5473f4f6f6e07d1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82810732"
---
# <a name="sysdm_tran_active_transactions-transact-sql"></a>sys.dm_tran_active_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información sobre transacciones de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para llamar a este método desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use el nombre **Sys. dm_pdw_nodes_tran_active_transactions**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|Identificador de la transacción en el nivel de instancia, no en el de base de datos. Es solo exclusiva en todas las bases de datos dentro de una instancia, pero no es exclusiva en todas las instancias del servidor.|  
|name|**nvarchar(32)**|Nombre de transacción. Se sobrescribe si la transacción está marcada y el nombre marcado reemplaza el nombre de transacción.|  
|transaction_begin_time|**datetime**|Hora en que se ha iniciado la transacción.|  
|transaction_type|**int**|Tipo de transacción.<br /><br /> 1 = Transacciones de lectura/escritura<br /><br /> 2 = Transacción de solo lectura<br /><br /> 3 = Transacción de sistema<br /><br /> 4 = Transacción distribuida|  
|transaction_uow|**uniqueidentifier**|Identificador de la unidad de trabajo (UOW) de la transacción para transacciones distribuidas. MS DTC usa el identificador UOW para trabajar con la transacción distribuida.|  
|transaction_state|**int**|0 = La transacción aún no se ha inicializado completamente.<br /><br /> 1 = La transacción se ha inicializado, pero no ha comenzado.<br /><br /> 2 = La transacción está activa.<br /><br /> 3 = La transacción ha finalizado. Se utiliza para transacciones de solo lectura.<br /><br /> 4 = El proceso de confirmación se ha iniciado en la transacción distribuida. Es solo para transacciones distribuidas. La transacción distribuida aún está activa, pero no se puede realizar ningún otro proceso adicional.<br /><br /> 5 = La transacción está en estado de preparada y esperando una resolución.<br /><br /> 6 = La transacción se ha confirmado.<br /><br /> 7 = La transacción se está revirtiendo.<br /><br /> 8 = La transacción se ha revertido.|  
|transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_state|**int**|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (versión inicial hasta la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299659)).<br /><br /> 1 = ACTIVE<br /><br /> 2 = PREPARED<br /><br /> 3 = COMMITTED<br /><br /> 4 = ABORTED<br /><br /> 5 = RECOVERED|  
|dtc_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_isolation_level|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|filestream_transaction_id|**varbinary(128)**|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (versión inicial hasta la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299659)).<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
  
## <a name="see-also"></a>Consulte también  
 [Sys. dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Sys. dm_tran_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


