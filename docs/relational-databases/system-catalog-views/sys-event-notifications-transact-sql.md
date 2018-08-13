---
title: Sys.event_notifications (Transact-SQL) | Microsoft Docs
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
- event_notifications_TSQL
- event_notifications
- sys.event_notifications_TSQL
- sys.event_notifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.event_notifications catalog view
ms.assetid: 136a76ee-2b35-4418-ab46-fda2d51f7d99
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1b07ca793821b39a549e709f52fa57bf1dd32dcb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562099"
---
# <a name="syseventnotifications-transact-sql"></a>sys.event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada objeto que es una notificación de eventos con **sys.objects.type** = es.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la notificación de eventos.|  
|**object_id**|**int**|Número de identificación del objeto. Es único en una base de datos.|  
|**parent_class**|**tinyint**|Clase del elemento primario.<br /><br /> 0 = Base de datos<br /><br /> 1 = objeto o columna|  
|**parent_class_desc**|**nvarchar(60)**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|Id. distinto de cero del objeto primario.<br /><br /> 0 = La clase primaria es la base de datos.|  
|**create_date**|**datetime**|Fecha de creación.|  
|**modify_date**|**datetime**|Siempre es igual a **create_date**.|  
|**service_name**|**nvarchar(256)**|Nombre del servicio de destino al que se envía la notificación.|  
|**BROKER_INSTANCE**|**nvarchar(128)**|Instancia de agente a la que se envía la notificación.|  
|**principal_id**|**int**|El Id. de la entidad de seguridad de la base de datos a la que pertenece esta notificación de eventos.|  
|**creator_sid**|**varbinary(85)**|SID del inicio de sesión que ha creado la notificación de eventos.<br /><br /> Es NULL si no se especifica la opción FAN_IN.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
