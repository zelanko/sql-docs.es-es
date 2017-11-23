---
title: sp_adddynamicsnapshot_job (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords: sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3b2201611c5b58b795063dd06ecc7c0918c57f4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un trabajo de agente que genera una instantánea de datos filtrados para una publicación con filtros de fila con parámetros. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. Lo utiliza el administrador para crear manualmente trabajos de instantáneas de datos filtrados para los suscriptores.  
  
> [!NOTE]  
>  Para crear un trabajo de instantáneas de datos filtrados, antes debe existir un trabajo de instantáneas estándar para la publicación.  
  
 Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación a la que se agrega el trabajo de instantáneas de datos filtrados. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@suser_sname** =] **'***suser_sname***'**  
 Es el valor utilizado al crear una instantánea de datos filtrados para una suscripción que está filtrada por el valor de la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) función en el suscriptor. *SUSER_SNAME* es **sysname**, no tiene ningún valor predeterminado. *SUSER_SNAME* debe ser NULL si esta función no se utiliza para filtrar dinámicamente la publicación.  
  
 [  **@host_name** =] **'***host_name***'**  
 Es el valor utilizado al crear una instantánea de datos filtrados para una suscripción que está filtrada por el valor de la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función en el suscriptor. *HOST_NAME* es **sysname**, no tiene ningún valor predeterminado. *HOST_NAME* debe ser NULL si esta función no se utiliza para filtrar dinámicamente la publicación.  
  
 [  **@dynamic_snapshot_jobname** =] **'***dynamic_snapshot_jobname***'**  
 Es el nombre del trabajo de instantáneas de datos filtrados creado. *dynamic_snapshot_jobname* es **sysname**, no tiene valor predeterminado es null, y es un parámetro OUTPUT opcional. Si se especifica, *dynamic_snapshot_jobname* debe resolverse en un único trabajo en el distribuidor. Si no se especifica, se generará un nombre de trabajo automáticamente, el cual se devolverá al conjunto de resultados. Allí, el nombre se crea del siguiente modo:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  Al generar el nombre del trabajo de instantáneas dinámicas, es posible truncar el nombre del trabajo de instantáneas estándar.  
  
 [  **@dynamic_snapshot_jobid** =] **'***dynamic_snapshot_jobid***'**  
 Es un identificador para el trabajo de instantáneas de datos filtrados creado. *dynamic_snapshot_jobid* es **uniqueidentifier**, no tiene valor predeterminado es null, y es un parámetro OUTPUT opcional.  
  
 [  **@frequency_type=**] *frequency_type*  
 Es la frecuencia con que se programa el trabajo de instantáneas de datos filtrados. *frequency_type* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4** (valor predeterminado)|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Es el período (medido en días) durante el que se ejecuta el trabajo de instantáneas de datos filtrados. *frequency_interval* es **int**, con un valor predeterminado de 1 y depende del valor de *frequency_type*.  
  
|Valor de *frequency_type*|Efecto en *frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* no se utiliza.|  
|**4** (valor predeterminado)|Cada *frequency_interval* días, con un valor predeterminado de diariamente.|  
|**8**|*frequency_interval* es uno o varios de los siguientes (combinado con un [&#124; &#40; OR bit a bit &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md) operador lógico):<br /><br /> **1** = el domingo &#124; **2** = el lunes &#124; **4** = el martes &#124; **8** = el miércoles &#124; **16** = el jueves &#124; **32** = el viernes &#124; **64** = el sábado|  
|**16**|En el *frequency_interval* día del mes.|  
|**32**|*frequency_interval* es uno de los siguientes:<br /><br /> **1** = el domingo &#124; **2** = el lunes &#124; **3** = el martes &#124; **4** = el miércoles &#124; **5** = el jueves &#124; **6** = el viernes &#124; **7** = el sábado &#124; **8** = día &#124; **9** = día de la semana &#124; **10** = día del fin de semana|  
|**64**|*frequency_interval* no se utiliza.|  
|**128**|*frequency_interval* no se utiliza.|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Especifica las unidades de *frequency_subday_interval*. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4** (valor predeterminado)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es el número de *frequency_subday* períodos que transcurren entre cada ejecución del trabajo. *frequency_subday_interval* es **int**, su valor predeterminado es 5.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Es la repetición del trabajo de instantáneas de datos filtrados en cada mes. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (predeterminado)|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, con un valor predeterminado es 0.  
  
 [  **@active_start_date=**] *active_start_date*  
 Es la fecha en que el trabajo de instantáneas de datos filtrados se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_date=**] *active_end_date*  
 Es la fecha en que el trabajo de instantáneas de datos filtrados deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora en que el trabajo de instantáneas de datos filtrados se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora en que el trabajo de instantáneas de datos filtrados deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica el trabajo de instantáneas de datos filtrados en el [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) tabla del sistema.|  
|**dynamic_snapshot_jobname**|**sysname**|Nombre del trabajo de instantáneas de datos filtrados.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica de forma única el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente en el distribuidor.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adddynamicsnapshot_job** se utiliza en la replicación de mezcla para publicaciones que utilizan un filtro con parámetros.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_adddynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vea también  
 [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
