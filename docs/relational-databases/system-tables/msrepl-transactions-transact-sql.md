---
title: MSrepl_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_transactions_TSQL
- MSrepl_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_transactions system table
ms.assetid: d325288d-47ae-4488-8799-122f7ab43459
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 642a6331f8466a37dbb3531d9d2e0052638bdbb6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752664"
---
# <a name="msrepl_transactions-transact-sql"></a>MSrepl_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSrepl_transactions** contiene una fila por cada transacción replicada. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|El Id. de la base de datos del publicador.|  
|**xact_id**|**varbinary(16)**|El Id. de la transacción.|  
|**xact_seqno**|**varbinary(16)**|El número de secuencia de la transacción.|  
|**entry_time**|**datetime**|La hora a la que la transacción entró en la base de datos de distribución.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
