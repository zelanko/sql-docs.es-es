---
title: sp_delete_job (Transact-SQL) | Documentos de Microsoft
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
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 90d213daa9d5a17a6630142e06e5b7ef441a9e9c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262918"
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un trabajo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 Es el número de identificación del trabajo que se va a eliminar. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name=** ] **'***job_name***'**  
 Es el nombre del trabajo que se va a eliminar. *job_name* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name*debe especificarse; no se pueden especificar ambos.  
  
 [  **@originating_server=** ] **'***server***'**  
 Para uso interno.  
  
 [  **@delete_history=** ] *delete_history*  
 Especifica si se debe eliminar el historial del trabajo. *delete_history* es **bits**, su valor predeterminado es **1**. Cuando *delete_history* es **1**, se elimina el historial de trabajos para el trabajo. Cuando *delete_history* es **0**, no se elimina el historial de trabajos.  
  
 Tenga en cuenta que cuando se elimina un trabajo y no se elimina el historial, la información histórica para el trabajo no se mostrará en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] historial de trabajos de interfaz gráfica de usuario de agente, pero la información continúa estando en la **sysjobhistory**tabla el **msdb** base de datos.  
  
 [  **@delete_unused_schedule=** ] *delete_unused_schedule*  
 Especifica si se deben eliminar las programaciones adjuntas a este trabajo si no están adjuntas a ningún otro trabajo. *delete_unused_schedule* es **bits**, su valor predeterminado es **1**. Cuando *delete_unused_schedule* es **1**, las programaciones adjuntas a este trabajo se eliminan si no hay otros trabajos hacen referencia a la programación. Cuando *delete_unused_schedule* es **0**, no se eliminan las programaciones.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 El **@originating_server** argumento está reservado para uso interno.  
  
 El **@delete_unused_schedule** argumento proporciona compatibilidad con versiones anteriores de SQL Server quitando automáticamente las programaciones que no están adjuntas a ningún trabajo. Tenga en cuenta que este parámetro tiene como valor predeterminado el comportamiento compatible con versiones anteriores. Para mantener las programaciones que no están conectadas a un trabajo, debe proporcionar el valor **0** como el **@delete_unused_schedule** argumento.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un método gráfico sencillo para administrar trabajos y es el método recomendado para crear y administrar la infraestructura de trabajo.  
  
 Este procedimiento almacenado no puede eliminar planes de mantenimiento y tampoco puede eliminar trabajos que forman parte de planes de mantenimiento. En su lugar, utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para eliminar planes de mantenimiento.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_delete_job** para eliminar cualquier trabajo. Un usuario que no sea miembro del rol fijo de servidor **sysadmin** solo puede eliminar los trabajos de los que sea propietario.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina el trabajo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
