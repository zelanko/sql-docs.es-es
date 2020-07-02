---
title: Sys. server_event_notifications (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a8268cd4796743afd0f71e59afc409a07c840d5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85664811"
---
# <a name="sysserver_event_notifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Devuelve una fila para cada objeto de notificación de eventos de nivel de servidor.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de notificación de eventos de servidor. Este nombre es único en todas las notificaciones de eventos de nivel de servidor.|  
|**object_id**|**int**|Número de identificación del objeto. Es único en la base de datos **maestra** .|  
|**parent_class**|**tinyint**|Clase del elemento primario. Siempre es 100 = Servidor.|  
|**parent_class_desc**|**nvarchar(60)**|Descripción de la clase de elemento primario. Siempre es SERVER.|  
|**parent_id**|**int**|Siempre es 0.|  
|**create_date**|**datetime**|Fecha de creación.|  
|**modify_date**|**datetime**|Es la fecha en que el objeto ha sido modificado por última vez mediante la instrucción ALTER.|  
|**service_name**|**nvarchar(256)**|Nombre del servicio de destino al que se envía la notificación.|  
|**broker_instance**|**nvarchar(128)**|El Service Broker en que se ha definido el servicio de destino con nombre.|  
|**creator_sid**|**varbinary(85)**|El SID del inicio de sesión que ejecuta la instrucción que crea la notificación de eventos. NULL si WITH FAN_IN no se especifica en la definición de notificación de eventos.|  
|**principal_id**|**int**|El Id. de la entidad de seguridad del servidor a la que pertenece.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
