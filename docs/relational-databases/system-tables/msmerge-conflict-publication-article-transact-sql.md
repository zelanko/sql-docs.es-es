---
title: MSmerge_conflict_&lt;(&gt;publicación&lt;) _article&gt; (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 342b0f51fb4f68945f6ab8c4b511c5299acfba49
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893582"
---
# <a name="msmerge_conflict_ltpublicationgt_ltarticlegt-transact-sql"></a>Artículo\_&lt;\_sobrepublicación&lt;de conflictos de MSmerge (Transact-SQL)&gt;\_&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La **tabla\_de\_ _ depublicación\_de conflictos de MSmerge** contiene información sobre las filas en conflicto o los cambios de filas que se deshicieron para lograr la convergencia de datos. En una publicación, cada tabla replicada posee una tabla de conflictos; el nombre de esta tabla de conflictos se anexa al nombre del artículo y la publicación. Estas tablas de conflictos específicos del artículo se encuentran en la base de datos utilizada para registrar los conflictos, que normalmente es la base de datos de publicaciones, pero que puede ser la base de datos de suscripciones si el registro de conflictos está descentralizado.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|** _**|**variable**|Representa una columna en una tabla replicada. Esta tabla del sistema contiene una columna para cada columna del artículo de la tabla.|  
|**rowguid**|**uniqueidentifier**|El identificador de fila para la fila de conflicto.|  
|**ModifiedDate**|**datetime**|La fecha en que ocurrió el conflicto.|  
|**\_identificador\_del origen de origen**|**uniqueidentifier**|La suscripción en la que se deshizo el cambio de fila o se perdió el conflicto.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas &#40;de replicación de TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
