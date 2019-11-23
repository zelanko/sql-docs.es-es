---
title: sp_add_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
author: stevestein
ms.author: sstein
ms.openlocfilehash: b679f34e16b0f22018357f3c6fd6a531d283b2bc
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2019
ms.locfileid: "70810542"
---
# <a name="sp_add_jobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Agrega un paso (operación) a un trabajo del Agente SQL.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > En [instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), se admiten la mayoría de los tipos de trabajo de Agente SQL Server, pero no todos. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.
  
## <a name="syntax"></a>Sintaxis  
  
```
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'   
     [ , [ @step_id = ] step_id ]   
     { , [ @step_name = ] 'step_name' }   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @command = ] 'command' ]   
     [ , [ @additional_parameters = ] 'parameters' ]   
          [ , [ @cmdexec_success_code = ] code ]   
     [ , [ @on_success_action = ] success_action ]   
          [ , [ @on_success_step_id = ] success_step_id ]   
          [ , [ @on_fail_action = ] fail_action ]   
          [ , [ @on_fail_step_id = ] fail_step_id ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @database_user_name = ] 'user' ]   
     [ , [ @retry_attempts = ] retry_attempts ]   
     [ , [ @retry_interval = ] retry_interval ]   
     [ , [ @os_run_priority = ] run_priority ]   
     [ , [ @output_file_name = ] 'file_name' ]   
     [ , [ @flags = ] flags ]   
     [ , { [ @proxy_id = ] proxy_id   
         | [ @proxy_name = ] 'proxy_name' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` el número de identificación del trabajo al que se va a agregar el paso. *job_id* es de tipo **uniqueidentifier**y su valor predeterminado es NULL.  
  
`[ @job_name = ] 'job_name'` el nombre del trabajo al que se va a agregar el paso. *job_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos.  
  
`[ @step_id = ] step_id` el número de identificación de la secuencia para el paso de trabajo. Los números de identificación de los pasos empiezan en **1** y se incrementan sin huecos. Si se inserta un paso en la secuencia existente, los números de secuencia se ajustan automáticamente. Si no se especifica *step_id* , se proporciona un valor. *step_id* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @step_name = ] 'step_name'` el nombre del paso. *step_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @subsystem = ] 'subsystem'` el subsistema utilizado por el servicio del agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar el *comando*. el *subsistema* es **nvarchar (40)** y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**'|Script Active<br /><br /> **\*\* Importante \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|Comando del sistema operativo o programa ejecutable|  
|'**Distribución**'|Trabajo del Agente de distribución de replicación|  
|'**Snapshot**'|Trabajo del Agente de instantáneas de replicación|  
|'**Lector de registro**'|Trabajo del Agente de registro del LOG de replicación|  
|'**Merge**'|Trabajo del Agente de mezcla de replicación|  
|'**QueueReader**'|Trabajo del Agente de lectura de cola de replicación|  
|'**ANALYSISQUERY**'|Consulta de Analysis Services (MDX, DMX)|  
|'**ANALYSISCOMMAND**'|Comando de Analysis Services (XMLA)|  
|'**DTS**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ejecución de paquetes|  
|'**PowerShell**'|Script de PowerShell|  
|'**Tsql**' (predeterminado)|Instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]|  
  
`[ @command = ] 'command'` los comandos que va a ejecutar el servicio **SQLServerAgent** a través *del subsistema*. el *comando* es de tipo **nvarchar (Max)** y su valor predeterminado es NULL. El Agente SQL Server proporciona sustitución de tokens, que ofrece la misma flexibilidad que ofrecen las variables al escribir programas de software.  
  
> [!IMPORTANT]  
>  Todos los tokens que se usan en pasos de trabajo deben adjuntar ahora una macro de escape; de lo contrario, esos pasos de trabajo producirán un error. Además, ahora debe escribir los nombres de los tokens entre paréntesis y colocar un signo de dólar (`$`) al principio de la sintaxis del token. Por ejemplo:  
>   
>  `$(ESCAPE_` *nombre de macro* `(DATE))`  
  
 Para obtener más información sobre estos tokens y la actualización de los pasos de trabajo para usar la nueva sintaxis de token, consulte [usar tokens en pasos de trabajo](../../ssms/agent/use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
>  Todos los usuarios de Windows que tengan permisos de escritura en el Registro de eventos de Windows pueden tener acceso a los pasos de trabajo activados por alertas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de WMI. Para evitar este riesgo de seguridad, se deshabilitan de manera predeterminada los tokens del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pueden utilizarse en trabajos activados por alertas. Estos tokens son: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**y **WMI(** _propiedad_ **)** . Tenga en cuenta que en esta versión el uso de los tokens se ha ampliado a todas las alertas.  
>   
>  Si necesita usar estos tokens, asegúrese primero de que solo los miembros de los grupos de seguridad de Windows de confianza, como el grupo Administradores, tienen permisos de escritura en el registro de eventos del equipo donde reside [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A continuación, para habilitar estos tokens, haga clic con el botón derecho en **Agente SQL Server** en el Explorador de objetos, elija **Propiedades** y, en la página **Sistema de alerta**, active la casilla **Reemplazar tokens para todas las respuestas de trabajos a alertas**.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *parámetros* es **ntext**y su valor predeterminado es NULL.  
  
`[ @cmdexec_success_code = ] code` el valor devuelto por un comando del subsistema **CmdExec** para indicar que el *comando* se ejecutó correctamente. el *código* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @on_success_action = ] success_action` la acción que se realizará si el paso se realiza correctamente. *success_action* es **tinyint**y puede tener uno de estos valores.  
  
|Valor|Descripción (acción)|  
|-----------|----------------------------|  
|**1** (predeterminado)|Salir con éxito|  
|**2**|Salir con error|  
|**3**|Ir al paso siguiente|  
|**4**|Vaya al paso *on_success_step_id*|  
  
`[ @on_success_step_id = ] success_step_id` el identificador del paso de este trabajo que se va a ejecutar si el paso se realiza correctamente y *success_action* es **4**. *success_step_id* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @on_fail_action = ] fail_action` la acción que se realizará si se produce un error en el paso. *fail_action* es **tinyint**y puede tener uno de estos valores.  
  
|Valor|Descripción (acción)|  
|-----------|----------------------------|  
|**1**|Salir con éxito|  
|**2** (predeterminado)|Salir con error|  
|**3**|Ir al paso siguiente|  
|**4**|Vaya al paso *on_fail_step_id*|  
  
`[ @on_fail_step_id = ] fail_step_id` el identificador del paso de este trabajo que se va a ejecutar si se produce un error en el paso y *fail_action* es **4**. *fail_step_id* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *Server* es **nvarchar (30)** y su valor predeterminado es NULL.  
  
`[ @database_name = ] 'database'` el nombre de la base de datos en la que se va a ejecutar un paso de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *Database* es de **tipo sysname y su**valor predeterminado es null, en cuyo caso se utiliza la base de datos **maestra** . No se permiten nombres incluidos entre corchetes ([ ]). En un paso de trabajo de ActiveX, la *base de datos* es el nombre del lenguaje de scripting que usa el paso.  
  
`[ @database_user_name = ] 'user'` el nombre de la cuenta de usuario que se va a usar al ejecutar un paso de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *User* es de **tipo sysname y su**valor predeterminado es NULL. Cuando *User* es null, el paso se ejecuta en el contexto de usuario del propietario del trabajo en la *base de datos*.  El Agente SQL Server solo incluirá este parámetro si el propietario del trabajo es un administrador de sistema de SQL Server. En ese caso, el paso de Transact-SQL dado se ejecutará en el contexto del nombre de usuario de SQL Server determinado. Si el propietario del trabajo no es un SQL Server sysadmin, el paso de Transact-SQL siempre se ejecutará en el contexto del inicio de sesión que posee este trabajo y se omitirá el parámetro @database_user_name.  
  
`[ @retry_attempts = ] retry_attempts` el número de reintentos que se deben usar si se produce un error en este paso. *retry_attempts* es de **tipo int**y su valor predeterminado es **0**, que indica que no hay reintentos.  
  
`[ @retry_interval = ] retry_interval` la cantidad de tiempo en minutos entre reintentos. *retry_interval* es de **tipo int**y su valor predeterminado es **0**, que indica un intervalo de **0**minutos.  
  
`[ @os_run_priority = ] run_priority` reservado.  
  
`[ @output_file_name = ] 'file_name'` el nombre del archivo en el que se guarda la salida de este paso. *file_name* es de tipo **nvarchar (200)** y su valor predeterminado es NULL. *file_name* puede incluir uno o varios de los tokens enumerados en *comando*. Este parámetro solo es válido con los comandos que se ejecutan en los subsistemas [!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, **PowerShell**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
`[ @flags = ] flags` es una opción que controla el comportamiento. *Flags* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Sobrescribir el archivo de salida|  
|**2**|Anexar al archivo de salida|  
|**4**|Escribir la salida del paso de trabajo [!INCLUDE[tsql](../../includes/tsql-md.md)] en el historial de pasos|  
|**8**|Escribir el registro en la tabla (sobrescribir el historial existente)|  
|**16**|Escribir el registro en la tabla (anexar al historial existente)|  
|**32**|Escribir todo el resultado en el historial de trabajos|  
|**64**|Crear un evento Windows para usarlo como señal y que se anule el paso de trabajo de Cmd|  
  
`[ @proxy_id = ] proxy_id` el número de identificación del proxy con el que se ejecuta el paso de trabajo. *proxy_id* es de tipo **int**y su valor predeterminado es NULL. Si no se especifica ningún *proxy_id* , no se especifica ningún *proxy_name* y no se especifica ningún *user_name* , el paso de trabajo se ejecuta como la cuenta de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
`[ @proxy_name = ] 'proxy_name'` el nombre del proxy con el que se ejecuta el paso de trabajo. *proxy_name* es de tipo **sysname y su**valor predeterminado es NULL. Si no se especifica ningún *proxy_id* , no se especifica ningún *proxy_name* y no se especifica ningún *user_name* , el paso de trabajo se ejecuta como la cuenta de servicio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Remarks  
 **sp_add_jobstep** se debe ejecutar desde la base de datos **msdb** .  
  
 SQL Server Management Studio ofrece un método gráfico sencillo para administrar trabajos y es el método recomendado para crear y administrar la infraestructura de trabajo.  
  
 Un paso de trabajo debe especificar un proxy a menos que el creador del paso de trabajo sea miembro del rol fijo de seguridad **sysadmin** .  
  
 Un proxy puede identificarse mediante *proxy_name* o *proxy_id*.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 El creador del paso de trabajo debe tener acceso al proxy para el paso de trabajo. Los miembros del rol fijo de servidor **sysadmin** tienen acceso a todos los servidores proxy. Se debe conceder acceso al proxy de forma explícita al resto de los usuarios.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se crea un paso de trabajo que cambia el acceso a la base de datos de modo que sea de solo lectura para la base de datos Sales. Además, en este ejemplo se especifican 5 reintentos, cada uno de los cuales se produce tras una espera de 5 minutos.  
  
> [!NOTE]  
>  En este ejemplo se da por supuesto que el trabajo de `Weekly Sales Data Backup` ya existe.  
  
```sql
USE msdb;  
GO  
EXEC sp_add_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_name = N'Set database to read only',  
    @subsystem = N'TSQL',  
    @command = N'ALTER DATABASE SALES SET READ_ONLY',
    @retry_attempts = 5,  
    @retry_interval = 5 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Ver o modificar trabajos](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
