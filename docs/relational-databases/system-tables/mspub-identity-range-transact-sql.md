---
title: MSpub_identity_range (Transact-SQL) | Documentos de Microsoft
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
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1e74fd6c4f1352a98151beb525304cec2a518c51
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSpub_identity_range** tabla proporciona soporte de administración de intervalo de identidad. Esta tabla se almacena en la base de datos de publicaciones y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**ObjID**|**int**|Identificador de la tabla cuya columna de identidad se administra mediante la replicación.|  
|**intervalo**|**bigint**|Controla el tamaño del intervalo de los valores de identidad consecutivos que podrían asignarse a la suscripción en un ajuste.|  
|**pub_range**|**bigint**|Controla el tamaño del intervalo de los valores de identidad consecutivos que podrían asignarse a la publicación en un ajuste.|  
|**current_pub_range**|**bigint**|Intervalo actual que utiliza la publicación. Puede ser diferente de *pub_range* si se muestra después de que se va a cambiar **sp_changearticle** y antes del siguiente ajuste de intervalo.|  
|**Umbral**|**int**|Valor de porcentaje que controla cuándo el Agente de distribución asigna un nuevo intervalo de identidad. Cuando se especifica el porcentaje de valores en *umbral* es usa, el agente de distribución crea un nuevo intervalo de identidad.|  
|**last_seed**|**bigint**|Límite inferior del intervalo actual.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
