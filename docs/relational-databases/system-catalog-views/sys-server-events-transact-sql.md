---
title: Sys. server_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0f5e753b2d5db8d75739f8e65c909f593f8b6e77
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894951"
---
# <a name="sysserver_events-transact-sql"></a>sys.server_events (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila por cada evento para el que se activa una notificación de eventos o un desencadenador DDL en el servidor. Las columnas **object_id** y **tipo** identifican de forma única el evento de servidor.  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador de la notificación de eventos o del desencadenador DDL que se activan en el servidor.|  
|**type**|**int**|Tipo del evento que provoca la activación de la notificación de eventos o el desencadenador DDL.|  
|**type_desc**|**nvarchar(60)**|Descripción del evento que provoca la activación del desencadenador DDL o de la notificación de eventos.|  
|**event_group_type**|**int**|Grupo de eventos donde se crea el desencadenador o la notificación de eventos o NULL si no se crea en un grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descripción del grupo de eventos en el que se crea el desencadenador o la notificación de eventos, o null si no se crea en un grupo de eventos|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
