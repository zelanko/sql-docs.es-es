---
title: Sys.Messages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13120ff00d2935ed4cb10b91afad9c9076302c05
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741733"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Vistas de catálogo de mensajes (para errores): sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada **message_id** o **language_id** los mensajes de error en el sistema, para los mensajes definidos por el usuario y definido por el sistema. Para obtener más información, vea [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|Id. del mensaje. Es único en todo el servidor. Los Id. de mensaje inferiores a 50000 son mensajes del sistema.|  
|**language_id**|**smallint**|Id. de idioma para el que el texto en **texto** se usa, como se define en **syslanguages**. Debe ser único para un determinado **message_id**.|  
|**severity**|**tinyint**|Nivel de gravedad del mensaje, entre 1 y 25. Esto es lo mismo para todos los idiomas del mensaje un **message_id**.|  
|**is_event_logged**|**bit**|1 = Cuando hay un error, el mensaje se registra en el registro de eventos. Esto es lo mismo para todos los idiomas del mensaje un **message_id**.|  
|**texto**|**nvarchar(2048)**|Texto del mensaje utilizado para el correspondiente **language_id** está activo.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mensajes &#40;errores&#41; vistas de catálogo &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Mensaje de excepción cuadro programación](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Mensajes de error](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventos y errores del motor de base de datos](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
