---
description: MSrepl_commands (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8596aefdaecce0e7d39033b2a484ebfe6a4f46b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540293"
---
# <a name="msrepl_commands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
|**command**|**varbinary (1024)**|El valor del comando.|  
|**hashkey**|**int**|Solo para uso interno.|  
|**originator_lsn**|**varbinary(16)**|Identifica el LSN del comando en la publicación de origen. Se utiliza en la replicación transaccional punto a punto.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
