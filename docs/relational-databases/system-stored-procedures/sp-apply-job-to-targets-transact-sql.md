---
title: sp_apply_job_to_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 64da8efb8018748a6fe114d5ee719d71f9940e92
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833576"
---
# <a name="sp_apply_job_to_targets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
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
`[ @job_id = ] job_id`Número de identificación del trabajo que se va a aplicar a los servidores de destino o grupos de servidores de destino especificados. *job_id* es de tipo **uniqueidentifier**y su valor predeterminado es NULL.  
  
`[ @job_name = ] 'job_name'`Nombre del trabajo que se va a aplicar a los servidores de destino o grupos de servidores de destino asociados especificados. *job_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos.  
  
`[ @target_server_groups = ] 'target_server_groups'`Lista separada por comas de los grupos de servidores de destino a los que se va a aplicar el trabajo especificado. *target_server_groups* es de tipo **nvarchar (2048)** y su valor predeterminado es NULL.  
  
`[ @target_servers = ] 'target_servers'`Lista separada por comas de los servidores de destino a los que se va a aplicar el trabajo especificado. *target_servers*es de tipo **nvarchar (2048)** y su valor predeterminado es NULL.  
  
`[ @operation = ] 'operation'`Indica si se debe aplicar o quitar el trabajo especificado en los servidores de destino o grupos de servidores de destino especificados. la *operación*es **VARCHAR (7)** y su valor predeterminado es Apply. Las operaciones válidas son **Apply** y **Remove**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_apply_job_to_targets** proporciona una manera sencilla de aplicar (o quitar) un trabajo de varios servidores de destino y es una alternativa a llamar a **sp_add_jobserver** (o **sp_delete_jobserver**) una vez por cada servidor de destino necesario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [sp_add_jobserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
