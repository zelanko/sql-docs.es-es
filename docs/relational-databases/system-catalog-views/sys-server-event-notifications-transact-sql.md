---
title: sys.server_event_notifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b985d915d3d7bb6b3130ccb63a400f314fa05a38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62860917"
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada objeto de notificación de eventos de nivel de servidor.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de notificación de eventos de servidor. Este nombre es único en todas las notificaciones de eventos de nivel de servidor.|  
|**object_id**|**int**|Número de identificación del objeto. Es único dentro de la **maestro** base de datos.|  
|**parent_class**|**tinyint**|Clase del elemento primario. Siempre es 100 = Servidor.|  
|**parent_class_desc**|**nvarchar(60)**|Descripción de la clase de elemento primario. Siempre es SERVER.|  
|**parent_id**|**int**|Es siempre 0.|  
|**create_date**|**datetime**|Fecha de creación.|  
|**modify_date**|**datetime**|Es la fecha en que el objeto ha sido modificado por última vez mediante la instrucción ALTER.|  
|**service_name**|**nvarchar(256)**|Nombre del servicio de destino al que se envía la notificación.|  
|**broker_instance**|**nvarchar(128)**|El Service Broker en que se ha definido el servicio de destino con nombre.|  
|**creator_sid**|**varbinary(85)**|El SID del inicio de sesión que ejecuta la instrucción que crea la notificación de eventos. NULL si WITH FAN_IN no se especifica en la definición de notificación de eventos.|  
|**principal_id**|**int**|El Id. de la entidad de seguridad del servidor a la que pertenece.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
