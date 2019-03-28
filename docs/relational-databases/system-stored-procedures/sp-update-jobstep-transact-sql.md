---
title: sp_update_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1ab6c1408b9f9c2de2e4070ab35e34ea8a458df
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526767"
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de un paso de un trabajo que se utiliza para realizar actividades automatizadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` El número de identificación del trabajo al que pertenece el paso. *job_id*es **uniqueidentifier**, su valor predeterminado es null. Cualquier *job_id* o *job_name* debe especificarse, pero no se pueden especificar ambos.  
  
`[ @job_name = ] 'job_name'` El nombre del trabajo al que pertenece el paso. *job_name*es **sysname**, su valor predeterminado es null. Cualquier *job_id* o *job_name* debe especificarse, pero no se pueden especificar ambos.  
  
`[ @step_id = ] step_id` El número de identificación del paso de trabajo va a modificar. Este número no puede modificarse. *step_id*es **int**, no tiene ningún valor predeterminado.  
  
`[ @step_name = ] 'step_name'` Es un nuevo nombre para el paso. *Step_name*es **sysname**, su valor predeterminado es null.  
  
`[ @subsystem = ] 'subsystem'` El subsistema utilizado por el agente de Microsoft SQL Server para ejecutar *comando*. *subsistema* es **nvarchar (40)**, su valor predeterminado es null.  
  
`[ @command = ] 'command'` Los comandos que se ejecutará a través de *subsistema*. *comando* es **nvarchar (max)**, su valor predeterminado es null.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code` El valor devuelto por un **CmdExec** comando del subsistema para indicar que *comando* se ha ejecutado correctamente. *success_code* es **int**, su valor predeterminado es null.  
  
`[ @on_success_action = ] success_action` La acción que se realizará si el paso termina correctamente. *success_action* es **tinyint**, su valor predeterminado es null, y puede tener uno de estos valores.  
  
|Valor|Descripción (acción)|  
|-----------|----------------------------|  
|**1**|Salir correctamente.|  
|**2**|Salir con error.|  
|**3**|Ir al paso siguiente.|  
|**4**|Vaya al paso *success_step_id.*|  
  
`[ @on_success_step_id = ] success_step_id` El número de identificación del paso de este trabajo que se ejecutará si el paso se realiza correctamente y *success_action* es **4**. *success_step_id* es **int**, su valor predeterminado es null.  
  
`[ @on_fail_action = ] fail_action` La acción que se realizará si se produce un error en el paso. *fail_action* es **tinyint**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Valor|Descripción (acción)|  
|-----------|----------------------------|  
|**1**|Salir correctamente.|  
|**2**|Salir con error.|  
|**3**|Ir al paso siguiente.|  
|**4**|Vaya al paso *fail_step_id **.*|  
  
`[ @on_fail_step_id = ] fail_step_id` El número de identificación del paso de este trabajo que se ejecutará si se produce un error en el paso y *fail_action* es **4**. *fail_step_id* es **int**, su valor predeterminado es null.  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *servidor* es **nvarchar (128)**, su valor predeterminado es null.  
  
`[ @database_name = ] 'database'` El nombre de la base de datos en el que se va a ejecutar un [!INCLUDE[tsql](../../includes/tsql-md.md)] paso. *base de datos*es **sysname**. No se permiten nombres incluidos entre corchetes ([ ]). El valor predeterminado es NULL.  
  
`[ @database_user_name = ] 'user'` El nombre de la cuenta de usuario debe usar al ejecutar un [!INCLUDE[tsql](../../includes/tsql-md.md)] paso. *usuario*es **sysname**, su valor predeterminado es null.  
  
`[ @retry_attempts = ] retry_attempts` El número de reintentos intenta utilizar si se produce un error en este paso. *retry_attempts*es **int**, su valor predeterminado es null.  
  
`[ @retry_interval = ] retry_interval` La cantidad de tiempo en minutos entre reintentos. *retry_interval* es **int**, su valor predeterminado es null.  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'` El nombre del archivo que se guarda la salida de este paso. *file_name* es **nvarchar (200)**, su valor predeterminado es null. Este parámetro solo es válido con comandos que se ejecutan en subsistemas [!INCLUDE[tsql](../../includes/tsql-md.md)] o CmdExec.  
  
 Para restablecer output_file_name en NULL, se debe establecer *nombre_archivo_de_salida* en una cadena vacía (' ') o en una cadena de caracteres en blanco, pero no se puede usar el **CHAR(32)** función. Por ejemplo, establezca este argumento en una cadena vacía del modo siguiente:  
  
 **@output_file_name = ' '**  
  
`[ @flags = ] flags` Una opción que controla el comportamiento. *marcas* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Sobrescribir el archivo de salida.|  
|**2**|Anexar al archivo de salida|  
|**4**|Escribir la salida del paso de trabajo Transact-SQL en el historial de pasos|  
|**8**|Escribir el registro en la tabla (sobrescribir el historial existente)|  
|**16**|Escribir el registro en la tabla (anexar al historial existente)|  
  
`[ @proxy_id = ] proxy_id` Número de identificación del proxy que se ejecuta el paso de trabajo. *proxy_id* es de tipo **int**, su valor predeterminado es null. Si no hay ningún *proxy_id* se especifica, no hay *proxy_name* se especifica y no *user_name* se especifica, el paso de trabajo se ejecuta como la cuenta de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
`[ @proxy_name = ] 'proxy_name'` El nombre del servidor proxy que se ejecuta el paso de trabajo. *proxy_name* es de tipo **sysname**, su valor predeterminado es null. Si no hay ningún *proxy_id* se especifica, no hay *proxy_name* se especifica y no *user_name* se especifica, el paso de trabajo se ejecuta como la cuenta de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_update_jobstep** se debe ejecutar desde la **msdb** base de datos.  
  
 La actualización de un paso de trabajo incrementa el número de la versión del trabajo.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo los miembros del **sysadmin** puede actualizar un paso de trabajo pertenece a otro usuario.  
  
 Si el paso de trabajo requiere acceso a un proxy, el creador del paso de trabajo debe tener acceso al proxy del paso de trabajo. Todos los subsistemas, excepto Transact-SQL, necesitan una cuenta de proxy. Los miembros de **sysadmin** tienen acceso a todos los servidores proxy y puede usar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente para el proxy.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se modifica el número de reintentos para el primer paso del trabajo `Weekly Sales Data Backup`. Después de ejecutar este ejemplo, el número de reintentos es `10`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Ver o modificar trabajos](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
