---
title: sp_update_jobstep (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4708d2cfe45f192a80836f592e3f774378eeb03e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de un paso de un trabajo que se utiliza para realizar actividades automatizadas.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
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
 [  **@job_id =**] *job_id*  
 Número de identificación del trabajo al que perteneces el paso. *job_id*es **uniqueidentifier**, su valor predeterminado es null. Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@job_name =**] **'***job_name***'**  
 El nombre del trabajo al que pertenece el paso. *job_name*es **sysname**, su valor predeterminado es null. Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@step_id =**] *step_id*  
 Número de identificación del paso de trabajo que va a modificarse. Este número no puede modificarse. *step_id*es **int**, no tiene ningún valor predeterminado.  
  
 [  **@step_name =**] **'***step_name***'**  
 Es el nombre nuevo del paso. *Step_name*es **sysname**, su valor predeterminado es null.  
  
 [  **@subsystem =**] **'***subsistema***'**  
 El subsistema que utiliza el agente de Microsoft SQL Server para ejecutar *comando*. *subsistema* es **nvarchar (40)**, su valor predeterminado es null.  
  
 [  **@command =**] **'***comando***'**  
 Los comandos que se ejecutará a través de *subsistema*. *comando* es **nvarchar (max)**, su valor predeterminado es null.  
  
 [  **@additional_parameters =**] **'***parámetros***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@cmdexec_success_code =**] *success_code*  
 El valor devuelto por un **CmdExec** comando del subsistema para indicar que *comando* ejecutado correctamente. *success_code* es **int**, su valor predeterminado es null.  
  
 [  **@on_success_action =**] *success_action*  
 La acción que se realizará si el paso termina correctamente. *success_action* es **tinyint**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Valor|Descripción (acción)|  
|-----------|----------------------------|  
|**1**|Salir correctamente.|  
|**2**|Salir con error.|  
|**3**|Ir al paso siguiente.|  
|**4**|Vaya al paso *success_step_id.*|  
  
 [  **@on_success_step_id =**] *success_step_id*  
 El número de identificación del paso de este trabajo que se ejecutará si el paso termina correctamente y *success_action* es **4**. *success_step_id* es **int**, su valor predeterminado es null.  
  
 [  **@on_fail_action =**] *fail_action*  
 La acción que se realizará si se produce un error en el paso. *fail_action* es **tinyint**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Valor|Descripción (acción)|  
|-----------|----------------------------|  
|**1**|Salir correctamente.|  
|**2**|Salir con error.|  
|**3**|Ir al paso siguiente.|  
|**4**|Vaya al paso *fail_step_id**.*|  
  
 [  **@on_fail_step_id =**] *fail_step_id.*  
 El número de identificación del paso de este trabajo que se ejecutará si se produce un error en el paso y *fail_action* es **4**. *fail_step_id* es **int**, su valor predeterminado es null.  
  
 [  **@server =**] **'***server***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*server* es **nvarchar (128)**, su valor predeterminado es null.  
  
 [  **@database_name =**] **'***base de datos***'**  
 Nombre de la base de datos en la que se va a ejecutar un paso de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *base de datos*es **sysname**. No se permiten nombres incluidos entre corchetes ([ ]). El valor predeterminado es NULL.  
  
 [  **@database_user_name =**] **'***usuario***'**  
 El nombre de la cuenta de usuario que se va a utilizar al ejecutar un paso de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *usuario*es **sysname**, su valor predeterminado es null.  
  
 [  **@retry_attempts =**] *retry_attempts*  
 Número de reintentos en caso de que el paso dé error. *retry_attempts*es **int**, su valor predeterminado es null.  
  
 [  **@retry_interval =**] *retry_interval*  
 Tiempo en minutos entre reintentos. *retry_interval* es **int**, su valor predeterminado es null.  
  
 [  **@os_run_priority =**] *run_priority*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@output_file_name =**] **'***file_name***'**  
 Nombre del archivo en el que se guarda el resultado de este paso. *file_name* es **nvarchar (200)**, su valor predeterminado es null. Este parámetro solo es válido con comandos que se ejecutan en subsistemas [!INCLUDE[tsql](../../includes/tsql-md.md)] o CmdExec.  
  
 Para restablecer output_file_name en NULL, debe establecer *nombre_archivo_de_salida* en una cadena vacía (' ') o en una cadena de caracteres en blanco, pero no se puede usar el **CHAR(32)** (función). Por ejemplo, establezca este argumento en una cadena vacía del modo siguiente:  
  
 **@output_file_name = ' '**  
  
 [  **@flags =**] *marcas*  
 Una opción que controla el comportamiento. *marcas de* es **int**, y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Sobrescribir el archivo de salida.|  
|**2**|Anexar al archivo de salida|  
|**4**|Escribir la salida del paso de trabajo Transact-SQL en el historial de pasos|  
|**8**|Escribir el registro en la tabla (sobrescribir el historial existente)|  
|**16**|Escribir el registro en la tabla (anexar al historial existente)|  
  
 [  **@proxy_id** =] *proxy_id*  
 Número de identificación del proxy con el que se ejecuta el paso de trabajo. *proxy_id* es de tipo **int**, su valor predeterminado es null. Si no hay ningún *proxy_id* se especifica, no *proxy_name* se especifica y no *nombre_usuario* se especifica, el paso de trabajo se ejecuta como la cuenta de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
 [  **@proxy_name** =] **'***proxy_name***'**  
 Nombre del proxy con el que se ejecuta el paso de trabajo. *proxy_name* es de tipo **sysname**, su valor predeterminado es null. Si no hay ningún *proxy_id* se especifica, no *proxy_name* se especifica y no *nombre_usuario* se especifica, el paso de trabajo se ejecuta como la cuenta de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_update_jobstep** se debe ejecutar desde la **msdb** base de datos.  
  
 La actualización de un paso de trabajo incrementa el número de la versión del trabajo.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Solo los miembros del **sysadmin** puede actualizar un paso de trabajo pertenece a otro usuario.  
  
 Si el paso de trabajo requiere acceso a un proxy, el creador del paso de trabajo debe tener acceso al proxy del paso de trabajo. Todos los subsistemas, excepto Transact-SQL, necesitan una cuenta de proxy. Los miembros de **sysadmin** tienen acceso a todos los servidores proxy y puede usar la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente para el proxy.  
  
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
 [Ver o modificar trabajos](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_delete_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
