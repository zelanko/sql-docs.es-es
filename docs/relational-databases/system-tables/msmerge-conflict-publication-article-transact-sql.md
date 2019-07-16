---
title: MSmerge_conflict_&lt;publicación&gt;_&lt;artículo&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
ms.openlocfilehash: dfae18a55ddb8b1c95aad25e27f006b28fde79af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895112"
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>MSmerge_conflict_&lt;publicación&gt;_&lt;artículo&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_conflict_*publicación*_ * artículo*** tabla contiene información sobre las filas que entran en conflicto o cambios de filas que se deshicieron para conseguir la convergencia de los datos. En una publicación, cada tabla replicada posee una tabla de conflictos; el nombre de esta tabla de conflictos se anexa al nombre del artículo y la publicación. Estas tablas de conflictos específicos del artículo se encuentran en la base de datos utilizada para registrar los conflictos, que normalmente es la base de datos de publicaciones, pero que puede ser la base de datos de suscripciones si el registro de conflictos está descentralizado.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|Representa una columna en una tabla replicada. Esta tabla del sistema contiene una columna para cada columna del artículo de la tabla.|  
|**rowguid**|**uniqueidentifier**|El identificador de fila para la fila de conflicto.|  
|**ModifiedDate**|**datetime**|La fecha en que ocurrió el conflicto.|  
|**origin_datasource_id**|**uniqueidentifier**|La suscripción en la que se deshizo el cambio de fila o se perdió el conflicto.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
