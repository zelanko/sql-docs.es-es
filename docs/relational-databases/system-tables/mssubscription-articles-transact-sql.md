---
description: MSsubscription_articles (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f1f046a44c3dcfbe2a44de93efe2185600633e3c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89523806"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSsubscription_articles** contiene información sobre los artículos de una suscripción en cola. Esta tabla solo se llena con los tipos de replicación de actualización en cola y actualización inmediata con la actualización en cola como una conmutación por error.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|El Id. del agente que sirve a este artículo.|  
|**artid**|**int**|El identificador de artículo de la tabla **sysarticles** .|  
|**artículo**|**sysname**|Nombre del artículo de la tabla **sysarticles** .|  
|**dest_table**|**sysname**|El nombre de la tabla de destino de la tabla **sysarticles** .|  
|**propietario**|**sysname**|El propietario de la suscripción.|  
|**cft_table**|**sysname**|El nombre de la tabla de conflictos de este artículo, para el tipo de replicación de actualización en cola.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
