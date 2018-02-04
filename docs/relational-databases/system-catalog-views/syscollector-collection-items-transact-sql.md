---
title: syscollector_collection_items (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca9b8aed18c716e235d1848d7130395cf4fe7875
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre un elemento en un conjunto de recopilación.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|Identifica el conjunto de recopilación. No admite valores NULL.|  
|**collection_item_id**|**int**|Identifica un elemento en el conjunto de recopilación. No admite valores NULL.|  
|**collector_type_uid**|**uniqueidentifier**|GUID utilizado para identificar el tipo de recopilador. No admite valores NULL.|  
|**Nombre**|**nvarchar(4000)**|Nombre del conjunto de recopilación. Acepta valores NULL.|  
|**frecuencia**|**int**|Frecuencia con que un elemento de recopilación recopila datos. No admite valores NULL.|  
|**parámetros**|**xml**|Describe la parametrización para el tipo de recopilador asociado al elemento de recopilación. El esquema XML para este elemento de recopilación se valida con los esquemas XML (XSD) almacenado en el **parameter_schema** para un tipo de recopilador determinado. Acepta valores NULL. Para obtener más información, consulte [syscollector_collector_types &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md).|  
  
## <a name="permissions"></a>Permissions  
 Requiere SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
