---
title: sp_remove_job_from_targets (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs: TSQL
helpviewer_keywords: sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8748e6968197faeb3809cf8adef59bc9b2452d57
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spremovejobfromtargets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita el trabajo especificado de los servidores de destino o de los grupos de servidores de destino dados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id =**] *job_id*  
 Número de identificación del trabajo que se va a quitar de los servidores o grupos de servidores de destino especificados. Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name =**] **'***job_name***'**  
 Nombre del trabajo que se va a quitar de los servidores o grupos de servidores de destino especificados. Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos. *job_name* es **sysname**, su valor predeterminado es null.  
  
 [  **@target_server_groups =**] **'***target_server_groups***'**  
 Lista separada por comas que contiene los grupos de servidores de destino que se van a quitar del trabajo especificado. *target_server_groups* es **nvarchar (1024)**, su valor predeterminado es null.  
  
 [  **@target_servers =**] **'***target_servers***'**  
 Lista separada por comas que contiene los servidores de destino que se van a quitar del trabajo especificado. *target_servers* es **nvarchar (1024)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="permissions"></a>Permissions  
 Los permisos de ejecución para este procedimiento corresponden de forma predeterminada a los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el trabajo `Weekly Sales Backups`, creado previamente, del grupo de servidores de destino `Servers Processing Customer Orders` y de los servidores `SEATTLE1` y `SEATTLE2`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_remove_job_from_targets  
    @job_name = N'Weekly Sales Backups',  
    @target_server_groups = N'Servers Processing Customer Orders',   
    @target_servers = N'SEATTLE2,SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_apply_job_to_targets &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
