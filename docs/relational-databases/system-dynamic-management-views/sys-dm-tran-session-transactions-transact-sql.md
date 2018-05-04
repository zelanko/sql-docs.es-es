---
title: Sys.dm_tran_session_transactions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 33f46110017b80cf066cbb1726ce4793759a7484
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información de correlación para sesiones y transacciones asociadas.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_tran_session_transactions**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|Id. de la sesión en que se ejecuta la transacción.|  
|transaction_id|**bigint**|Identificador de la transacción.|  
|transaction_descriptor|**binary (8)**|Identificador de la transacción utilizado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al comunicarse con el controlador cliente.|  
|enlist_count|**int**|Número de solicitudes activas en la sesión de la transacción.|  
|is_user_transaction|**bit**|1 = Transacción iniciada por una solicitud de usuario.<br /><br /> 0 = Transacción de sistema.|  
|is_local|**bit**|1 = Transacción local.<br /><br /> 0 = Transacción distribuida o transacción de sesión enlazada dada de alta.|  
|is_enlisted|**bit**|1 = Transacción distribuida dada de alta.<br /><br /> 0 = No es una transacción distribuida dada de alta.|  
|is_bound|**bit**|1 = La transacción está activa en la sesión a través de sesiones enlazadas.<br /><br /> 0 = La transacción no está activa en la sesión a través de sesiones enlazadas.|  
|open_transaction_count||La cantidad de transacciones abiertas para cada sesión.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="remarks"></a>Comentarios  
 Por medio de sesiones enlazadas y transacciones distribuidas, una transacción puede ejecutarse en más de una sesión. En tales casos, sys.dm_tran_session_transactions mostrará varias filas para el mismo valor de transaction_id, una por cada sesión en la que se ejecuta la transacción.  
  
 Al ejecutar varias solicitudes en modo de confirmación automática mediante el uso de conjuntos de resultados activos múltiples (MARS), puede tener más de una transacción activa en una sola sesión. En tales casos, sys.dm_tran_session_transactions mostrará varias filas para el mismo valor de session_id, una por cada transacción que se ejecuta en la sesión.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


