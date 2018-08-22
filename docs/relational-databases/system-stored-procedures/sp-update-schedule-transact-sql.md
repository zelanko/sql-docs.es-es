---
title: sp_update_schedule (Transact-SQL) | Microsoft Docs
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
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab45f997cbe9713a5d48646884c61ee5eaf967dc
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393324"
---
# <a name="spupdateschedule-transact-sql"></a>sp_update_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de una programación del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@schedule_id =** ] *schedule_id*  
 Identificador de la programación que se va a modificar. *schedule_id* es **int**, no tiene ningún valor predeterminado. Cualquier *schedule_id* o *schedule_name* debe especificarse.  
  
 [  **@name =** ] **'***schedule_name***'**  
 Nombre de la programación que se va a modificar. *schedule_name*es **sysname**, no tiene ningún valor predeterminado. Cualquier *schedule_id* o *schedule_name* debe especificarse.  
  
 [ **@new_name**= ] *new_name*  
 El nuevo nombre para la programación. *new_name* es **sysname**, su valor predeterminado es null. Cuando *new_name* es NULL, el nombre de la programación se ha modificado.  
  
 [  **@enabled =** ] *habilitado*  
 Indica el estado actual de la programación. *habilitado*es **tinyint**, su valor predeterminado es **1** (habilitado). Si **0**, la programación no está habilitada. Si la programación no está habilitada, no se ejecuta ningún trabajo en esta programación.  
  
 [ **@freq_type =** ] *freq_type*  
 Valor que indica cuándo se va a ejecutar un trabajo. *freq_type*es **int**, su valor predeterminado es **0**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente, relativo a *freq_interval*|  
|**64**|Se ejecuta cuando se inicia el servicio SQLServerAgent|  
|**128**|Cuando el equipo esté inactivo|  
  
 [ **@freq_interval =** ] *freq_interval*  
 Días en que se ejecuta un trabajo. *freq_interval* es **int**, su valor predeterminado es **0**y depende del valor de *freq_type*.  
  
|Valor de *freq_type*|Efecto en *freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (una vez)|*freq_interval* no se utiliza.|  
|**4** (diariamente)|Cada *freq_interval* días.|  
|**8** (semanalmente)|*freq_interval* es uno o varios de los siguientes (combinados con un **OR** operador lógico):<br /><br /> **1** = el domingo<br /><br /> **2** = el lunes<br /><br /> **4** = el martes<br /><br /> **8** = el miércoles<br /><br /> **16** = el jueves<br /><br /> **32** = el viernes<br /><br /> **64** = el sábado|  
|**16** (mensual)|En el *freq_interval* día del mes.|  
|**32** (relativo mensual)|*freq_interval* es uno de los siguientes:<br /><br /> **1** = el domingo<br /><br /> **2** = el lunes<br /><br /> **3** = el martes<br /><br /> **4** = el miércoles<br /><br /> **5** = el jueves<br /><br /> **6** = el viernes<br /><br /> **7** = el sábado<br /><br /> **8** = día<br /><br /> **9** = día de la semana<br /><br /> **10** = día del fin de semana|  
|**64** (cuando se inicia el servicio SQLServerAgent)|*freq_interval* no se utiliza.|  
|**128**|*freq_interval* no se utiliza.|  
  
 [ **@freq_subday_type =** ] *freq_subday_type*  
 Especifica las unidades de *freq_subday_interval **.* *freq_subday_type*es **int**, su valor predeterminado es **0**, y puede tener uno de estos valores.  
  
|Valor|Descripción (unidad)|  
|-----------|--------------------------|  
|**0x1**|A la hora especificada|  
|**0x2**|Segundos|  
|**0x4**|Minutos|  
|**0x8**|Horas|  
  
 [ **@freq_subday_interval =** ] *freq_subday_interval*  
 El número de *freq_subday_type* períodos que transcurren entre cada ejecución de un trabajo. *freq_subday_interval*es **int**, su valor predeterminado es **0**.  
  
 [ **@freq_relative_interval =** ] *freq_relative_interval*  
 Aparición de un trabajo de *freq_interval* en cada mes, si *freq_interval* es **32** (relativo mensual). *freq_relative_interval*es **int**, su valor predeterminado es **0**, y puede tener uno de estos valores.  
  
|Valor|Descripción (unidad)|  
|-----------|--------------------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 [ **@freq_recurrence_factor =** ] *freq_recurrence_factor*  
 Número de semanas o meses entre las ejecuciones programadas de un trabajo. *freq_recurrence_factor* solo se usa si *freq_type* es **8**, **16**, o **32**. *freq_recurrence_factor*es **int**, su valor predeterminado es **0**.  
  
 [ **@active_start_date =** ]  *active_start_date*  
 La fecha en que puede comenzar la ejecución de un trabajo. *active_start_date*es **int**, su valor predeterminado es NULL, lo que indica la fecha de hoy. La fecha tiene el formato AAAAMMDD. Si *active_start_date* no es NULL, la fecha debe ser mayor o igual a 19900101.  
  
 Una vez creada la programación, revise la fecha de inicio y confirme que es correcta. Para obtener más información, vea la sección "Programar fechas de inicio" en [crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 [ **@active_end_date =** ] *active_end_date*  
 Fecha en la que puede detenerse la ejecución de un trabajo. *active_end_date*es **int**, su valor predeterminado es **99991231**, lo que indica el 31 de diciembre de 9999. Tiene el formato AAAAMMDD.  
  
 [  **@active_start_time =** ] *active_start_time*  
 La hora de un día entre *active_start_date* y *active_end_date* para comenzar la ejecución de un trabajo. *active_start_time*es **int**, su valor predeterminado es 000000, lo que indica 12:00:00 A.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [  **@active_end_time =** ] *active_end_time*  
 La hora de un día entre *active_start_date* y *active_end_date* para finalizar la ejecución de un trabajo. *active_end_time*es **int**, su valor predeterminado es **235959**, lo que indica 11:59:59 P.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [ **@owner_login_name**=] **'***owner_login_name***'**]  
 Nombre de la entidad de seguridad del servidor a la que pertenece la programación. *owner_login_name* es **sysname**, su valor predeterminado es NULL, lo que indica que la programación pertenece al creador.  
  
 [ **@automatic_post =**] *automatic_post*  
 Reservado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 Todos los trabajos que utilizan la programación emplean de inmediato la nueva configuración. No obstante, el cambio de la programación no detiene la ejecución en curso de los trabajos.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo los miembros del **sysadmin** puede modificar una programación que pertenece a otro usuario.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se cambia el estado de habilitación de la programación `NightlyJobs` a `0` y se establece el propietario en `terrid`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Programar un trabajo](../../ssms/agent/schedule-a-job.md)   
 [Crear una programación](../../ssms/agent/create-a-schedule.md)   
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
