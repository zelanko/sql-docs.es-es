---
title: MSpeer_topologyresponse (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 524442e677bddcebb8e3d773ace4bf29448fb6a8
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532445"
---
# <a name="mspeertopologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Se utiliza en la replicación punto a punto para almacenar la respuesta de cada nodo a una solicitud del estado de la topología. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifica una entrada de solicitud de estado de topología en el [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) tabla.|  
|peer|**sysname**|Nombre de la instancia del servidor que generó la respuesta.|  
|peer_version|**int**|Identifica el número de versión del publicador.|  
|peer_db|**sysname**|Base de datos de suscripciones del mismo nivel que generó la respuesta.|  
|originator_id|**int**|Identifica cada nodo de la topología para detectar conflictos. Para obtener más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Período de tiempo, en días, durante el cual los metadatos se almacenan en tablas conflictivas.|  
|received_date|**datetime**|Momento en el que se recibió la solicitud de topología.|  
|connection_info|**xml**|Información sobre el nodo que respondió a la solicitud.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
