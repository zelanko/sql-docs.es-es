---
title: Sys.Messages (Transact-SQL) | Documentos de Microsoft
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
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 07a5a426c0a2cf0b4b7c0385850471c3580d4fd3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33179001"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Vistas de catálogo de mensajes (de errores) - sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada **message_id** o **language_id** de los mensajes de error en el sistema, para los mensajes definidos por el usuario y definidas por el sistema. Para obtener más información, vea [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|Id. del mensaje. Es único en todo el servidor. Los Id. de mensaje inferiores a 50000 son mensajes del sistema.|  
|**language_id**|**smallint**|Id. de idioma para el que el texto en **texto** se utiliza, como se define en **syslanguages**. Esta capacidad es única para un determinado **message_id**.|  
|**severity**|**tinyint**|Nivel de gravedad del mensaje, entre 1 y 25. Este es el mismo para todos los idiomas del mensaje un **message_id**.|  
|**is_event_logged**|**bit**|1 = Cuando hay un error, el mensaje se registra en el registro de eventos. Este es el mismo para todos los idiomas del mensaje un **message_id**.|  
|**texto**|**nvarchar(2048)**|Texto del mensaje utilizado para la correspondiente **language_id** está activo.|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mensajes &#40;errores&#41; vistas de catálogo &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Mensaje de excepción cuadro programación](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Mensajes de error](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventos y errores del motor de base de datos](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
