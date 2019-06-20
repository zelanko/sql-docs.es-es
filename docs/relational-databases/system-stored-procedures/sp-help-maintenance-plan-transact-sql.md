---
title: sp_help_maintenance_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f842060c6ca621fc52fa34f08838541dc65e993
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719550"
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información relacionada con el plan de mantenimiento especificado. Si no se especifica un plan, este procedimiento almacenado devuelve información acerca de todos los planes de mantenimiento.  
  
> **NOTA:** Este procedimiento almacenado se utiliza con planes de mantenimiento de bases de datos. Esta característica se ha reemplazado por planes de mantenimiento que no utilizan este procedimiento almacenado. Utilice este procedimiento para conservar planes de mantenimiento de bases de datos en instalaciones actualizadas de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @plan_id = ] 'plan\_id'` Especifica el identificador del plan del plan de mantenimiento. *plan_id* es **UNIQUEIDENTIFIER**. El valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si *plan_id* se especifica, **sp_help_maintenance_plan** devolverá tres tablas: Plan, base de datos y de trabajo.  
  
### <a name="plan-table"></a>Tabla Plan  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Id. del plan de mantenimiento.|  
|**plan_name**|**sysname**|Nombre del plan de mantenimiento.|  
|**date_created**|**datetime**|Fecha de creación del plan de mantenimiento.|  
|**owner**|**sysname**|Propietario del plan de mantenimiento.|  
|**max_history_rows**|**int**|Número máximo de filas asignadas para registrar el historial del plan de mantenimiento de la tabla del sistema.|  
|**remote_history_server**|**int**|El nombre del servidor remoto en el que se puede escribir el informe de historial.|  
|**max_remote_history_rows**|**int**|Número máximo de filas asignadas en la tabla del sistema en un servidor remoto en el que se puede escribir el informe del historial.|  
|**user_defined_1**|**int**|Valor predeterminado es NULL.|  
|**user_defined_2**|**nvarchar(100)**|Valor predeterminado es NULL.|  
|**user_defined_3**|**datetime**|Valor predeterminado es NULL.|  
|**user_defined_4**|**uniqueidentifier**|Valor predeterminado es NULL.|  
  
### <a name="database-table"></a>Tabla Database  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**database_name**|Nombre de todas las bases de datos asociadas con el plan de mantenimiento. *database_name* es **sysname**.|  
  
### <a name="job-table"></a>Tabla Job  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**job_id**|Identificador de todos los trabajos asociados con el plan de mantenimiento. *job_id* es **uniqueidentifier**.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_maintenance_plan** está en el **msdb** base de datos.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_help_maintenance_plan**.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se proporciona información descriptiva acerca del plan de mantenimiento FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Vea también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Procedimientos almacenados de planes de mantenimiento de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
