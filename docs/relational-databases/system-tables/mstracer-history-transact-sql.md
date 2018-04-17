---
title: MStracer_history (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
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
applies_to:
- SQL Server
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 789289c449c70f4bffafb26798f3364a404cc174
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mstracerhistory-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MStracer_history** tabla mantiene un registro de todos los testigos de seguimiento que se han recibido en el suscriptor. Esta tabla se almacena en la base de datos de distribución y es utilizada por la replicación para la supervisión del rendimiento.   
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|Identifica un token de seguimiento de forma exclusiva.|  
|**agent_id**|**int**|Identifica al agente que administra el registro del token de seguimiento.|  
|**subscriber_commit**|**datetime**|La fecha y la hora en que se ha confirmado el registro del token de seguimiento en el suscriptor.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
