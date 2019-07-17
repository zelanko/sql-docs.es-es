---
title: Sys.dm_tran_session_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 148cab2122a907c138a2bd74c5f3403d231e2793
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262668"
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información de correlación para sesiones y transacciones asociadas.  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_tran_session_transactions**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
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
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   

## <a name="remarks"></a>Comentarios  
 Por medio de sesiones enlazadas y transacciones distribuidas, una transacción puede ejecutarse en más de una sesión. En tales casos, sys.dm_tran_session_transactions mostrará varias filas para el mismo valor de transaction_id, una por cada sesión en la que se ejecuta la transacción.  
  
 Al ejecutar varias solicitudes en modo de confirmación automática mediante el uso de conjuntos de resultados activos múltiples (MARS), puede tener más de una transacción activa en una sola sesión. En tales casos, sys.dm_tran_session_transactions mostrará varias filas para el mismo valor de session_id, una por cada transacción que se ejecuta en la sesión.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


