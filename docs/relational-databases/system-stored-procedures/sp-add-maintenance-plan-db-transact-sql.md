---
title: sp_add_maintenance_plan_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_maintenance_plan_db_TSQL
- sp_add_maintenance_plan_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_maintenance_plan_db
ms.assetid: 76f4fefa-5b99-4deb-beed-e198987a45a9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8a3af8712870400d979a131dd26c4f6891b1b16a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646637"
---
# <a name="sp_add_maintenance_plan_db-transact-sql"></a>sp_add_maintenance_plan_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Asocia un plan de mantenimiento a una base de datos.  
  
> [!NOTE]  
>  Este procedimiento almacenado se utiliza con planes de mantenimiento de bases de datos. Esta característica se ha reemplazado por planes de mantenimiento que no utilizan este procedimiento almacenado. Utilice este procedimiento para conservar planes de mantenimiento de bases de datos en instalaciones actualizadas de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_maintenance_plan_db [ @plan_id = ] 'plan_id' ,   
     [ @db_name = ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @plan_id = ] 'plan_id'`Especifica el identificador del plan de mantenimiento. *plan_id* es de tipo **uniqueidentifier**y debe ser un ID. válido.  
  
`[ @db_name = ] 'database_name'`Especifica el nombre de la base de datos que se va a agregar al plan de mantenimiento. La base de datos deberá crearse o bien existir antes de su adición al plan. *database_name* es **sysname**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_add_maintenance_plan_db** se debe ejecutar desde la base de datos **msdb** .  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_add_maintenance_plan_db**.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se agrega la base de datos **AdventureWorks2012** al plan de mantenimiento creado en **sp_add_maintenance_plan**.  
  
```  
EXECUTE   sp_add_maintenance_plan_db N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC',N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Consulte también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Procedimientos almacenados del plan de mantenimiento de bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
