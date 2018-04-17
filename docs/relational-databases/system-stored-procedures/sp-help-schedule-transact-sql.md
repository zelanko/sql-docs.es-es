---
title: sp_help_schedule (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c29f9e803884778a4bc4222eec29feb40e867996
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de programaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@schedule_id =** ] *Id.*  
 Identificador de la programación que se va a mostrar. *schedule_name* es **int**, no tiene ningún valor predeterminado. Cualquier *schedule_id* o *schedule_name* se puede especificar.  
  
 [  **@schedule_name =** ] **'***schedule_name***'**  
 Nombre de la programación que se va a mostrar. *schedule_name* es **sysname**, no tiene ningún valor predeterminado. Cualquier *schedule_id* o *schedule_name* se puede especificar.  
  
 [ **@attached_schedules_only** =] *attached_schedules_only* ]  
 Especifica si se muestran únicamente las programaciones a las que está adjunto un trabajo. *attached_schedules_only* es **bits**, su valor predeterminado es **0**. Cuando *attached_schedules_only* es **0**, se muestran todas las programaciones. Cuando *attached_schedules_only* es **1**, el conjunto de resultados contiene únicamente las programaciones que se adjuntan a un trabajo.  
  
 [ **@include_description** =] *include_description*  
 Especifica si se incluyen descripciones en el conjunto de resultados. *include_description* es **bits**, su valor predeterminado es **0**. Cuando *include_description* es **0**, *schedule_description* columna del conjunto de resultados contiene un marcador de posición. Cuando *include_description* es **1**, la descripción de la programación se incluye en el conjunto de resultados.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Este procedimiento devuelve el siguiente conjunto de resultados:  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Número de identificador de la programación.|  
|**schedule_uid**|**uniqueidentifier**|Identificador de la programación.|  
|**schedule_name**|**sysname**|Nombre de la programación.|  
|**enabled**|**int**|Si la programación está habilitada (**1**) o no habilitada (**0**).|  
|**freq_type**|**int**|Valor que indica cuándo el trabajo se va a ejecutar.<br /><br /> **1** = una vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente, relativo a la **freq_interval**<br /><br /> **64** = se ejecuta cuando se inicia el servicio SQLServerAgent.|  
|**freq_interval**|**int**|Días cuando se ejecuta el trabajo. El valor depende del valor de **freq_type**. Para obtener más información, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|Unidades de **freq_subday_interval**. Para obtener más información, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|Número de **freq_subday_type** períodos que transcurren entre cada ejecución del trabajo. Para obtener más información, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|El trabajo programado de la **freq_interval** cada mes. Para obtener más información, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|Número de meses entre las ejecuciones programadas del trabajo.|  
|**active_start_date**|**int**|Fecha en que se activó la programación.|  
|**active_end_date**|**int**|Fecha final de la programación.|  
|**active_start_time**|**int**|Hora del día en que se inicia la programación.|  
|**active_end_time**|**int**|Hora del día en que termina la programación.|  
|**date_created**|**datetime**|Fecha en que se creó la programación.|  
|**schedule_description**|**nvarchar(4000)**|Descripción de la programación en inglés (si se solicita).|  
|**job_count**|**int**|Devuelve cuántos trabajos hacen referencia a esta programación.|  
  
## <a name="remarks"></a>Comentarios  
 Si no se proporcionan parámetros, **sp_help_schedule** muestra información para todas las programaciones de la instancia.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Los miembros de **SQLAgentUserRole** solo se pueden ver las programaciones que les pertenecen.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. Mostrar información de todas las programaciones de la instancia  
 El ejemplo siguiente muestra información de todas las programaciones de la instancia.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. Mostrar información de una programación específica  
 El ejemplo siguiente muestra información de la programación denominada `NightlyJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
