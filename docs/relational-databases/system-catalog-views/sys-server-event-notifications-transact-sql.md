---
title: Sys.server_event_notifications (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94af1bc2f9288f09855f4bb06ea8ae929b9cb757
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada objeto de notificación de eventos de nivel de servidor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de notificación de eventos de servidor. Este nombre es único en todas las notificaciones de eventos de nivel de servidor.|  
|**object_id**|**int**|Número de identificación del objeto. Es único dentro de la **maestro** base de datos.|  
|**parent_class**|**tinyint**|Clase del elemento primario. Siempre es 100 = Servidor.|  
|**parent_class_desc**|**nvarchar(60)**|Descripción de la clase de elemento primario. Siempre es SERVER.|  
|**parent_id**|**int**|Es siempre 0.|  
|**create_date**|**datetime**|Fecha de creación.|  
|**modify_date**|**datetime**|Es la fecha en que el objeto ha sido modificado por última vez mediante la instrucción ALTER.|  
|**service_name**|**nvarchar(256)**|Nombre del servicio de destino al que se envía la notificación.|  
|**BROKER_INSTANCE**|**nvarchar(128)**|El Service Broker en que se ha definido el servicio de destino con nombre.|  
|**creator_sid**|**varbinary(85)**|El SID del inicio de sesión que ejecuta la instrucción que crea la notificación de eventos. NULL si WITH FAN_IN no se especifica en la definición de notificación de eventos.|  
|**principal_id**|**int**|El Id. de la entidad de seguridad del servidor a la que pertenece.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
