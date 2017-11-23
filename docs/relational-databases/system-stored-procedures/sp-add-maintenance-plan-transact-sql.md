---
title: sp_add_maintenance_plan (Transact-SQL) | Documentos de Microsoft
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
- sp_add_maintenance_plan
- sp_add_maintenance_plan_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_maintenance_plan
ms.assetid: 01ab1834-6260-47cb-a1b7-20722217b062
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7868617e22111a843bbe3831adb014b3454f8760
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spaddmaintenanceplan-transact-sql"></a>sp_add_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un plan de mantenimiento y devuelve el Id. del plan.  
  
> [!NOTE]  
>  Este procedimiento almacenado se utiliza con planes de mantenimiento de bases de datos. Esta característica se ha reemplazado por planes de mantenimiento que no utilizan este procedimiento almacenado. Utilice este procedimiento para conservar planes de mantenimiento de bases de datos en instalaciones actualizadas de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_maintenance_plan [ @plan_name = ] 'plan_name' ,   
     @plan_id = 'plan_id' OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@plan_name =**] **'***plan_name***'**  
 Especifica el nombre del plan de mantenimiento que va a agregarse. *plan_name* es **varchar (128)**.  
  
 **@plan_id= '** *plan_id* **'**  
 Especifica el Id. del plan de mantenimiento. *plan_id* es **uniqueidentifier**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_add_maintenance_plan** se debe ejecutar desde la **msdb** la base de datos y crea un plan de mantenimiento nuevo, aunque vacío. Para agregar una o varias bases de datos y asociarlas a un trabajo o trabajos, ejecute **sp_add_maintenance_plan_db** y **sp_add_maintenance_plan_job**.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_add_maintenance_plan**.  
  
## <a name="examples"></a>Ejemplos  
 Cree un plan de mantenimiento denominado Myplan.  
  
```  
DECLARE   @myplan_id UNIQUEIDENTIFIER;  
EXECUTE   sp_add_maintenance_plan N'Myplan',@plan_id=@myplan_id OUTPUT  
PRINT   'The id for the maintenance plan "Myplan" is:'+convert(varchar(256),@myplan_id);  
GO  
```  
  
 Si el plan de mantenimiento se crea correctamente, se devolverá el Id. del plan.  
  
```  
'The id for the maintenance plan "Myplan" is:' FAD6F2AB-3571-11D3-9D4A-00C04FB925FC  
```  
  
## <a name="see-also"></a>Vea también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Plan de mantenimiento de bases de datos almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
