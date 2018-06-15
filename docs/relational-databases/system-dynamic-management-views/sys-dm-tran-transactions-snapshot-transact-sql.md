---
title: Sys.dm_tran_transactions_snapshot (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7e862da4552d605993a5dde7913fe1bec5856603
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464321"
---
# <a name="sysdmtrantransactionssnapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una tabla virtual para el **sequence_number** de transacciones que están activas cuando la transacción de instantáneas se inicia. La información que devuelve esta vista le puede ayudar a realizar las siguientes acciones:  
  
-   Buscar el número de transacciones de instantáneas activas actualmente.  
  
-   Identificar modificaciones de datos pasadas por alto por una transacción de instantáneas determinada. Si existe una transacción activa cuando comienza una transacción de instantáneas, todas las modificaciones de datos de la primera, incluso después de confirmarla, se pasan por alto en la transacción de instantáneas.  
  
 Por ejemplo, considere el siguiente resultado de **sys.dm_tran_transactions_snapshot**:  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 La columna `transaction_sequence_num` identifica el número de secuencia de transacción (XSN) de las transacciones de instantáneas actuales. El resultado muestra dos: `59` y `60`. La columna `snapshot_sequence_num` identifica el número de secuencia de las transacciones activas al iniciarse cada transacción de instantáneas.  
  
 El resultado muestra que la transacción de instantáneas XSN-59 comienza mientras se ejecutan dos transacciones activas, XSN-57 y XSN-58. Si XSN-57 o XSN-58 realizan modificaciones de datos, XSN-59 pasa por alto los cambios y utiliza versiones de fila para conservar una vista coherente de la base de datos desde el punto de vista transaccional.  
  
 La transacción de instantáneas XSN-60 pasa por alto las modificaciones efectuadas por XSN-57 y XSN-58 y también por XSN 59.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dm_tran_transactions_snapshot  
```  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Número de secuencia de transacción (XSN) de una transacción de instantáneas.|  
|**snapshot_id**|**int**|Id. de instantánea de cada instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] iniciada con lectura confirmada y que utiliza las versiones de fila. Este valor se utiliza para generar una vista de la base de datos transaccionalmente coherente que admita cada consulta que se ejecute en una lectura confirmada utilizando las versiones de fila.|  
|**snapshot_sequence_num**|**bigint**|Número de secuencia de una transacción que estaba activa cuando se inició la transacción de instantánea.|  
  
## <a name="permissions"></a>Permissions

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="remarks"></a>Comentarios  
 Cuando se inicia una transacción de instantáneas, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] registra todas las transacciones activas en ese momento determinado. **Sys.dm_tran_transactions_snapshot** proporciona esta información de todas las transacciones de instantáneas actualmente activas.  
  
 Cada transacción se identifica mediante un número de secuencia que se asigna cuando se inicia la transacción. Las transacciones empiezan en el momento en que se ejecuta una instrucción BEGIN TRANSACTION o BEGIN WORK. No obstante, [!INCLUDE[ssDE](../../includes/ssde-md.md)] asigna el número de secuencia de la transacción con la ejecución de la primera instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] que tiene acceso a datos después de la instrucción BEGIN TRANSACTION o BEGIN WORK. Los números de secuencia de la transacción se incrementan de uno en uno.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

