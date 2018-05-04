---
title: MScached_peer_lsns (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 31e7f3edbed18158ceb2343796796b9491c252fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mscachedpeerlsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MScached_peer_lsns** tabla sirve para realizar un seguimiento de los valores LSN en el registro de transacciones que se usan para determinar los comandos para volver a un suscriptor determinado en la replicación punto a punto. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Id. del Agente de distribución.|  
|**originador**|**sysname**|Nombre del publicador de origen.|  
|**originator_db**|**sysname**|Nombre de la base de datos de publicación de origen.|  
|**originator_publication_id**|**int**|Identifica la publicación de origen.|  
|**originator_db_version**|**int**|Identifica el número de versión de la base de datos de origen.|  
|**originator_lsn**|**varbinary (16)**|LSN de la transacción de origen.|  
  
## <a name="remarks"></a>Comentarios  
 Los valores de LSN solo se utilizan inmediatamente después de la inserción, y no tienen un significado duradero en el sistema.  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
