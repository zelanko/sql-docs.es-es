---
title: sp_stop_job (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/01/2016
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
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b90ea52e3a64f245633b19f23382b9a147fd1639
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica al Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que detenga la ejecución de un trabajo.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_name =**] **'***job_name***'**  
 Nombre del trabajo que se va a detener. *job_name* es **sysname**, su valor predeterminado es null.  
  
 [ **@job_id =**] *job_id*  
 Número de identificación del trabajo que se va a detener. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@originating_server =**] **'***master_server***'**  
 Nombre del servidor principal. Si se especifica, se detienen todos los trabajos multiservidor. *master_server* es **nvarchar (128)**, su valor predeterminado es null. Especifique este parámetro únicamente cuando se llama **sp_stop_job** en un servidor de destino.  
  
> [!NOTE]  
>  Solo se puede especificar uno de los tres primeros parámetros.  
  
 [  **@server_name =**] **'***target_server***'**  
 Nombre del servidor de destino específico en que se va a detener un trabajo multiservidor. *target_server* es **nvarchar (128)**, su valor predeterminado es null. Especifique este parámetro únicamente cuando se llama **sp_stop_job** en un servidor maestro para un trabajo multiservidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_stop_job** envía una señal de detención para la base de datos. Algunos procesos se pueden detener inmediatamente y algunos deben llegar a un punto estable (o punto de entrada a la ruta de acceso del código) antes de que puede detener. Algunas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] de ejecución prolongada, como BACKUP, RESTORE y algunos comandos DBCC, pueden tardar mucho tiempo en finalizar. Cuando se ejecutan, puede tardar unos instantes antes de que se cancele el trabajo. Si se detiene un trabajo, se registrará una entrada de trabajo cancelado en el historial de trabajos.  
  
 Si un trabajo está ejecutando un paso de tipo **CmdExec** o **PowerShell**, el proceso que se va a ejecutar (por ejemplo, MyProgram.exe) se ve obligado a finalización prematura del objeto. La finalización prematura puede provocar un comportamiento imprevisible como, por ejemplo, que los archivos que el proceso utiliza se mantengan abiertos. Por lo tanto, **sp_stop_job** debe usarse solo en situaciones extremas si el trabajo contiene pasos de tipo **CmdExec** o **PowerShell**.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Los miembros de **SQLAgentUserRole** y **SQLAgentReaderRole** sólo se puede detener trabajos que les pertenecen. Los miembros de **SQLAgentOperatorRole** puede detener todos los trabajos locales, incluidos los que pertenecen a otros usuarios. Los miembros de **sysadmin** pueden detener todos los trabajos locales y multiservidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se detiene un trabajo denominado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
