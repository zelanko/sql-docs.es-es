---
title: sysmail_mailattachments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3bdcea5da463e2501954c4bf96ca58bac216eb58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060201"
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada archivo adjunto enviado al Correo electrónico de base de datos. Utilice esta vista cuando desee información acerca de los datos adjuntos del Correo electrónico de base de datos. Para revisar todos los mensajes de correo electrónico procesados por correo electrónico de base de datos, utilice [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|Identificador de los datos adjuntos.|  
|**mailitem_id**|**int**|Identificador del elemento de correo que incluía los datos adjuntos.|  
|**filename**|**nvarchar (520)**|Nombre de archivo de los datos adjuntos. Cuando **attach_query_result** es 1 y **query_attachment_filename** es NULL, correo electrónico de base de datos crea un nombre de archivo arbitrario.|  
|**tamaño de archivo**|**int**|Tamaño de los datos adjuntos en bytes.|  
|**datos adjuntos**|**varbinary(max)**|Contenido de los datos adjuntos.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila.|  
  
## <a name="remarks"></a>Comentarios  
 Al solucionar problemas del Correo electrónico de base de datos, utilice esta vista para ver las propiedades de los datos adjuntos.  
  
 Los datos adjuntos almacenados en las tablas del sistema pueden provocar la **msdb** base de datos crezca. Use **sysmail_delete_mailitems_sp** para eliminar elementos del correo electrónico y los datos adjuntos asociados. Para obtener más información, consulte [crear un trabajo del Agente SQL Server para archivar mensajes de correo electrónico de base de datos y registros de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permisos  
 Concede a la **sysadmin** rol fijo de servidor y el **DatabaseMailUserRole** rol de base de datos. Cuando se ejecuta un miembro de la **sysadmin** rol fijo de servidor, esta vista muestra todos los datos adjuntos. Todos los demás usuarios verán únicamente los archivos adjuntos que envíen ellos mismos.  
  
## <a name="see-also"></a>Vea también  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
