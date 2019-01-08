---
title: MStracer_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1ba25e4f55debbe73a66de23986743a83d1feb5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765267"
---
# <a name="mstracerhistory-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MStracer_history** tabla mantiene un registro de todos los testigos de seguimiento que se han recibido en el suscriptor. Esta tabla se almacena en la base de datos de distribución y es utilizada por la replicación para la supervisión del rendimiento.   
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|Identifica un token de seguimiento de forma exclusiva.|  
|**valor de agent_id**|**int**|Identifica al agente que administra el registro del token de seguimiento.|  
|**subscriber_commit**|**datetime**|La fecha y la hora en que se ha confirmado el registro del token de seguimiento en el suscriptor.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
