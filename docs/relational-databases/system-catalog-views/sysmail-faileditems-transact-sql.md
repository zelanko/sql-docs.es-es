---
title: sysmail_faileditems (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
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
- sysmail_faileditems
- sysmail_faileditems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_faileditems database mail view
ms.assetid: a31562c5-358e-4cfc-a72d-b3faccc53851
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff656d7a531e7c5b9eb495c55f1a7e081da7a475
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailfaileditems-transact-sql"></a>sysmail_faileditems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada mensaje de correo electrónico de base de datos con la **no se pudo** estado. Utilice esta vista para determinar qué mensajes no se enviaron correctamente.  
  
 Para ver todos los mensajes procesados por el correo electrónico de base de datos, utilice [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver sólo los mensajes no enviados, utilice [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver sólo los mensajes que se enviaron, use [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md). Para ver los datos adjuntos de correo electrónico, use [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador del elemento de correo en la cola de correo electrónico.|  
|**profile_id**|**int**|El identificador del perfil utilizado para enviar el mensaje.|  
|**destinatarios**|**ntext**|Direcciones de correo electrónico de los destinatarios de mensajes.|  
|**copy_recipients**|**ntext**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje.|  
|**blind_copy_recipients**|**ntext**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje pero cuyos nombres no aparecen en el encabezado del mensaje.|  
|**Asunto**|**nvarchar(510)**|Línea de asunto del mensaje.|  
|**Cuerpo**|**ntext**|El cuerpo del mensaje.|  
|**body_format**|**varchar (20)**|El formato del cuerpo del mensaje. Los valores posibles son TEXT y HTML.|  
|**Importancia**|**varchar(6)**|El **importancia** parámetro del mensaje.|  
|**Sensibilidad**|**varchar (12)**|El **sensibilidad** parámetro del mensaje.|  
|**file_attachments**|**ntext**|Una lista delimitada por punto y coma de nombres de archivo adjuntadas al mensaje de correo electrónico.|  
|**Attachment_encoding**|**varchar (20)**|Tipo de datos adjuntos.|  
|**Query**|**ntext**|Consulta ejecutada por el programa de correo.|  
|**execute_query_database**|**sysname**|Contexto de base de datos en el cual el programa de correo ejecutó la consulta.|  
|**attach_query_result_as_file**|**bit**|Si el valor es 0, los resultados de la consulta se incluyeron en el cuerpo del mensaje de correo electrónico, después del contenido del cuerpo. Si el valor es 1, los resultados se devolvieron como datos adjuntos.|  
|**query_result_header**|**bit**|Si el valor es 1, los resultados de la consulta contenían encabezados de columna. Si el valor es 0, los resultados de la consulta no contenían encabezados de columna.|  
|**query_result_width**|**int**|El **query_result_width** parámetro del mensaje.|  
|**query_result_separator**|**char(1)**|Carácter utilizado para separar columnas en la salida de la consulta.|  
|**exclude_query_output**|**bit**|El **exclude_query_output** parámetro del mensaje. Para obtener más información, consulte [sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|El **append_query_error** parámetro del mensaje. El valor 0 indica que el Correo electrónico de base de datos no debe enviar el mensaje de correo electrónico si hay un error en la consulta.|  
|**send_request_date**|**datetime**|Fecha y hora en que se colocó el mensaje en la cola de correo electrónico.|  
|**send_request_user**|**sysname**|Usuario que envió el mensaje. Se trata del contexto de usuario del procedimiento del Correo electrónico de base de datos, no del campo De: del mensaje.|  
|**sent_account_id**|**int**|Identificador de la cuenta del Correo electrónico de base de datos utilizada para enviar el mensaje. Siempre es NULL para esta vista.|  
|**sent_status**|**varchar (8)**|Estado del mensaje. Siempre **no se pudo** para esta vista.|  
|**sent_date**|**datetime**|Fecha y hora en que se eliminó el mensaje de la cola de correo electrónico.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila.|  
  
## <a name="remarks"></a>Comentarios  
 Use la **sysmail_faileditems** vista para ver los mensajes que no se han enviado por correo electrónico de base de datos. Al solucionar problemas del Correo electrónico de base de datos, puede que esta vista le ayude a identificar la naturaleza del problema, pues en ella se muestran los atributos de los mensajes no enviados. Para ver el motivo del error, consulte la entrada del mensaje de error en la [sysmail_event_log &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) vista.  
  
## <a name="permissions"></a>Permissions  
 Concede a **sysadmin** rol fijo de servidor y **databasemailuserrole** rol de base de datos. Cuando se ejecuta un miembro de la **sysadmin** rol fijo de servidor, esta vista muestra los mensajes de errores en todos los. Todos los demás usuarios verán únicamente los mensajes con error que envíen ellos mismos.  
  
  
