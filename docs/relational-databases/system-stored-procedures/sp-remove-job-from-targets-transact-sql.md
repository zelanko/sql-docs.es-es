---
title: sp_remove_job_from_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 033a2c950ec695a64aced30a383d25206e7f6d10
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751687"
---
# <a name="sp_remove_job_from_targets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
`[ @job_id = ] job_id`Número de identificación del trabajo del que se van a quitar los servidores de destino o grupos de servidores de destino especificados. Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos. *job_id* es de tipo **uniqueidentifier**y su valor predeterminado es NULL.  
  
`[ @job_name = ] 'job_name'`Nombre del trabajo del que se van a quitar los servidores de destino o grupos de servidores de destino especificados. Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos. *job_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @target_server_groups = ] 'target_server_groups'`Lista separada por comas de los grupos de servidores de destino que se van a quitar del trabajo especificado. *target_server_groups* es de tipo **nvarchar (1024)** y su valor predeterminado es NULL.  
  
`[ @target_servers = ] 'target_servers'`Lista separada por comas de los servidores de destino que se van a quitar del trabajo especificado. *target_servers* es de tipo **nvarchar (1024)** y su valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="permissions"></a>Permisos  
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
  
## <a name="see-also"></a>Consulte también  
 [sp_apply_job_to_targets &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
