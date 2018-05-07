---
title: sp_add_alert (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd9e96ece5a5b8a3dc39c6246e0f2201bbffab1d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una alerta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] **'***nombre***'**  
 Nombre de la alerta. El nombre aparece en el mensaje de correo electrónico o de buscapersonas enviado como respuesta a la alerta. Debe ser único y puede contener el porcentaje (**%**) caracteres. *nombre* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@message_id =** ] *message_id*  
 El número de error de mensaje que define la alerta. (Normalmente, corresponde a un número de error en la **sysmessages** tabla.) *message_id* es **int**, su valor predeterminado es **0**. Si *gravedad* se utiliza para definir la alerta, *message_id* debe ser **0** o NULL.  
  
> [!NOTE]  
>  Solo **sysmessages** errores escritos en el registro de aplicación de Microsoft Windows pueden provocar que se envíe una alerta.  
  
 [  **@severity =** ] *gravedad*  
 El nivel de gravedad (de **1** a través de **25**) que define la alerta. Cualquier [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensaje almacenado en el **sysmessages** tabla enviado a la [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro de aplicación de Windows con la gravedad indicada hace que se envíe la alerta. *gravedad* es **int**, con un valor predeterminado es 0. Si *message_id* se utiliza para definir la alerta, *gravedad* debe ser **0**.  
  
 [  **@enabled =** ] *habilitado*  
 Indica el estado actual de la alerta. *habilitado* es **tinyint**, su valor predeterminado es 1 (habilitado). Si **0**, la alerta no está habilitada y no se activa.  
  
 [  **@delay_between_responses =** ] *delay_between_responses*  
 El intervalo de espera, en segundos, entre respuestas a la alerta. *delay_between_responses*es **int**, su valor predeterminado es **0**, lo que significa que no hay ninguna espera entre respuestas (cada aparición de la alerta genera una respuesta). La respuesta puede tener lugar de cualquiera de estas formas, o de ambas:  
  
-   Una o más notificaciones enviadas por correo electrónico o el buscapersonas  
  
-   Un trabajo que debe ejecutarse  
  
 Al establecer este valor, es posible evitar, por ejemplo, que se envíen mensajes de correo electrónico no deseados cuando una alerta se produce repetidamente en un período de tiempo breve.  
  
 [  **@notification_message =** ] **'***notification_message***'**  
 Es un mensaje adicional opcional enviado al operador como parte del correo electrónico, **mediante net send**, o una notificación por buscapersonas. *notification_message* es **nvarchar (512)**, su valor predeterminado es null. Especificar *notification_message* es útil para agregar notas especiales como los procedimientos para solucionarlo.  
  
 [  **@include_event_description_in =** ] *include_event_description_in*  
 Indica si la descripción del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se debe incluir como parte del mensaje de notificación. *include_event_description_in*es **tinyint**, su valor predeterminado es **5** (correo electrónico y **mediante net send**) y puede tener uno o varios de estos valores combinados con un **o** operador lógico.  
  
> [!IMPORTANT]  
>  Las opciones Buscapersonas y **net send** se quitarán del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar estas características en los nuevos trabajos de programación y planee modificar las aplicaciones que actualmente las utilizan.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|None|  
|**1**|Correo electrónico|  
|**2**|Buscapersonas|  
|**4**|**net send**|  
  
 [ **@database_name =** ] **'***database***'**  
 Base de datos en la que debe ocurrir el error para que se active la alerta. Si *base de datos*no se proporciona, la alerta se activa independientemente de donde se produjo el error. *base de datos* es **sysname**. No se permiten nombres incluidos entre corchetes ([ ]). El valor predeterminado es NULL.  
  
 [  **@event_description_keyword =** ] **'***vent_description_pattern***'**  
 Secuencia de caracteres a la que debe parecerse la descripción del error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se pueden usar caracteres de coincidencia de patrón de la expresión LIKE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *vent_description_pattern* es **nvarchar (100)**, su valor predeterminado es null. Este parámetro resulta útil para filtrar nombres de objeto (por ejemplo, **% customer_table %**).  
  
 [  **@job_id =** ] *job_id*  
 El número de identificación del trabajo que se ejecutará en respuesta a esta alerta. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name =** ] **'***job_name***'**  
 El nombre del trabajo que se ejecutará en respuesta a esta alerta. *job_name*es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@raise_snmp_trap =** ] *raise_snmp_trap*  
 No se implementa en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0. *raise_snmp_trap* es **tinyint**, con un valor predeterminado es 0.  
  
 [  **@performance_condition =** ] **'***performance_condition***'**  
 Es un valor expresado en el formato '*itemcomparatorvalue*'. *performance_condition* es **nvarchar (512)** con un valor predeterminado es NULL y consta de estos elementos.  
  
|Elemento de formato|Description|  
|--------------------|-----------------|  
|*Elemento*|Objeto de rendimiento, contador de rendimiento o instancia con nombre del contador|  
|*Comparador*|Uno de estos operadores: >, < o =.|  
|*Valor*|Valor numérico del contador|  
  
 [  **@category_name =** ] **'***categoría***'**  
 El nombre de la categoría de alerta. *categoría* es **sysname**, su valor predeterminado es null.  
  
 [ **@wmi_namespace**=] **'***wmi_namespace***'**  
 Es el espacio de nombres WMI para consultar eventos. *wmi_namespace* es **sysname**, su valor predeterminado es null. Solo se admiten espacios de nombres del servidor local.  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 La consulta que especifica el evento WMI para la alerta. *wmi_query* es **nvarchar (512)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_add_alert** se debe ejecutar desde la **msdb** base de datos.  
  
 Estas son las circunstancias en las que los errores y mensajes que generan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se envían al registro de aplicación Windows y que, por lo tanto, pueden generar alertas:  
  
-   Gravedad 19 o superior **sys.messages** errores  
  
-   Cualquier instrucción RAISERROR llamada con la sintaxis WITH LOG  
  
-   Cualquier **sys.messages** error modificados o creados mediante **sp_altermessage**  
  
-   Eventos registrados mediante **xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona una forma gráfica y fácil de administrar todo el sistema de alertas, y constituye el método recomendado para configurar una infraestructura de alertas.  
  
 Si una alerta no funciona correctamente, compruebe lo siguiente:  
  
-   El servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando.  
  
-   El evento ha aparecido en el registro de aplicación Windows.  
  
-   La alerta está habilitada.  
  
-   Los eventos generados durante **xp_logevent** se producen en la base de datos maestra. Por tanto, **xp_logevent** no desencadena una alerta a menos que el valor de **@database_name** de la alerta sea is **'master'** o NULL.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_add_alert**.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra cómo agregar una alerta (Test Alert) que ejecute el trabajo `Back up the AdventureWorks2012 Database` al activarse.  
  
> [!NOTE]  
>  En el ejemplo se da por supuesto que el mensaje 55001 y el trabajo `Back up the AdventureWorks2012 Database` ya existen. El siguiente es solo un ejemplo.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
