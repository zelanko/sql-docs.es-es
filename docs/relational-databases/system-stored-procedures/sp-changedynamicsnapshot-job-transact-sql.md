---
title: sp_changedynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b3f2d65811e856bfec95fcd5ffa1749f62c58c3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822479"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica el trabajo de agente que genera la instantánea para una suscripción a una publicación con un filtro de fila con parámetros. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 Es el nombre del trabajo de instantánea que se cambia. *dynamic_snapshot_jobname*es **sysname**, con el valor predeterminado es N '%'. Si *dynamic_snapshot_jobid* se especifica, debe usar el valor predeterminado de *dynamic_snapshot_jobname*.  
  
 [ **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 Es el identificador del trabajo de instantánea que se cambia. *dynamic_snapshot_jobid* es **uniqueidentifier**, su valor predeterminado es NULL. Si *dynamic_snapshot_jobname*se especifica, debe usar el valor predeterminado de *dynamic_snapshot_jobid*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 Es la frecuencia con que se programa el agente. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
|NULL (predeterminado)||  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Los días en que se ejecuta el agente. *frequency_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Lunes|  
|**3**|Martes|  
|**4**|Miércoles|  
|**5**|Jueves|  
|**6**|Viernes|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Días de la semana|  
|**10**|Días del fin de semana|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 Es la frecuencia de repetición de la programación durante el periodo definido. *frequency_subday* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 Es la fecha de ejecución del Agente de mezcla. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
|NULL (predeterminado)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Es la fecha en que el agente de mezcla se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Es la fecha en la que el agente de mezcla deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 Es la hora del día en que el agente de mezcla se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 Es la hora del día en que el agente de mezcla deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@job_login=** ] **'***job_login***'**  
 Es la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el agente de instantáneas al generar la instantánea para una suscripción con un filtro de fila con parámetros. *job_login* es **nvarchar (257)**, su valor predeterminado es null.  
  
 [  **@job_password=** ] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows con la que se ejecuta el agente de instantáneas al generar la instantánea para una suscripción con un filtro de fila con parámetros. *job_password* es **nvarchar (257)**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changedynamicsnapshot_job** se utiliza en la replicación de mezcla para publicaciones con filtros de fila con parámetros.  
  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vea también  
 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  (Ver y modificar la configuración de seguridad de la replicación)  
 [Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
