---
title: sp_attach_schedule (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs: TSQL
helpviewer_keywords: sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4768c463ceab85f34fb82ba7a0a6d3727f3ac787
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spattachschedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura una programación para un trabajo.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id=** ] *job_id*  
 El número de identificación del trabajo del trabajo al que se agrega la programación. *job_id*es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name =** ] **'***job_name***'**  
 El nombre del trabajo al que se agrega la programación. *job_name*es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@schedule_id =** ] *schedule_id*  
 Número de identificación de la programación que se va a configurar para el trabajo. *schedule_id*es **int**, su valor predeterminado es null.  
  
 [  **@schedule_name =** ] **'***schedule_name***'**  
 Nombre de la programación que se va a configurar para el trabajo. *schedule_name*es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *schedule_id* o *schedule_name* debe especificarse, pero no pueden especificarse ambos.  
  
## <a name="remarks"></a>Comentarios  
 La programación y el trabajo deben tener el mismo propietario.  
  
 Se puede configurar una programación para más de un trabajo. Se puede ejecutar un trabajo en más de una programación.  
  
 Este procedimiento almacenado se debe ejecutar desde la **msdb** base de datos.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que el propietario del trabajo puede adjuntar un trabajo a una programación y separar un trabajo de una programación sin tener que ser asimismo el propietario de la programación. Sin embargo, una programación no se puede eliminar si la separación la dejase sin trabajos, a menos que el llamador sea propietario de la programación.  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comprueba si el usuario es propietario del trabajo y la programación.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una programación llamada `NightlyJobs`. Los trabajos que usan esta programación se ejecutan a diario cuando la hora del servidor es `01:00`. En el ejemplo se asocia la programación a los trabajos `BackupDatabase` y `RunReports`.  
  
> [!NOTE]  
>  En este ejemplo se da por supuesto que el trabajo `BackupDatabase` y el trabajo `RunReports` ya existen.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_detach_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
