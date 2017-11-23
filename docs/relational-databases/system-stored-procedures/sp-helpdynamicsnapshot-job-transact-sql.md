---
title: sp_helpdynamicsnapshot_job (Transact-SQL) | Documentos de Microsoft
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
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords: sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f9accc8ae7ffb64d82fa10c3b60a2f8fec44b8a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre trabajos del agente que generan instantáneas de datos filtrados. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es  **%** , que devuelve información acerca de todos los trabajos de instantáneas de datos filtrados que coinciden con la cadena *dynamic_ snapshot_jobid*y *dynamic_snapshot_jobname*para todas las publicaciones.  
  
 [  **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 Es el nombre de un trabajo de instantáneas de datos filtrados. *dynamic_snapshot_jobname*es **sysname**, no tiene valor predeterminado de  **%** ', que devuelve todos los trabajos dinámicos para una publicación con los valores especificados *dynamic_ snapshot_jobid*. Si no se especificó un nombre de trabajo explícitamente cuando se creó el trabajo, el formato del nombre del trabajo es el siguiente:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [  **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 Es un identificador para un trabajo de instantáneas de datos filtrados. *dynamic_snapshot_jobid*es **uniqueidentifier**, su valor predeterminado es NULL, que devuelve todos los trabajos de instantáneas que coinciden con la cadena *dynamic_snapshot_jobname*.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica el trabajo de instantáneas de datos filtrados.|  
|**job_name**|**sysname**|Nombre del trabajo de instantáneas de datos filtrados.|  
|**job_id**|**uniqueidentifier**|Identifica la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente en el distribuidor.|  
|**dynamic_filter_login**|**sysname**|Valor utilizado para evaluar la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) función en un filtro de fila con parámetros definido para la publicación.|  
|**dynamic_filter_hostname**|**sysname**|Valor utilizado para evaluar la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función en un filtro de fila con parámetros definido para la publicación.|  
|**ubicacióndeinstantáneadinámica**|**nvarchar(255)**|Ruta a la carpeta de la que se leen los archivos de instantáneas si se utiliza un filtro de fila con parámetros.|  
|**frequency_type**|**int**|Se trata de la frecuencia de ejecución programada del agente, que puede ser uno de estos valores.<br /><br /> **1** = una vez<br /><br /> **2** = a petición<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente relativa<br /><br /> **64** = inicio automático<br /><br /> **128** = periódica|  
|**frequency_interval**|**int**|Los días en los que se ejecuta el agente; puede tener los valores siguientes.<br /><br /> **1** = el domingo<br /><br /> **2** = el lunes<br /><br /> **3** = el martes<br /><br /> **4** = el miércoles<br /><br /> **5** = el jueves<br /><br /> **6** = el viernes<br /><br /> **7** = el sábado<br /><br /> **8** = día<br /><br /> **9** = días laborables<br /><br /> **10** = días del fin de semana|  
|**frequency_subday_type**|**int**|Es el tipo que define la frecuencia con que el agente ejecuta cuando *frequency_type* es **4** (diariamente), y puede tener uno de estos valores.<br /><br /> **1** = a la hora especificada<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**int**|Número de intervalos de *frequency_subday_type* que se producen entre las ejecuciones programadas del agente.|  
|**frequency_relative_interval**|**int**|Es la semana en que el agente se ejecuta en un mes determinado cuando *frequency_type* es **32** (relativo mensual), y puede tener uno de estos valores.<br /><br /> **1** = primero<br /><br /> **2** = segundo<br /><br /> **4** = tercero<br /><br /> **8** = cuarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor**|**int**|Número de semanas o meses entre las ejecuciones programadas del agente.|  
|**active_start_date**|**int**|Fecha en que se programa la primera ejecución del agente, con el formato AAAAMMDD.|  
|**active_end_date**|**int**|Fecha en que se programa la última ejecución del agente, con el formato AAAAMMDD.|  
|**active_start_time**|**int**|Hora en que se programa la primera ejecución del agente, con el formato HHMMSS.|  
|**active_end_time**|**int**|Hora en que se programa la última ejecución del agente, con el formato HHMMSS.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdynamicsnapshot_job** se utiliza en la replicación de mezcla.  
  
 Si se utilizan todos los valores de parámetros predeterminados, se devuelve información sobre todos los trabajos de instantáneas de datos con particiones para toda la base de datos de publicaciones.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** corregidos rol de base de datos y la lista de acceso de publicación para la publicación pueden ejecutar **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
