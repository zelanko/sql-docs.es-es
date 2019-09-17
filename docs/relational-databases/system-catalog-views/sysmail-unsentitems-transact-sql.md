---
title: sysmail_unsentitems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
author: stevestein
ms.author: sstein
ms.openlocfilehash: f84e84ed7801beb20bdaca5c92d333133fad3b63
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745353"
---
# <a name="sysmail_unsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Contiene una fila por cada mensaje de Correo electrónico de base de datos con el estado sin **Enviar** o de **reintento** . Los mensajes con el estado unsent o retrying siguen en la cola de correo y pueden ser enviados en cualquier momento. Los mensajes pueden tener el estado sin **Enviar** por los siguientes motivos:  
  
-   El mensaje es nuevo y, aunque se ha colocado en la cola de correo, el Correo electrónico de base de datos está ocupado con otros mensajes y aún no ha alcanzado éste.  
  
-   El programa externo del Correo electrónico de base de datos no está en ejecución y no se envía ningún mensaje.  
  
 Los mensajes pueden tener el estado **reintentando** por los siguientes motivos:  
  
-   El Correo electrónico de base de datos intentó enviar el mensaje, pero no se pudo contactar con el servidor de correo SMTP. El Correo electrónico de base de datos seguirá intentando enviar el mensaje con otras cuentas propias asignadas al perfil que envió el mensaje. Si ninguna cuenta puede enviar el correo, Correo electrónico de base de datos esperará durante el período de tiempo configurado para el parámetro de **intervalo entre reintentos de cuenta** y, a continuación, intentará volver a enviar el mensaje. Correo electrónico de base de datos usa el parámetro **reintentos de cuenta** para determinar cuántas veces se intentará enviar el mensaje. Los mensajes conservan el estado de **reintento** , siempre y cuando correo electrónico de base de datos esté intentando enviar el mensaje.  
  
 Utilice esta vista cuando desee ver cuántos mensajes hay en espera para ser enviados y cuánto tiempo llevan en la cola de correo. Normalmente, el número de mensajes sin **Enviar** será bajo. Realice una prueba comparativa durante las operaciones normales para determinar un número razonable de mensajes en la cola para las operaciones.  
  
 Para ver todos los mensajes procesados por Correo electrónico de base de datos, use [Transact &#40;-&#41;SQL de sysmail_allitems](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver solo los mensajes con el estado de error, use [Transact &#40;-&#41;SQL de sysmail_faileditems](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver solo los mensajes que se enviaron, use [Transact &#40;-&#41;SQL de sysmail_sentitems](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador del elemento de correo en la cola de correo electrónico.|  
|**profile_id**|**int**|Identificador del perfil que se usa para enviar el mensaje.|  
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
|**send_request_user**|**sysname**|Usuario que envió el mensaje. Este es el contexto de usuario del procedimiento del correo electrónico de base de datos, no del campo **de** del mensaje.|  
|**sent_account_id**|**int**|Identificador de la cuenta del Correo electrónico de base de datos utilizada para enviar el mensaje. Siempre es NULL para esta vista.|  
|**sent_status**|**varchar(8)**|Se **desenviará** Si correo electrónico de base de datos no ha intentado enviar el correo. Volverá a **intentarlo** Si correo electrónico de base de datos no pudo enviar el mensaje, pero lo intentará de nuevo.|  
|**sent_date**|**datetime**|Fecha y hora en las que el Correo electrónico de base de datos intentó por última vez enviar el mensaje. Será NULL si el Correo electrónico de base de datos no ha intentado enviar el mensaje.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila.|  
  
## <a name="remarks"></a>Comentarios  
 Al solucionar problemas del Correo electrónico de base de datos, puede que esta vista le ayude a identificar la naturaleza del problema, pues en ella se muestra el número de mensajes a la espera de ser enviados y el tiempo que llevan esperando. Si no se está enviando ningún mensaje, puede que el programa externo del Correo electrónico de base de datos no esté en ejecución o que un problema de red impida que el Correo electrónico de base de datos se ponga en contacto con los servidores SMTP. Si muchos de los mensajes sin enviar tienen el mismo **profile_id**, puede haber un problema con el servidor SMTP. Considere la posibilidad de agregar cuentas adicionales al perfil. Si se envían los mensajes pero pasan demasiado tiempo en la cola, puede que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesite más recursos para procesar el volumen de mensajes que requiere.  
  
## <a name="permissions"></a>Permisos  
 Se concede al rol fijo de servidor **sysadmin** y al rol de base de datos **DatabaseMailUserRole** . Cuando lo ejecuta un miembro del rol fijo de servidor **sysadmin** , esta vista muestra todos los mensajes no **enviados** o de **reintento** . Todos los demás usuarios solo verán los mensajes no **enviados** o de **reintento** que enviaron.  
  
  
