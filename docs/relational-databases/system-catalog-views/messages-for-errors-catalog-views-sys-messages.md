---
title: Sys. Messages (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8ed45ac6fd511d2024cc11916fe70980a7a6a065
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816113"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Vistas de catálogo de mensajes (para errores): sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada **message_id** o **language_id** de los mensajes de error del sistema, tanto para los mensajes definidos por el sistema como para los definidos por el usuario. Para obtener más información, vea [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|Id. del mensaje. Es único en todo el servidor. Los Id. de mensaje inferiores a 50000 son mensajes del sistema.|  
|**language_id**|**smallint**|IDENTIFICADOR de idioma para el que se utiliza el texto en el **texto** , tal como se define en **syslanguages**. Es único para un **message_id**especificado.|  
|**severity**|**tinyint**|Nivel de gravedad del mensaje, entre 1 y 25. Es lo mismo para todos los idiomas de los mensajes dentro de un **message_id**.|  
|**is_event_logged**|**bit**|1 = Cuando hay un error, el mensaje se registra en el registro de eventos. Es lo mismo para todos los idiomas de los mensajes dentro de un **message_id**.|  
|**text**|**nvarchar(2048)**|Texto del mensaje que se utiliza cuando el **language_id** correspondiente está activo.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mensajes &#40;los errores&#41; vistas de catálogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Programación de cuadros de mensajes de excepción](https://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Mensajes de error](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventos y errores de Motor de base de datos](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
