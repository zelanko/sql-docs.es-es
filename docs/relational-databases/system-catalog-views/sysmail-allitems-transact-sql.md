---
title: sysmail_allitems (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs: TSQL
helpviewer_keywords: sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ba8deb3b11b01cf9f53e02024815150fa4441b6d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailallitems-transact-sql"></a>sysmail_allitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada mensaje procesado por el Correo electrónico de base de datos. Utilice esta vista cuando desee ver el estado de todos los mensajes.  
  
 Para ver sólo los mensajes con el estado de error, utilice [sysmail_faileditems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver sólo los mensajes no enviados, utilice [sysmail_unsentitems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver sólo los mensajes que se enviaron, use [sysmail_sentitems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador del elemento de correo en la cola de correo electrónico.|  
|**profile_id**|**int**|Identificador del perfil utilizado para enviar el mensaje.|  
|**destinatarios**|**varchar(max)**|Direcciones de correo electrónico de los destinatarios de mensajes.|  
|**copy_recipients**|**varchar(max)**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje.|  
|**blind_copy_recipients**|**varchar(max)**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje pero cuyos nombres no aparecen en el encabezado del mensaje.|  
|**Asunto**|**nvarchar(510)**|Línea de asunto del mensaje.|  
|**cuerpo**|**varchar(max)**|El cuerpo del mensaje.|  
|**body_format**|**varchar (20)**|El formato del cuerpo del mensaje. Los valores posibles son TEXT y HTML.|  
|**importancia**|**varchar(6)**|El **importancia** parámetro del mensaje.|  
|**sensibilidad**|**varchar (12)**|El **sensibilidad** parámetro del mensaje.|  
|**file_attachments**|**varchar(max)**|Una lista delimitada por punto y coma de nombres de archivo adjuntadas al mensaje de correo electrónico.|  
|**attachment_encoding**|**varchar (20)**|Tipo de datos adjuntos.|  
|**consulta**|**varchar(max)**|Consulta ejecutada por el programa de correo.|  
|**execute_query_database**|**sysname**|Contexto de base de datos en el cual el programa de correo ejecutó la consulta.|  
|**attach_query_result_as_file**|**bit**|Si el valor es 0, los resultados de la consulta se incluyeron en el cuerpo del mensaje de correo electrónico, después del contenido del cuerpo. Si el valor es 1, los resultados se devolvieron como datos adjuntos.|  
|**query_result_header**|**bit**|Si el valor es 1, los resultados de la consulta contenían encabezados de columna. Si el valor es 0, los resultados de la consulta no contenían encabezados de columna.|  
|**query_result_width**|**int**|El **query_result_width** parámetro del mensaje.|  
|**query_result_separator**|**Char (1)**|Carácter utilizado para separar columnas en la salida de la consulta.|  
|**exclude_query_output**|**bit**|El **exclude_query_output** parámetro del mensaje. Para obtener más información, vea [sp_send_dbmail &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|El **append_query_error** parámetro del mensaje. El valor 0 indica que el Correo electrónico de base de datos no debe enviar el mensaje de correo electrónico si hay un error en la consulta.|  
|**send_request_date**|**datetime**|Fecha y hora en que se colocó el mensaje en la cola de correo electrónico.|  
|**send_request_user**|**sysname**|Usuario que envió el mensaje. Se trata del contexto de usuario del procedimiento del Correo electrónico de base de datos, no del campo De: del mensaje.|  
|**sent_account_id**|**int**|Identificador de la cuenta del Correo electrónico de base de datos utilizada para enviar el mensaje.|  
|**sent_status**|**varchar (8)**|Estado del mensaje. Los valores posibles son:<br /><br /> **enviar** -se envió el correo electrónico.<br /><br /> **sin enviar** -correo electrónico de base de datos todavía está intentando enviar el mensaje.<br /><br /> **volver a intentar** -no se pudo enviar el mensaje de correo electrónico de base de datos pero está intentando enviarlo de nuevo.<br /><br /> **no se pudo** -correo electrónico de base de datos no pudo enviar el mensaje.|  
|**sent_date**|**datetime**|Fecha y hora en que se envió el mensaje.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila.|  
  
## <a name="remarks"></a>Comentarios  
 Use la **sysmail_allitems** vista para ver el estado de todos los mensajes procesados por el correo electrónico de base de datos. Al solucionar problemas del Correo electrónico de base de datos, puede que esta vista le ayude a identificar la naturaleza del problema, pues en ella se muestran los atributos de los mensajes enviados comparados con los de los mensajes no enviados.  
  
 Las tablas del sistema expuestas por esta vista contiene todos los mensajes y puede provocar la **msdb** base de datos crezca. Elimine periódicamente los mensajes antiguos de la vista para reducir el tamaño de las tablas. Para obtener más información, consulte [crear un trabajo del Agente SQL Server para archivar mensajes de correo electrónico de base de datos y registros de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissions  
 Concede a **sysadmin** rol fijo de servidor y **DatabaseMailUserRole** rol de base de datos. Cuando se ejecuta un miembro de la **sysadmin** rol fijo de servidor, esta vista muestra todos los mensajes. Todos los demás usuarios verán únicamente los mensajes que envíen ellos mismos.  
  
  
