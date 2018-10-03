---
title: sysmail_event_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ac38c2e54fde2beb02e009e00b9f587e9265a43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781103"
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada mensaje de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelto por el sistema del Correo electrónico de base de datos. El término "mensaje" en el contexto de esta frase hace referencia por ejemplo a un mensaje de error, no de correo de electrónico. Configurar la **Logging Level** parámetro mediante el uso de la **configurar parámetros del sistema** cuadro de diálogo del Asistente para configuración de correo electrónico de base de datos, o la [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)procedimiento almacenado para determinar qué mensajes se devuelven.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|Identificador de elementos del registro.|  
|**event_type**|**varchar (11)**|Tipo de aviso insertado en el registro. Los valores posibles son errores, advertencias, mensajes informativos, mensajes de operación correcta y otros mensajes internos.|  
|**log_date**|**datetime**|Fecha y hora en que se realiza la entrada de registro.|  
|**Descripción**|**nvarchar(max)**|Texto del mensaje que se registra.|  
|**Id**|**int**|Id. de proceso del programa externo del Correo electrónico de base de datos. Suele cambiar cada vez que se inicia el programa externo del Correo electrónico de base de datos.|  
|**mailitem_id**|**int**|Identificador del elemento de correo en la cola de correo electrónico. Su valor será NULL si el mensaje no está relacionado con un elemento de correo electrónico determinado.|  
|**account_id**|**int**|El **account_id** de la cuenta relacionada con el evento. Su valor será NULL si el mensaje no está relacionado con una cuenta de correo electrónico determinada.|  
|**last_mod_date**|**datetime**|Fecha y hora de la modificación más reciente de la fila.|  
|**last_mod_user**|**sysname**|Usuario que realizó la modificación más reciente de la fila. En el caso de los mensajes de correo electrónico, se trata del usuario que envió el mensaje. En el caso de los mensajes generados por el programa externo del Correo electrónico de base de datos, se trata del contexto de usuario del programa.|  
  
## <a name="remarks"></a>Comentarios  
 Para solucionar el problema de correo electrónico de base de datos, buscar el **sysmail_event_log** vista para los eventos relacionados con errores de correo electrónico. Algunos mensajes, como los de error del programa externo del Correo electrónico de base de datos, no están asociados con mensajes de correo electrónico determinados. Para buscar errores relacionados con correos electrónicos específicos, buscar el **mailitem_id** del correo electrónico con errores en el **sysmail_faileditems** ver y, a continuación, buscar el **sysmail_event_log**para mensajes relacionados con la que **mailitem_id**. Cuando se devuelve un error de **sp_send_dbmail**, no se envía el correo electrónico en el sistema de correo electrónico de base de datos y el error no se muestra en esta vista.  
  
 Si se producen errores en los intentos de entrega de cuentas individuales, el Correo electrónico de base de datos conservará los mensajes de error durante los reintentos hasta que la entrega del elemento de correo se realice correctamente o provoque un error. En el caso de éxito final, todos los errores acumulados se registrarán como advertencias independientes con el **account_id**. Por tanto, puede que aparezcan advertencias aunque se haya enviado el mensaje. En caso de error de entrega, se registrarán todas las advertencias anteriores como mensaje de error de uno sin un **account_id**, ya que se han producido un error en todas las cuentas.  
  
## <a name="permissions"></a>Permisos  
 Debe ser un miembro de la **sysadmin** rol fijo de servidor o el **DatabaseMailUserRole** rol de base de datos para tener acceso a esta vista. Los miembros de **DatabaseMailUserRole** que no son miembros de la **sysadmin** rol, solo puede ver los eventos para los correos electrónicos que envíen ellos mismos.  
  
## <a name="see-also"></a>Vea también  
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Programa externo Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
