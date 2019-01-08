---
title: IHpublisherindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a24126ef3226878b4d07a056573f3b60e94495c3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802517"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHpublisherindexes** tabla del sistema contiene una fila por cada índice replicado desde no publicadores de SQL Server utilizando el distribuidor actual. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|Identifica un índice publicado.|  
|**table_id**|**int**|Identifica la tabla de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) al que pertenece el índice.|  
|**publisher_id**|**smallint**|Identifica el no publicador de SQL Server desde el que se está publicando el índice.|  
|**Nombre**|**sysname**|Nombre del índice publicado.|  
|**Tipo**|**nvarchar(255)**|Tipo de índice admitido desde el [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md) tabla del sistema.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
