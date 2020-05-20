---
title: sp_start_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2eeeae39d23cf611aa57cd2853e911ad7b22c391
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820360"
---
# <a name="sp_start_job-transact-sql"></a>sp_start_job (Transact-SQL)
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
`[ @job_name = ] 'job_name'`Nombre del trabajo que se va a iniciar. Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos. *job_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @job_id = ] job_id`Número de identificación del trabajo que se va a iniciar. Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos. *job_id* es de tipo **uniqueidentifier**y su valor predeterminado es NULL.  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'`El servidor de destino en el que se va a iniciar el trabajo. *SERVER_NAME* es de tipo **nvarchar (128)** y su valor predeterminado es NULL. *SERVER_NAME* debe ser uno de los servidores de destino a los que está dirigido actualmente el trabajo.  
  
`[ @step_name = ] 'step_name'`Nombre del paso en el que se va a iniciar la ejecución del trabajo. Solo se aplica a trabajos locales. *step_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 Este procedimiento almacenado está en la base de datos **msdb** .  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Los miembros de **SQLAgentUserRole** y **SQLAgentReaderRole** solo pueden iniciar trabajos que les pertenezcan. Los miembros de **SQLAgentOperatorRole** pueden iniciar todos los trabajos locales, incluidos los que pertenecen a otros usuarios. Los miembros de **sysadmin** pueden iniciar todos los trabajos locales y multiservidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se inicia un trabajo llamado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_delete_job &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
