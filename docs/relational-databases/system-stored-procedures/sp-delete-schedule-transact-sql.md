---
title: sp_delete_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6ec2fe4ba5ad90d044a9407be04acc850ae16b73
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591499"
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina una programación.  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@schedule_id=** ] *schedule_id*  
 Número de identificación de la programación que se va a eliminar. *schedule_id* es **int**, su valor predeterminado es null.  
  
> **NOTA:** Cualquier *schedule_id* o *schedule_name* debe especificarse, pero no se pueden especificar ambos.  
  
 [  **@schedule_name=** ] **'**_schedule_name_**'**  
 Nombre de la programación que se va a eliminar. *schedule_name* es **sysname**, su valor predeterminado es null.  
  
> **NOTA:** Cualquier *schedule_id* o *schedule_name* debe especificarse, pero no se pueden especificar ambos.  
  
 [ **@force_delete** =] *force_delete*  
 Especifica si el procedimiento debe generar un error si la programación está adjunta a un trabajo. *Force_delete* es de tipo bit, su valor predeterminado es **0**. Cuando *force_delete* es **0**, el procedimiento almacenado produce un error si la programación está adjunta a un trabajo. Cuando *force_delete* es **1**, se eliminó el programa independientemente de si la programación está adjunta a un trabajo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 De manera predeterminada, una programación no se puede eliminar si está adjunta a un trabajo. Para eliminar una programación que se adjunta a un trabajo, especifique un valor de **1** para *force_delete*. La eliminación de una programación no detiene los trabajos actualmente en ejecución.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Observe que el propietario del trabajo puede adjuntar un trabajo a una programación y separar un trabajo de una programación sin tener que ser asimismo el propietario de la programación. Sin embargo, una programación no se puede eliminar si la separación la dejase sin trabajos, a menos que el llamador sea propietario de la programación.  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo los miembros de la **sysadmin** pueden eliminar una programación de trabajo que pertenece a otro usuario.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-deleting-a-schedule"></a>A. Eliminar una programación  
 En el ejemplo siguiente se elimina la programación `NightlyJobs`. Si la programación está adjunta a algún trabajo, en el ejemplo no se elimina la programación.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>b. Eliminar una programación adjunta a un trabajo  
 En el ejemplo siguiente se elimina la programación `RunOnce`, independientemente de si está adjunta a un trabajo.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Implementar trabajos](../../ssms/agent/implement-jobs.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
