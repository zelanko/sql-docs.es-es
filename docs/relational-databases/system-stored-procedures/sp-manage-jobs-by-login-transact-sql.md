---
title: sp_manage_jobs_by_login (Transact-SQL) | Documentos de Microsoft
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
- sp_manage_jobs_by_login
- sp_manage_jobs_by_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_manage_jobs_by_login
ms.assetid: 832ec15a-6e92-4eb5-8c4a-af4dba79fbaa
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59f79ac7f0dfa72be2f63d0c3e711969f92ea93d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33251091"
---
# <a name="spmanagejobsbylogin-transact-sql"></a>sp_manage_jobs_by_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina o reasigna trabajos que pertenecen al inicio de sesión especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_manage_jobs_by_login  
     [ @action = ] 'action'  
     [, [@current_owner_login_name = ] 'current_owner_login_name']  
     [, [@new_owner_login_name = ] 'new_owner_login_name']  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@action=** ] **'***acción***'**  
 Acción que se va a realizar para el inicio de sesión especificado. *acción* es **varchar (10)**, no tiene ningún valor predeterminado. Cuando *acción*es **eliminar**, **sp_manage_jobs_by_login** elimina todos los trabajos que pertenecen a *current_owner_login_name*. Cuando *acción* es **REASIGNAR**, todos los trabajos se asignan a *new_owner_login_name*.  
  
 [  **@current_owner_login_name=** ] **'***current_owner_login_name***'**  
 Nombre de inicio de sesión del propietario del trabajo actual. *current_owner_login_name* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@new_owner_login_name=** ] **'***new_owner_login_name***'**  
 Es el nombre de inicio de sesión del nuevo propietario del trabajo. Use este parámetro solo si *acción* es **REASIGNAR**. *new_owner_login_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este procedimiento almacenado, deben concederse a los usuarios la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se reasignan todos los trabajos de `danw` a `françoisa`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_manage_jobs_by_login  
    @action = N'REASSIGN',  
    @current_owner_login_name = N'danw',  
    @new_owner_login_name = N'françoisa' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
