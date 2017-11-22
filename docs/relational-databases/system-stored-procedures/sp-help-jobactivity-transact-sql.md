---
title: sp_help_jobactivity (Transact-SQL) | Documentos de Microsoft
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
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs: TSQL
helpviewer_keywords: sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cb0d3d344b97f0ce14e3bd156b5915a1721c8f4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpjobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca del estado en tiempo de ejecución de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =**] *job_id*  
 El número de identificación del trabajo. *job_id*es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name =**] **'***job_name***'**  
 Nombre del trabajo. *job_name*es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@session_id**  =] *session_id*  
 Identificador de sesión sobre el que se proporcionará información. *session_id* es **int**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve el siguiente conjunto de resultados:  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Número de identificación de la sesión del Agente.|  
|**job_id**|**uniqueidentifier**|Identificador del trabajo.|  
|**job_name**|**sysname**|Nombre del trabajo.|  
|**run_requested_date**|**datetime**|Fecha para la que se solicitó la ejecución del trabajo.|  
|**run_requested_source**|**sysname**|Origen de la solicitud de ejecución del trabajo. Una de las siguientes opciones:<br /><br /> **1** = ejecutar según una programación<br /><br /> **2** = ejecutar en respuesta a una alerta<br /><br /> **3** = ejecutar al inicio<br /><br /> **4** = ejecutar por usuario<br /><br /> **6** = ejecutar según la programación de CPU inactiva|  
|**queued_date**|**datetime**|Fecha en la que la solicitud se puso en cola. NULL si el trabajo se ejecutó directamente.|  
|**start_execution_date**|**datetime**|Fecha en la que el trabajo se asignó a un subproceso ejecutable.|  
|**last_executed_step_id**|**int**|Identificado de paso del paso de trabajo ejecutado más recientemente.|  
|**last_exectued_step_date**|**datetime**|Momento en que comenzó a ejecutarse el paso de trabajo ejecutado más recientemente.|  
|**stop_execution_date**|**datetime**|Momento en el que el trabajo dejó de ejecutarse.|  
|**next_scheduled_run_date**|**datetime**|Cuando el trabajo se ha programado la próxima a ejecutar.|  
|**job_history_id**|**int**|Identificador del historial de trabajos en la tabla del historial de trabajos.|  
|**Mensaje**|**nvarchar (1024)**|Mensaje generado durante la última ejecución del trabajo.|  
|**run_status**|**int**|Estado devuelto en la última ejecución del trabajo:<br /><br /> **0** = error de error<br /><br /> **1** = se ha realizado correctamente<br /><br /> **3** = cancelado<br /><br /> **5** = estado desconocido|  
|**operator_id_emailed**|**int**|Número de Id. del operador notificado a través de correo electrónico al término del trabajo.|  
|**operator_id_netsent**|**int**|Número de identificación del operador notificado a través de **mediante net send** al término del trabajo.|  
|**operator_id_paged**|**int**|Número de Id. del operador notificado a través de buscapersonas al término del trabajo.|  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento proporciona una instantánea del estado actual de los trabajos. Los resultados devueltos representan la información disponible en el momento de procesar la solicitud.  
  
 El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un Id. de sesión cada vez que se inicia el servicio del Agente. El identificador de sesión se almacena en la tabla **msdb.dbo.syssessions**.  
  
 Si no *session_id* se proporciona, se muestra información acerca de la sesión más reciente.  
  
 Si no *job_name* o *job_id* se proporciona, se muestra información de todos los trabajos.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Solo los miembros del **sysadmin** puede ver la actividad de trabajos que pertenecen a otros usuarios.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra la actividad para todos los trabajos que el usuario actual está autorizado a ver.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Agente SQL Server almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
