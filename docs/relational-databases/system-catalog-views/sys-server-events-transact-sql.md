---
title: Sys.server_events (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_events_TSQL
- sys.server_events_TSQL
- server_events
- sys.server_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_events catalog view
ms.assetid: 996f6c9b-6426-4847-95d9-6b77541422be
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b8f41c89cc17602f5a9aa2ab8ee292506ad1eee8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysserverevents-transact-sql"></a>sys.server_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada evento para el que se activa una notificación de eventos o un desencadenador DDL en el servidor. Las columnas **object_id** y **tipo** identificar de forma única el evento de servidor.  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador de la notificación de eventos o del desencadenador DDL que se activan en el servidor.|  
|**Tipo**|**int**|Tipo del evento que provoca la activación de la notificación de eventos o el desencadenador DDL.|  
|**type_desc**|**nvarchar(60)**|Descripción del evento que provoca la activación del desencadenador DDL o de la notificación de eventos.|  
|**event_group_type**|**int**|Grupo de eventos donde se crea el desencadenador o la notificación de eventos o NULL si no se crea en un grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descripción del grupo de eventos en el que se creó la notificación de eventos o desencadenador, o null si no se crea en un grupo de eventos|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
