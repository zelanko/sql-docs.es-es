---
title: sp_purge_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed89736333db4260fe7defe81160935407ec74af
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43091654"
---
# <a name="sppurgejobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita los registros de historial de un trabajo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_name=** ] **'***job_name***'**  
 Nombre del trabajo del que se van a eliminar registros de historial. *job_name*es **sysname**, su valor predeterminado es null. Cualquier *job_id* o *job_name* debe especificarse, pero no se pueden especificar ambos.  
  
> [!NOTE]  
>  Los miembros de la **sysadmin** rol fijo de servidor o los miembros de la **SQLAgentOperatorRole** rol fijo de base de datos se puede ejecutar **sp_purge_jobhistory** sin especificar un *job_name* o *job_id*. Cuando **sysadmin** a los usuarios no especifican estos argumentos, se elimina el historial de trabajos para todos los trabajos locales y multiservidor en el tiempo especificado por *oldest_date*. Cuando **SQLAgentOperatorRole** a los usuarios no especifican estos argumentos, se elimina el historial de trabajos para todos los trabajos locales en el tiempo especificado por *oldest_date*.  
  
 [ **@job_id=** ] *job_id*  
 Número de identificación del trabajo para los registros que se van a eliminar. *job_id*es **uniqueidentifier**, su valor predeterminado es null. Cualquier *job_id* o *job_name* debe especificarse, pero no se pueden especificar ambos. Consulte la nota en la descripción de **@job_name** para obtener información acerca de cómo **sysadmin** o **SQLAgentOperatorRole** los usuarios pueden usar este argumento.  
  
 [ **@oldest_date** =] *oldest_date*  
 Registro más antiguo que se mantendrá en el historial. *oldest_date* es **datetime**, su valor predeterminado es null. Cuando *oldest_date* se especifica, **sp_purge_jobhistory** solo quita los registros que sean más antiguos que el valor especificado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Notas  
 Cuando **sp_purge_jobhistory** se completa correctamente, se devuelve un mensaje.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, solo los miembros de la **sysadmin** rol fijo de servidor o el **SQLAgentOperatorRole** rol fijo de base de datos puede ejecutar este procedimiento almacenado. Los miembros de **sysadmin** pueden purgar el historial de trabajos para todos los trabajos locales y multiservidor. Los miembros de **SQLAgentOperatorRole** pueden purgar el historial de trabajos para todos los trabajos locales.  
  
 Otros usuarios, incluidos los miembros de **SQLAgentUserRole** y los miembros de **SQLAgentReaderRole**, debe ser concedido explícitamente el permiso EXECUTE en **sp_purge_jobhistory**. Una vez que disponen del permiso EXECUTE en este procedimiento almacenado, estos usuarios solo pueden purgar el historial de los trabajos que les pertenecen.  
  
 El **SQLAgentUserRole**, **SQLAgentReaderRole**, y **SQLAgentOperatorRole** roles fijos de base de datos están en el **msdb** base de datos. Para obtener más información sobre sus permisos, consulte [Roles fijos de base de datos de SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. Quitar el historial de un trabajo determinado  
 En el ejemplo siguiente se quita el historial de un trabajo denominado `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. Quitar el historial de todos los trabajos  
  
> [!NOTE]  
>  Solo los miembros de la **sysadmin** fijo de servidor y los miembros de la **SQLAgentOperatorRole** puede quitar el historial de todos los trabajos. Cuando **sysadmin** los usuarios ejecutan este procedimiento almacenado sin parámetros, se quita el historial de trabajos para todos los trabajos locales y multiservidor. Cuando **SQLAgentOperatorRole** los usuarios ejecutan este procedimiento almacenado sin parámetros, se quita el historial de trabajos para todos los trabajos locales.  
  
 En el ejemplo siguiente se ejecuta el procedimiento sin parámetros para quitar todos los registros de historial.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Permisos de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
