---
title: sysmail_unsentitems (Transact-SQL) | Documentos de Microsoft
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
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs: TSQL
helpviewer_keywords: sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a7147621db09dfc1c29077f82cc3eadb39b3c5b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailunsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada mensaje de correo electrónico de base de datos con la **sin enviar** o **reintentando** estado. Los mensajes con el estado unsent o retrying siguen en la cola de correo y pueden ser enviados en cualquier momento. Los mensajes pueden tener la **sin enviar** estado por las razones siguientes:  
  
-   El mensaje es nuevo y, aunque se ha colocado en la cola de correo, el Correo electrónico de base de datos está ocupado con otros mensajes y aún no ha alcanzado éste.  
  
-   El programa externo del Correo electrónico de base de datos no está en ejecución y no se envía ningún mensaje.  
  
 Los mensajes pueden tener la **reintentando** estado por las razones siguientes:  
  
-   El Correo electrónico de base de datos intentó enviar el mensaje, pero no se pudo contactar con el servidor de correo SMTP. El Correo electrónico de base de datos seguirá intentando enviar el mensaje con otras cuentas propias asignadas al perfil que envió el mensaje. Si no hay ninguna cuenta puede enviar el correo electrónico, correo electrónico de base de datos va a esperar el período de tiempo configurado para el **entre reintentos de cuenta** parámetro y vuelva a intentar enviar el mensaje de nuevo. Base de datos utiliza correo electrónico la **reintentos de cuenta** parámetro para determinar cuántas veces debe para intentar enviar el mensaje. Los mensajes conservan **reintentando** siempre que está intentando enviar el mensaje de correo electrónico de base de datos de estado.  
  
 Utilice esta vista cuando desee ver cuántos mensajes hay en espera para ser enviados y cuánto tiempo llevan en la cola de correo. Normalmente, el número de **sin enviar** mensajes será bajos. Realice una prueba comparativa durante las operaciones normales para determinar un número razonable de mensajes en la cola para las operaciones.  
  
 Para ver todos los mensajes procesados por el correo electrónico de base de datos, utilice [sysmail_allitems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). Para ver sólo los mensajes con el estado de error, utilice [sysmail_faileditems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). Para ver sólo los mensajes que se enviaron, use [sysmail_sentitems &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|Identificador del elemento de correo en la cola de correo electrónico.|  
|**profile_id**|**int**|El identificador del perfil utilizado para enviar el mensaje.|  
|**destinatarios**|**varchar(max)**|Direcciones de correo electrónico de los destinatarios de mensajes.|  
|**copy_recipients**|**varchar(max)**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje.|  
|**blind_copy_recipients**|**varchar(max)**|Direcciones de correo electrónico de los destinatarios que reciben copias del mensaje pero cuyos nombres no aparecen en el encabezado del mensaje.|  
|**Asunto**|**nvarchar(510)**|Línea de asunto del mensaje.|  
|**cuerpo**|**varchar(max)**|El cuerpo del mensaje.|  
|**body_format**|**varchar (20)**|El formato del cuerpo del mensaje. Los valores posibles son **texto** y **HTML**.|  
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
|**send_request_user**|**sysname**|Usuario que envió el mensaje. Se trata del contexto de usuario del procedimiento del correo electrónico de base de datos, no el **de** campo del mensaje.|  
|**sent_account_id**|**int**|Identificador de la cuenta del Correo electrónico de base de datos utilizada para enviar el mensaje. Siempre es NULL para esta vista.|  
|**sent_status**|**varchar (8)**|Será **sin enviar** si el correo electrónico de base de datos no ha intentado enviar el correo electrónico. Será **reintentando** si el correo electrónico de base de datos no pudo enviar el mensaje pero está intentando de nuevo.|  
|**sent_date**|**datetime**|Fecha y hora en las que el Correo electrónico de base de datos intentó por última vez enviar el mensaje. Será NULL si el Correo electrónico de base de datos no ha intentado enviar el mensaje.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila.|  
  
## <a name="remarks"></a>Comentarios  
 Al solucionar problemas del Correo electrónico de base de datos, puede que esta vista le ayude a identificar la naturaleza del problema, pues en ella se muestra el número de mensajes a la espera de ser enviados y el tiempo que llevan esperando. Si no se está enviando ningún mensaje, puede que el programa externo del Correo electrónico de base de datos no esté en ejecución o que un problema de red impida que el Correo electrónico de base de datos se ponga en contacto con los servidores SMTP. Si muchos de los mensajes sin enviar tienen el mismo **profile_id**, puede haber un problema con el servidor SMTP. Considere la posibilidad de agregar cuentas adicionales al perfil. Si se envían los mensajes pero pasan demasiado tiempo en la cola, puede que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesite más recursos para procesar el volumen de mensajes que requiere.  
  
## <a name="permissions"></a>Permissions  
 Concede a **sysadmin** rol fijo de servidor y **DatabaseMailUserRole** rol de base de datos. Cuando se ejecuta un miembro de la **sysadmin** rol fijo de servidor, esta vista muestra todos los **sin enviar** o **reintentando** mensajes. Todos los demás usuarios verán únicamente los **sin enviar** o **reintentando** mensajes que envíen ellos mismos.  
  
  
