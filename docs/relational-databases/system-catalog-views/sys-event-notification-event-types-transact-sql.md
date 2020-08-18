---
description: sys.event_notification_event_types (Transact-SQL)
title: Sys. event_notification_event_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.event_notification_event_types_TSQL
- sys.event_notification_event_types
- event_notification_event_types_TSQL
- event_notification_event_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.event_notification_event_types catalog view
ms.assetid: 73dae456-7044-4b00-b0bd-990ef810b356
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 22dbab533f189952b72ae7ada8d5f736b745a885
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88401701"
---
# <a name="sysevent_notification_event_types-transact-sql"></a>sys.event_notification_event_types (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve una fila para cada evento o grupo de eventos en el que se puede activar una notificación de eventos.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**type**|**int**|Tipo de evento o grupo de eventos que activa una notificación de eventos.|  
|**type_name**|**nvarchar(128)**|Nombre de un evento o grupo de eventos. Se puede especificar en la cláusula FOR de una instrucción [Create Event Notification](../../t-sql/statements/create-event-notification-transact-sql.md) .|  
|**parent_type**|**int**|Tipo de grupo de eventos que es el elemento primario del evento o grupo de eventos.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
