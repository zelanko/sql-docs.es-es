---
title: MSmerge_history (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
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
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1e28c0aae7f29099ebef75d5c0aa7ef81eec0379
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005832"
---
# <a name="msmergehistory-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_history** tabla contiene filas de historial con descripciones detalladas de los resultados de las sesiones de trabajo de agente de mezcla anteriores. Esta tabla contiene una fila por cada línea de resultados del agente. Esta tabla se utiliza en la base de datos de distribución y en cada base de datos de suscripciones. En la base de datos de distribución, contiene el historial para todas las publicaciones de combinación y suscripciones que utilizan el Distribuidor. En cada base de datos de suscripciones, contiene el historial para las publicaciones a las que se suscribe el Suscriptor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|El Id. del trabajo del Agente de mezcla.|  
|**agent_id**|**int**|El Id. del Agente de mezcla.|  
|**Comentarios**|**nvarchar(255)**|El texto del mensaje.|  
|**error_id**|**int**|El identificador de un error en la [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) tabla del sistema.|  
|**timestamp**|**timestamp**|La columna de marca de tiempo de esta tabla.|  
|**updatable_row**|**bit**|Establecido en **1** si la fila de historial se puede sobrescribir.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
