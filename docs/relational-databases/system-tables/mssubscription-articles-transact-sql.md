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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e0aaa6b412f1ccbbc71e9e5b19f68a518912f333
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812269"
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
  
  
