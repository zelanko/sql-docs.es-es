---
title: sysmail_sentitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_sentitems_TSQL
- sysmail_sentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_sentitems database mail view
ms.assetid: 16eb2a44-cebb-4cec-93ac-e2498c39989f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c935a83c3c3fdd9fa577a3232e46caed7865c1c3
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745368"
---
# <a name="sysmail_sentitems-transact-sql"></a>sysmail_sentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Contiene una fila por cada mensaje enviado por el Correo electrónico de base de datos. Use **sysmail_sentitems** cuando desee ver los mensajes que se enviaron correctamente.  
  
 Para ver todos los mensajes procesados por Correo electrónico de base de datos, use [Transact &#40;-&#41;SQL de sysmail_allitems](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver solo los mensajes con el estado de error, use [Transact &#40;-&#41;SQL de sysmail_faileditems](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver solo los mensajes no enviados o de reintento, use [sysmail_unsentitems &#40;Transact&#41;-SQL](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md). Para ver los datos adjuntos de correo electrónico, use [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador del elemento de correo en la cola de correo electrónico.|  
|**profile_id**|**int**|Identificador del perfil utilizado para enviar el mensaje.|  
|**destinatarios**|**ntext**|Direcciones de correo electrónico de los destinatarios de mensajes.|  
|**copy_recipients**|**ntext**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje.|  
|**blind_copy_recipients**|**ntext**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje pero cuyos nombres no aparecen en el encabezado del mensaje.|  
|**subject**|**nvarchar(510)**|Línea de asunto del mensaje.|  
|**body**|**ntext**|El cuerpo del mensaje.|  
|**body_format**|**varchar(20)**|El formato del cuerpo del mensaje. Los valores posibles son **Text** y **html**.|  
|**importance**|**varchar(6)**|Parámetro de **importancia** del mensaje.|  
|**distinga**|**varchar(12)**|Parámetro de **sensibilidad** del mensaje.|  
|**file_attachments**|**ntext**|Una lista delimitada por signos de punto y coma de nombres de archivo adjuntos al mensaje de correo electrónico.|  
|**attachment_encoding**|**varchar(20)**|Tipo de datos adjuntos.|  
|**query**|**ntext**|Consulta ejecutada por el programa de correo.|  
|**execute_query_database**|**sysname**|Contexto de base de datos en el cual el programa de correo ejecutó la consulta.|  
|**attach_query_result_as_file**|**bit**|Si el valor es 0, los resultados de la consulta se incluyeron en el cuerpo del mensaje de correo electrónico, después del contenido del cuerpo. Si el valor es 1, los resultados se devolvieron como datos adjuntos.|  
|**query_result_header**|**bit**|Si el valor es 1, los resultados de la consulta contenían encabezados de columna. Si el valor es 0, los resultados de la consulta no contenían encabezados de columna.|  
|**query_result_width**|**int**|Parámetro **query_result_width** del mensaje.|  
|**query_result_separator**|**char(1)**|Carácter utilizado para separar columnas en la salida de la consulta.|  
|**exclude_query_output**|**bit**|Parámetro **exclude_query_output** del mensaje. Para obtener más información, [vea &#40;SP_SEND_DBMAIL Transact-&#41;SQL](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|Parámetro **append_query_error** del mensaje. El valor 0 indica que el Correo electrónico de base de datos no debe enviar el mensaje de correo electrónico si hay un error en la consulta.|  
|**send_request_date**|**datetime**|Fecha y hora en que se colocó el mensaje en la cola de correo electrónico.|  
|**send_request_user**|**sysname**|El usuario que envió el mensaje. Se trata del contexto de usuario del procedimiento del Correo electrónico de base de datos, no del campo De: del mensaje.|  
|**sent_account_id**|**int**|Identificador de la cuenta del Correo electrónico de base de datos utilizada para enviar el mensaje.|  
|**sent_status**|**varchar(8)**|Estado del mensaje. Siempre se **envía** para esta vista.|  
|**sent_date**|**datetime**|Fecha y hora en que se envió el mensaje.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila.|  
  
## <a name="remarks"></a>Comentarios  
 Al solucionar problemas del Correo electrónico de base de datos, puede que esta vista le ayude a identificar la naturaleza del problema, pues en ella se muestran los atributos de los mensajes enviados correctamente. El Correo electrónico de base de datos marca los mensajes como enviados cuando se envían correctamente a un servidor de correo SMTP. Normalmente, los mensajes de correo electrónico se reciben en pocos minutos, pero puede que se retrasen a causa de problemas con el servidor SMTP. El Correo electrónico de base de datos marca los mensajes como enviados cuando los acepta el servidor de correo SMTP. Los mensajes de correo electrónico con errores en el servidor de correo SMTP, como una dirección de correo electrónico de destinatario no válida, no se devuelven al Correo electrónico de base de datos. Estos mensajes se registran como enviados aunque no se hayan entregado. Este tipo de error se debe solucionar en el servidor SMTP. Asimismo, puede que el servidor de correo SMTP envíe a la dirección de respuesta de una cuenta del Correo electrónico de base de datos una notificación en la que se indica que no se puede entregar el mensaje.  
  
## <a name="permissions"></a>Permisos  
 Se concede al rol fijo de servidor **sysadmin** y al rol de base de datos **DatabaseMailUserRole** . Cuando lo ejecuta un miembro del rol fijo de servidor **sysadmin** , esta vista muestra todos los mensajes enviados. Los demás usuarios verán únicamente los mensajes que ellos han enviado.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de mensajería de Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
  
