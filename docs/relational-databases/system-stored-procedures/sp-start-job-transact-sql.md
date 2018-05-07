---
title: sp_start_job (Transact-SQL) | Documentos de Microsoft
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
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58fb415b74bf26880c1000e1f3122b5f6b86f2e4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spstartjob-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica al Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecute un trabajo inmediatamente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_name=** ] **'***job_name***'**  
 Nombre del trabajo que se va a iniciar. Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos. *job_name* es **sysname**, su valor predeterminado es null.  
  
 [ **@job_id=** ] *job_id*  
 Número de identificación del trabajo que se va a iniciar. Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@error_flag=** ] *error_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@server_name=** ] **'***nombre_servidor***'**  
 Servidor de destino en el que se va a iniciar el trabajo. *nombre_servidor* es **nvarchar (128)**, su valor predeterminado es null. *nombre_servidor* debe ser uno de los servidores de destino a la que el trabajo está destinado actualmente.  
  
 [  **@step_name=** ] **'***step_name***'**  
 Nombre del paso en el que se iniciará la ejecución del trabajo. Solo se aplica a trabajos locales. *Step_name* es **sysname**, su valor predeterminado es null  
  
 [  **@output_flag=** ] *output_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento almacenado se encuentra en la **msdb** base de datos.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Los miembros de **SQLAgentUserRole** y **SQLAgentReaderRole** sólo se puede iniciar trabajos que les pertenecen. Los miembros de **SQLAgentOperatorRole** puede iniciar todos los trabajos locales, incluidos los que pertenecen a otros usuarios. Los miembros de **sysadmin** pueden iniciar todos los trabajos locales y multiservidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se inicia un trabajo llamado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
