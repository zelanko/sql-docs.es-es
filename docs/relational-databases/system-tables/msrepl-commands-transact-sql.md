---
title: MSrepl_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: stevestein
ms.author: sstein
ms.openlocfilehash: c02a0201483617966d7d1c8aadfbad4ab39971e3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127431"
---
# <a name="msrepl_commands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSrepl_commands** contiene filas de comandos replicados. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|El Id. de la base de datos del publicador.|  
|**xact_seqno**|**varbinary(16)**|El número de secuencia de la transacción.|  
|**type**|**int**|Tipo de comando.|  
|**article_id**|**int**|Id. del artículo.|  
|**originator_id**|**int**|Id. del originador.|  
|**command_id**|**int**|Id. del comando.|  
|**partial_command**|**bit**|Indica si se trata de un comando parcial o no.|  
|**Command**|**varbinary (1024)**|El valor del comando.|  
|**hashkey**|**int**|Solo para uso interno.|  
|**originator_lsn**|**varbinary(16)**|Identifica el LSN del comando en la publicación de origen. Se utiliza en la replicación transaccional punto a punto.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
