---
title: Sys.trigger_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 2f8be2ef8f840dcb6492263eaf3b0d76e6ab5209
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39550265"
---
# <a name="systriggerevents-transact-sql"></a>sys.trigger_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por evento para el que se activa un desencadenador.  
  
> [!NOTE]  
>  **Sys.trigger_events** no es aplicable a las notificaciones de eventos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<Columnas heredan de sys.events >**|No aplicable|Hereda el **object_id**, **tipo**, **type_desc** columnas de [sys.events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md).|  
|**is_first**|**bit**|El desencadenador está marcado como el primero que se activará para este evento.|  
|**is_last**|**bit**|El desencadenador está marcado como el último que se activará para este evento.|  
|**event_group_type**|**int**|Grupo de eventos donde se crea el desencadenador o NULL si no se crea en un grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descripción del grupo de eventos donde se crea el desencadenador o NULL si no se crea en un grupo de eventos.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
