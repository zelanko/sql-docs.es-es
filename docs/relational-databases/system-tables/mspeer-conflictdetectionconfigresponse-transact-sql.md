---
title: MSpeer_conflictdetectionconfigresponse (T-SQL)
description: Describe el MSPeer_conflictdetectionconfigureresponse procedimiento almacenado que se usa en la replicación punto a punto para almacenar la respuesta de cada nodo a una solicitud de configuración de toda la topología.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ed3a127d2527b35c301ab7f3d05305c4f8d2ced
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322136"
---
# <a name="mspeer_conflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza en la replicación punto a punto para almacenar la respuesta de cada nodo a una solicitud de configuración de toda la topología. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|request_id|**Inter**|Identifica una entrada de solicitud de configuración de conflictos en la tabla [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md) .|  
|peer_node|**sysname**|Nombre de la instancia del servidor que generó la respuesta.|  
|peer_db|**sysname**|Base de datos de suscripciones en el elemento del mismo nivel que generó la respuesta.|  
|peer_version|**sysname**|Identifica el número de versión del publicador.|  
|peer_db_version|**sysname**|Identifica el número de versión de la base de datos del mismo nivel.|  
|is_peer|**poco**|Indica si un nodo es un suscriptor de solo lectura. Un valor de **0** indica un suscriptor de solo lectura.|  
|conflict_detection_enabled|**poco**|Indica si la detección de conflictos está habilitada para la topología.|  
|originator_id|**varbinary(16)**|Identifica cada nodo de la topología para detectar conflictos. Para más información, consulte [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**Inter**|Período de tiempo, en días, durante el cual los metadatos se almacenan en tablas conflictivas.|  
|peer_subscriptions|**LENGUAJE**|Información sobre el nodo que respondió a la solicitud.|  
|progress_phase|**nvarchar (32)**|Identifica la fase actual de procesamiento, utilizando uno de los valores siguientes:<br /><br /> Started<br /><br /> Versión del mismo nivel recopilada<br /><br /> Estado recopilado|  
|modified_date|**DateTime**|Fecha y hora en que se completó una fase.|  
  
## <a name="see-also"></a>Véase también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
