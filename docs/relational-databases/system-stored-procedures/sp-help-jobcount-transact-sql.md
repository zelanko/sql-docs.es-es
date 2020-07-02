---
title: sp_help_jobcount (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobcount
- sp_help_jobcount_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobcount
ms.assetid: ae8ef851-646c-4889-bc11-c8ec78762572
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6df2b3b8ac52211cc7a558724549870da8ff85e7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730030"
---
# <a name="sp_help_jobcount-transact-sql"></a>sp_help_jobcount (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Proporciona el número de trabajos a los que se ha adjuntado una programación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_jobcount   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @schedule_id = ] schedule_id`Identificador de la programación que se va a mostrar. *schedule_id* es de **tipo int**y no tiene ningún valor predeterminado. Se puede especificar *schedule_id* o *schedule_name* .  
  
`[ @schedule_name = ] 'schedule_name'`Nombre de la programación que se va a mostrar. *schedule_name* es de **tipo sysname**y no tiene ningún valor predeterminado. Se puede especificar *schedule_id* o *schedule_name* .  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve el siguiente conjunto de resultados:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**JobCount**|**int**|Número de trabajos para la programación especificada.|  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento muestra el número de trabajos adjuntos a la programación especificada.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo los miembros de **sysadmin** pueden ver los recuentos de los trabajos que son propiedad de otros usuarios.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra el número de trabajos adjuntos a la programación `NightlyJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobcount  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Agente SQL Server procedimientos almacenados &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
