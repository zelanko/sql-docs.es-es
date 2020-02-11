---
title: sp_delete_jobserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobserver
- sp_delete_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobserver
ms.assetid: 6d63ed32-68cf-4d8f-aa40-05a3826e05b8
author: stevestein
ms.author: sstein
ms.openlocfilehash: a2f4b2e8dbcf8e8427f51388c7bead75263d95a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130642"
---
# <a name="sp_delete_jobserver-transact-sql"></a>sp_delete_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita el servidor de destino especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_jobserver { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`Número de identificación del trabajo del que se va a quitar el servidor de destino especificado. *job_id* es de tipo **uniqueidentifier**y su valor predeterminado es NULL.  
  
`[ @job_name = ] 'job_name'`Nombre del trabajo del que se va a quitar el servidor de destino especificado. *job_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  Se debe especificar *job_id* o *job_name* ; no se pueden especificar ambos.  
  
`[ @server_name = ] 'server'`Nombre del servidor de destino que se va a quitar del trabajo especificado. el *servidor* es de tipo **nvarchar (30)** y no tiene ningún valor predeterminado. el *servidor* puede ser **(local)** o el nombre de un servidor de destino remoto.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, los usuarios deben ser miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita `SEATTLE2` el servidor del `Weekly Sales Backups`procesamiento del trabajo.  
  
> [!NOTE]  
>  En este ejemplo se da por supuesto que el trabajo `Weekly Sales Backups` se creó con anterioridad.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_jobserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_help_jobserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
