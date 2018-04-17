---
title: sp_delete_maintenance_plan_db (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_delete_maintenance_plan_db_TSQL
- sp_delete_maintenance_plan_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_db
- maintenance plans [SQL Server], deleting
- removing maintenance plan
- disassociating maintenance plan
ms.assetid: d1e8afb5-12ee-492b-a770-ba708ed7c8a4
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01b44b03bd454b352664b596839e54291ade13ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spdeletemaintenanceplandb-transact-sql"></a>sp_delete_maintenance_plan_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina las asociaciones del plan de mantenimiento especificado de la base de datos especificada.  
  
> [!NOTE]  
>  Este procedimiento almacenado se utiliza con planes de mantenimiento de bases de datos. Esta característica se ha reemplazado por planes de mantenimiento que no utilizan este procedimiento almacenado. Utilice este procedimiento para conservar planes de mantenimiento de bases de datos en instalaciones actualizadas de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_maintenance_plan_db [ @plan_id = ] 'plan_id' ,   
     [ @db_name = ] 'database_name'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@plan_id =**] **'***plan_id***'**  
 Especifica el identificador del plan de mantenimiento. *plan_id* es **uniqueidentifier**.  
  
 [  **@db_name =**] **'***database_name***'**  
 Especifica el nombre de la base de datos que se va a eliminar del plan de mantenimiento. *database_name* es **sysname**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_delete_maintenance_plan_db** se debe ejecutar desde la **msdb** base de datos.  
  
 El **sp_delete_maintenance_plan_db** procedimiento almacenado quita la asociación entre el plan de mantenimiento y la base de datos especificado; no quita ni destruye la base de datos.  
  
 Cuando **sp_delete_maintenance_plan_db** quita la última base de datos del plan de mantenimiento, el procedimiento almacenado también elimina el plan de mantenimiento.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_delete_maintenance_plan_db**.  
  
## <a name="examples"></a>Ejemplos  
 Elimina el plan de mantenimiento de la **AdventureWorks2012** base de datos, previamente agregado mediante **sp_add_maintenance_plan_db**.  
  
```  
EXECUTE   sp_delete_maintenance_plan_db N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vea también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Procedimientos almacenados de planes de mantenimiento de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
