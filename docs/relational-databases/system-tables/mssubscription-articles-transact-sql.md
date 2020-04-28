---
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8518c787f876152787ee30a20b9f25f936b9fa86
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139778"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSsubscription_articles** contiene información sobre los artículos de una suscripción en cola. Esta tabla solo se llena con los tipos de replicación de actualización en cola y actualización inmediata con la actualización en cola como una conmutación por error.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|El Id. del agente que sirve a este artículo.|  
|**artid**|**int**|El identificador de artículo de la tabla **sysarticles** .|  
|**ARTICLE**|**sysname**|Nombre del artículo de la tabla **sysarticles** .|  
|**dest_table**|**sysname**|El nombre de la tabla de destino de la tabla **sysarticles** .|  
|**propietario**|**sysname**|El propietario de la suscripción.|  
|**cft_table**|**sysname**|El nombre de la tabla de conflictos de este artículo, para el tipo de replicación de actualización en cola.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
