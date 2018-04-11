---
title: sp_add_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2da9a4bf2bc1fb7e2768922b6b5dd4d93452571
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2018
---
# <a name="spaddjobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una programación para un trabajo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 Número de identificación del trabajo al que se va a agregar la programación. *job_id* es **uniqueidentifier**, no tiene ningún valor predeterminado.  
  
 [  **@job_name=** ] **'***job_name***'**  
 Nombre del trabajo al que se va a agregar la programación. *job_name* es **nvarchar (128)**, no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [ **@name=** ] **'***name***'**  
 Nombre de la programación. *nombre* es **nvarchar (128)**, no tiene ningún valor predeterminado.  
  
 [ **@enabled=** ] *enabled_flag*  
 Indica el estado actual de la programación. *enabled_flag* es **tinyint**, su valor predeterminado es **1** (habilitado). Si **0**, la programación no está habilitada. Si la programación está deshabilitada, el trabajo no se ejecutará.  
  
 [ **@freq_type=** ] *frequency_type*  
 Valor que indica cuándo se va a ejecutar el trabajo. *frequency_type* es **int**, su valor predeterminado es **0**, y puede tener uno de los siguientes valores:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente, relativo a *frequency_interval.*|  
|**64**|Se ejecuta cuando se inicia el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**128**|Se ejecuta cuando el equipo está inactivo.|  
  
 [ **@freq_interval=** ] *frequency_interval*  
 Día en que se ejecuta el trabajo. *frequency_interval* es **int**, con un valor predeterminado es 0 y depende del valor de *frequency_type* como se indica en la tabla siguiente:  
  
|Value|Efecto|  
|-----------|------------|  
|**1** (una vez)|*frequency_interval* no se utiliza.|  
|**4** (diariamente)|Cada *frequency_interval* días.|  
|**8** (semanalmente)|*frequency_interval* es uno o varios de los siguientes (combinados con un operador lógico OR):<br /><br /> 1 = Domingo<br /><br /> 2 = Lunes<br /><br /> 4 = el martes<br /><br /> 8 = el miércoles<br /><br /> 16 = el jueves<br /><br /> 32 = el viernes<br /><br /> 64 = el sábado|  
|**16** (mensualmente)|En el *frequency_interval* día del mes.|  
|**32** (relativo mensual)|*frequency_interval* es uno de los siguientes:<br /><br /> 1 = Domingo<br /><br /> 2 = Lunes<br /><br /> 3 = Martes<br /><br /> 4 = Miércoles<br /><br /> 5 = Jueves<br /><br /> 6 = Viernes<br /><br /> 7 = Sábado<br /><br /> 8 = Día<br /><br /> 9 = Día de la semana<br /><br /> 10 = Día del fin de semana|  
|**64** (cuando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicie el servicio de agente)|*frequency_interval* no se utiliza.|  
|**128**|*frequency_interval* no se utiliza.|  
  
 [ **@freq_subday_type=** ] *frequency_subday_type*  
 Especifica las unidades de *frequency_subday_interval*. *frequency_subday_type* es **int**, no tiene ningún valor predeterminado y puede ser uno de los siguientes valores:  
  
|Value|Descripción (unidad)|  
|-----------|--------------------------|  
|**0x1**|A la hora especificada|  
|**0x4**|Minutos|  
|**0x8**|Horas|  
  
 [ **@freq_subday_interval=** ] *frequency_subday_interval*  
 Número de *frequency_subday_type* períodos que transcurren entre cada ejecución del trabajo. *frequency_subday_interval* es **int**, con un valor predeterminado es 0.  
  
 [ **@freq_relative_interval=** ] *frequency_relative_interval*  
 Define más detalladamente el *frequency_interval* cuando *frequency_type* está establecido en **32** (relativo mensual).  
  
 *frequency_relative_interval* es **int**, no tiene ningún valor predeterminado y puede ser uno de los siguientes valores:  
  
|Value|Descripción (unidad)|  
|-----------|--------------------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 *frequency_relative_interval* indica la repetición del intervalo. Por ejemplo, si *frequency_relative_interval* está establecido en **2**, *frequency_type* está establecido en **32**, y *frequency_ intervalo de* está establecido en **3**, el trabajo programado se produciría el segundo martes de cada mes.  
  
 [ **@freq_recurrence_factor=** ] *frequency_recurrence_factor*  
 Número de semanas o meses entre las ejecuciones programadas del trabajo. *frequency_recurrence_factor* solo se utiliza si *frequency_type* está establecido en **8**, **16**, o **32**. *frequency_recurrence_factor* es **int**, con un valor predeterminado es 0.  
  
 [ **@active_start_date=** ] *active_start_date*  
 Fecha en la que puede comenzar la ejecución del trabajo. *active_start_date* es **int**, no tiene ningún valor predeterminado. La fecha tiene el formato AAAAMMDD. Si *active_start_date* está establecido, la fecha debe ser mayor o igual a 19900101.  
  
 Una vez creada la programación, revise la fecha de inicio y confirme que es correcta. Para obtener más información, vea la sección "Programar fechas de inicio" en [crear y adjuntar programaciones a trabajos](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5).  
  
 [ **@active_end_date=** ] *active_end_date*  
 Fecha en la que puede detenerse la ejecución del trabajo. *active_end_date* es **int**, no tiene ningún valor predeterminado. La fecha tiene el formato AAAAMMDD.  
  
 [ **@active_start_time=** ] *active_start_time*  
 Hora de un día entre *active_start_date* y *active_end_date* para iniciar la ejecución del trabajo. *active_start_time* es **int**, no tiene ningún valor predeterminado. La hora tiene el formato HHMMSS en un reloj de 24 horas.  
  
 [ **@active_end_time=***active_end_time*  
 Hora de un día entre *active_start_date* y *active_end_date* para finalizar la ejecución de trabajo. *active_end_time* es **int**, no tiene ningún valor predeterminado. La hora tiene el formato HHMMSS en un reloj de 24 horas.  
  
 [ **@schedule_id=***schedule_id***OUTPUT**  
 Número de identificación asignado a la programación si se ha creado correctamente. *schedule_id* es una variable de salida de tipo **int**, no tiene ningún valor predeterminado.  
  
 [ **@schedule_uid**= ] *schedule_uid***OUTPUT**  
 Es un identificador único para la programación. *valor schedule_uid* es una variable de tipo **uniqueidentifier**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Ahora, las programaciones de trabajos se pueden administrar independientemente de los trabajos. Para agregar una programación para un trabajo, use **sp_add_schedule** para crear la programación y **sp_attach_schedule** para adjuntar la programación para un trabajo.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
 
 ## <a name="example"></a>Ejemplo
 En el ejemplo siguiente se asigna una programación de trabajo `SaturdayReports` que se ejecutará cada sábado a las 2:00 AM.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>Vea también  
 [Crear y adjuntar programaciones a trabajos](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [Programar un trabajo](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [Crear una programación](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
