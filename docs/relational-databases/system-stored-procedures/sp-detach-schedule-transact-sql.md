---
title: sp_detach_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 409dec92a6dbfe9c4dd2c8cef1d81b2aa7f21d91
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536373"
---
# <a name="spdetachschedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una asociación entre una programación y un trabajo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 Número de identificación del trabajo cuya programación se va a quitar. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name=** ] **'**_job_name_**'**  
 Nombre del trabajo cuya programación se va a quitar. *job_name* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no se pueden especificar ambos.  
  
 [  **@schedule_id=** ] *schedule_id*  
 Número de identificación de la programación que se va a quitar del trabajo. *schedule_id* es **int**, su valor predeterminado es null.  
  
 [  **@schedule_name=** ] **'**_schedule_name_**'**  
 Nombre de la programación se va a quitar del trabajo. *schedule_name* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *schedule_id* o *schedule_name* debe especificarse, pero no se pueden especificar ambos.  
  
 [  **@delete_unused_schedule=** ] *delete_unused_schedule*  
 Especifica si se van a eliminar las programaciones de trabajo no utilizadas. *delete_unused_schedule* es **bit**, su valor predeterminado es **0**, lo que significa que todas las programaciones se mantendrán, aunque ningún trabajo haga referencia a ellos. Si establece en **1**, las programaciones de trabajo no utilizadas se eliminan si ningún trabajo haga referencia a ellos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que el propietario del trabajo puede adjuntar un trabajo a una programación y separar un trabajo de una programación sin tener que ser asimismo el propietario de la programación. Sin embargo, una programación no se puede eliminar si la separación la dejase sin trabajos, a menos que el autor de la llamada sea el propietario de la programación.  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza una comprobación para determinar si el usuario es propietario de la programación. Solo los miembros de la **sysadmin** rol fijo de servidor puede separar programaciones de trabajos que pertenecen a otro usuario.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita una asociación entre una programación `'NightlyJobs'` y un trabajo `'BackupDatabase'`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
