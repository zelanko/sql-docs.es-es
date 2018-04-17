---
title: sp_apply_job_to_targets (Transact-SQL) | Documentos de Microsoft
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
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a9b3cca205dc3af412ae9c0dfd426b18c05a4fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spapplyjobtotargets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aplica un trabajo a uno o más servidores de destino, o a los servidores de destino que pertenecen a uno o más grupos de servidores de destino.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id =**] *job_id*  
 Número de identificación del trabajo que se va a aplicar a los servidores o grupos de servidores de destino especificados. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name =**] **'***job_name***'**  
 Nombre del trabajo que se va a aplicar a los servidores de destino o grupos de servidores de destino asociados especificados. *job_name* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@target_server_groups =**] **'***target_server_groups***'**  
 Lista separada por comas que contiene los grupos de servidores de destino a los que se va a aplicar el trabajo especificado. *target_server_groups* es **nvarchar (2048)**, su valor predeterminado es null.  
  
 [  **@target_servers=** ] **'***target_servers***'**  
 Lista separada por comas que contiene los servidores de destino a los que se va a aplicar el trabajo especificado. *target_servers*es **nvarchar (2048)**, su valor predeterminado es null.  
  
 [  **@operation=** ] **'***operación***'**  
 Indica si se debe aplicar o quitar el trabajo especificado en los servidores de destino o grupos de servidores de destino especificados. *operación*es **varchar(7)**, con un valor predeterminado es APPLY. Las operaciones válidas son **aplicar** y **quitar**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_apply_job_to_targets** proporciona una manera sencilla para aplicar (o quitar) un trabajo de varios servidores de destino y es una alternativa a llamar a **sp_add_jobserver** (o **sp_delete_jobserver**) una vez para cada servidor de destino requerido.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se aplica el trabajo `Backup Customer Information`, creado anteriormente, a todos los servidores de destino del grupo `Servers Maintaining Customer Information`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
