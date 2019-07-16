---
title: MSpub_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1b204024d65e72eb65eefc9f63f914eab6ace29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032603"
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSpub_identity_range** tabla proporciona soporte de administración del intervalo de identidad. Esta tabla se almacena en la base de datos de publicaciones y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|Identificador de la tabla cuya columna de identidad se administra mediante la replicación.|  
|**intervalo**|**bigint**|Controla el tamaño del intervalo de los valores de identidad consecutivos que podrían asignarse a la suscripción en un ajuste.|  
|**pub_range**|**bigint**|Controla el tamaño del intervalo de los valores de identidad consecutivos que podrían asignarse a la publicación en un ajuste.|  
|**current_pub_range**|**bigint**|Intervalo actual que utiliza la publicación. Puede ser diferente de *pub_range* si se muestra después de que se va a cambiar **sp_changearticle** y antes del siguiente ajuste de intervalo.|  
|**threshold**|**int**|Valor de porcentaje que controla cuándo el Agente de distribución asigna un nuevo intervalo de identidad. Cuando se especifica el porcentaje de valores en *umbral* es utilizado, el agente de distribución crea un nuevo intervalo de identidad.|  
|**last_seed**|**bigint**|Límite inferior del intervalo actual.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
