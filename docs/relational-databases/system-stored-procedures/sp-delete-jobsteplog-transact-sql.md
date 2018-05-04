---
title: sp_delete_jobsteplog (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
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
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 99f60818976dc3c89e11d2fd1256a7aecd7d8b63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita todos los registros de paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifican con los argumentos. Utilice este procedimiento almacenado para mantener la **sysjobstepslogs** tabla el **msdb** base de datos.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =**] **'***job_id***'**  
 Número de identificación del trabajo que contiene el registro de paso de trabajo que se va a quitar. *job_id* es **int**, su valor predeterminado es null.  
  
 [  **@job_name =**] **'***job_name***'**  
 Nombre del trabajo. *job_name* es **sysname**, su valor predeterminado es null.  
  
> **Nota:** cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [ **@step_id =**] *step_id*  
 Número de identificación del paso en el trabajo cuyo registro de paso de trabajo se va a eliminar. Si no se incluye, se eliminarán todos los registros de paso de trabajo en el trabajo a menos que **@older_than** o **@larger_than** se especifican. *step_id* es **int**, su valor predeterminado es null.  
  
 [  **@step_name =**] **'***step_name***'**  
 Nombre del paso del trabajo cuyo registro de paso de trabajo se va a eliminar. *Step_name* es **sysname**, su valor predeterminado es null.  
  
> **Nota:** cualquier *step_id* o *step_name* puede especificarse, pero no pueden especificarse ambos.  
  
 [  **@older_than =**] **'***fecha***'**  
 Fecha y hora del registro de paso de trabajo más antiguo que desea conservar. Todos los registros de paso de trabajo con fecha anterior a esta fecha y hora se quitarán. *fecha* es **datetime**, su valor predeterminado es null. Ambos **@older_than** y **@larger_than** se puede especificar.  
  
 [  **@larger_than =**] **'***size_in_bytes***'**  
 Tamaño en bytes del registro de paso de trabajo más grande que desea conservar. Todos los registros de paso de trabajo con un tamaño superior a este se quitan. Ambos **@larger_than** y **@older_than** se puede especificar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_delete_jobsteplog** está en el **msdb** base de datos.  
  
 Si ningún argumento excepto **@job_id** o **@job_name** se especifica, se eliminan todos los registros de paso de trabajo para el trabajo especificado.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Solo los miembros del **sysadmin** puede eliminar un registro de paso de trabajo que pertenece a otro usuario.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. Quitar todos los registros de paso de trabajo de un trabajo  
 En este ejemplo se quitan todos los registros de paso de trabajo correspondientes al trabajo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. Quitar el registro de paso de trabajo de un paso de trabajo determinado  
 En este ejemplo se quita el registro de paso de trabajo correspondiente al paso 2 del trabajo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. Quitar todos los registros de paso de trabajo en función de la antigüedad y el tamaño  
 En este ejemplo se quitan todos los registros de paso de trabajo que son anteriores a las 12 del mediodía del 25 de octubre de 2005, cuyo volumen es superior a 100 megabytes (MB), del trabajo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
