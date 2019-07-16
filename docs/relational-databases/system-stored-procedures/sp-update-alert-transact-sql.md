---
title: sp_update_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
ms.openlocfilehash: baecdca82d7edcb27196c7c43d9d071a82adf792
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084944"
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza la configuración de una alerta existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` El nombre de la alerta que va a actualizarse. *nombre* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @new_name = ] 'new_name'` Un nuevo nombre para la alerta. El nombre debe ser único. *new_name* es **sysname**, su valor predeterminado es null.  
  
`[ @enabled = ] enabled` Especifica si la alerta está habilitada (**1**) o no habilitada (**0**). *habilitado* es **tinyint**, su valor predeterminado es null. Para poder activar una alerta, ésta debe estar habilitada.  
  
`[ @message_id = ] message_id` Un nuevo número error o mensaje para la definición de alerta. Por lo general, *message_id* corresponde a un número de error en la **sysmessages** tabla. *message_id* es **int**, su valor predeterminado es null. Un mensaje de identificador se puede usar sólo si la configuración del nivel de gravedad de la alerta es **0**.  
  
`[ @severity = ] severity` Un nuevo nivel de gravedad (de **1** a través de **25**) para la definición de alerta. Cualquier [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensaje enviado en el registro de aplicación de Windows con la gravedad especificada activará la alerta. *gravedad* es **int**, su valor predeterminado es null. Un nivel de gravedad se puede usar sólo si la configuración de Id. de mensaje para la alerta es **0**.  
  
`[ @delay_between_responses = ] delay_between_responses` El nuevo período de espera, en segundos, entre respuestas a la alerta. *delay_between_responses* es **int**, su valor predeterminado es null.  
  
`[ @notification_message = ] 'notification_message'` Texto revisado de un mensaje adicional que se envía al operador como parte del correo electrónico, **net send**, o una notificación por buscapersonas. *notification_message* es **nvarchar (512)** , su valor predeterminado es null.  
  
`[ @include_event_description_in = ] include_event_description_in` Especifica si la descripción de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error desde el registro de aplicación de Windows debe incluirse en el mensaje de notificación. *include_event_description_in* es **tinyint**, su valor predeterminado es null, y puede tener uno o varios de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|None|  
|**1**|Correo electrónico|  
|**2**|Buscapersonas|  
|**4**|**net send**|  
|**7**|Todo|  
  
`[ @database_name = ] 'database'` El nombre de la base de datos en el que debe producirse el error para que se desencadene la alerta. *base de datos* es **sysname.** No se permiten nombres incluidos entre corchetes ([ ]). El valor predeterminado es NULL.  
  
`[ @event_description_keyword = ] 'event_description_keyword'` Una secuencia de caracteres que debe encontrarse en la descripción del error en el registro de mensajes de error. Se pueden usar caracteres de coincidencia de patrón de la expresión LIKE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *event_description_keyword* es **nvarchar (100)** , su valor predeterminado es null. Este parámetro resulta útil para filtrar los nombres de objeto (por ejemplo, **% customer_table %** ).  
  
`[ @job_id = ] job_id` El número de identificación del trabajo. *job_id* es **uniqueidentifier**, su valor predeterminado es null. Si *job_id* se especifica, *job_name* debe omitirse.  
  
`[ @job_name = ] 'job_name'` Nombre del trabajo que se ejecuta en respuesta a esta alerta. *job_name* es **sysname**, su valor predeterminado es null. Si *job_name* se especifica, *job_id* debe omitirse.  
  
`[ @occurrence_count = ] occurrence_count` Restablece el número de veces que se ha producido la alerta. *occurrence_count* es **int**, su valor predeterminado es null y se puede establecer solo en **0**.  
  
`[ @count_reset_date = ] count_reset_date` Restablece la fecha en que el recuento de repeticiones se restableció por última vez. *count_reset_date* es **int**, su valor predeterminado es null.  
  
`[ @count_reset_time = ] count_reset_time` Restablece la hora en que el recuento de repeticiones se restableció por última vez. *count_reset_time* es **int**, su valor predeterminado es null.  
  
`[ @last_occurrence_date = ] last_occurrence_date` Restablece la fecha en que se produjo por última vez la alerta. *last_occurrence_date* es **int**, su valor predeterminado es null y se puede establecer solo en **0**.  
  
`[ @last_occurrence_time = ] last_occurrence_time` Restablece la hora en que se produjo por última vez la alerta. *last_occurrence_time* es **int**, su valor predeterminado es null y se puede establecer solo en **0**.  
  
`[ @last_response_date = ] last_response_date` Restablece la fecha de que la última respuesta a la alerta del servicio SQLServerAgent. *last_response_date* es **int**, su valor predeterminado es null y se puede establecer solo en **0**.  
  
`[ @last_response_time = ] last_response_time` Restablece la hora de que la última respuesta a la alerta del servicio SQLServerAgent. *last_response_time* es **int**, su valor predeterminado es null y se puede establecer solo en **0**.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` Reservado.  
  
`[ @performance_condition = ] 'performance_condition'` Un valor expresado en formato **'***itemcomparatorvalue***'** . *performance_condition* es **nvarchar (512)** , su valor predeterminado es null y consta de estos elementos.  
  
|Elemento de formato|Descripción|  
|--------------------|-----------------|  
|*Elemento*|Objeto de rendimiento, contador de rendimiento o instancia con nombre del contador|  
|*Comparador*|Uno de estos operadores: **>** , **<** , **=**|  
|*Valor*|Valor numérico del contador|  
  
`[ @category_name = ] 'category'` El nombre de la categoría de alerta. *categoría* es **sysname** con el valor predeterminado es NULL.  
  
`[ @wmi_namespace = ] 'wmi_namespace'` El espacio de nombres WMI para consultar los eventos. *wmi_namespace* es **sysname**, su valor predeterminado es null.  
  
`[ @wmi_query = ] 'wmi_query'` La consulta que especifica el evento WMI para la alerta. *wmi_query* es **nvarchar (512)** , su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Solo **sysmessages** escribe en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro de aplicación de Windows puede desencadenar una alerta.  
  
 **sp_update_alert** cambia sólo los valores de alerta para el parámetro que se proporcionan los valores. Si se omite un parámetro, se conserva la configuración actual.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, los usuarios deben ser un miembro de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el valor de habilitación de `Test Alert` a `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
