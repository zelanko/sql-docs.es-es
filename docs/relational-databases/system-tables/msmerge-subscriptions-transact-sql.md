---
title: MSmerge_subscriptions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSmerge_subscriptions
- MSmerge_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_subscriptions system table
ms.assetid: cafd954a-92f8-44cb-a5d0-dce9aafa5ee1
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e985f871e1409dc9e837fcbc192b136365d212d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="msmergesubscriptions-transact-sql"></a>MSmerge_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_subscriptions** tabla contiene una fila por cada suscripción que atiende el agente de mezcla en el suscriptor. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|El identificador del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**subscriber_id**|**smallint**|El identificador del suscriptor.|  
|**subscriber_db**|**sysname**|El nombre de la base de datos de suscripción.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> 0 = Inserción.<br /><br /> 1 = Extracción.<br /><br /> 2 = Anónima.|  
|**sync_type**|**tinyint**|Tipo de sincronización:<br /><br /> 1 = Automática<br /><br /> 2 = Sin sincronización|  
|**status**|**tinyint**|El estado de la suscripción.|  
|**subscription_time**|**datetime**|Hora a la que se agregó la suscripción.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
