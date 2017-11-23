---
title: sp_help_maintenance_plan (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
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
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs: TSQL
helpviewer_keywords: sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a48991c0baec6c8466d0ce33bee730d0948c97e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información relacionada con el plan de mantenimiento especificado. Si no se especifica un plan, este procedimiento almacenado devuelve información acerca de todos los planes de mantenimiento.  
  
> **Nota:** este procedimiento almacenado se utiliza con planes de mantenimiento de bases de datos. Esta característica se ha reemplazado por planes de mantenimiento que no utilizan este procedimiento almacenado. Utilice este procedimiento para conservar planes de mantenimiento de bases de datos en instalaciones actualizadas de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@plan_id =**] **'***plan_id***'**  
 Especifica el identificador del plan del plan de mantenimiento. *plan_id* es **UNIQUEIDENTIFIER**. El valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si *plan_id* se especifica, **sp_help_maintenance_plan** devolverá tres tablas: Plan, Database y Job.  
  
### <a name="plan-table"></a>Tabla Plan  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Id. del plan de mantenimiento.|  
|**plan_name**|**sysname**|Nombre del plan de mantenimiento.|  
|**Date_Created**|**datetime**|Fecha de creación del plan de mantenimiento.|  
|**propietario**|**sysname**|Propietario del plan de mantenimiento.|  
|**max_history_rows**|**int**|Número máximo de filas asignadas para registrar el historial del plan de mantenimiento de la tabla del sistema.|  
|**remote_history_server**|**int**|El nombre del servidor remoto en el que se puede escribir el informe de historial.|  
|**max_remote_history_rows**|**int**|Número máximo de filas asignadas en la tabla del sistema en un servidor remoto en el que se puede escribir el informe del historial.|  
|**user_defined_1**|**int**|Valor predeterminado es NULL.|  
|**user_defined_2**|**nvarchar (100)**|Valor predeterminado es NULL.|  
|**user_defined_3**|**datetime**|Valor predeterminado es NULL.|  
|**user_defined_4**|**uniqueidentifier**|Valor predeterminado es NULL.|  
  
### <a name="database-table"></a>Tabla Database  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**database_name**|Nombre de todas las bases de datos asociadas con el plan de mantenimiento. *database_name* es **sysname**.|  
  
### <a name="job-table"></a>Tabla Job  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**job_id**|Identificador de todos los trabajos asociados con el plan de mantenimiento. *job_id* es **uniqueidentifier**.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_maintenance_plan** está en el **msdb** base de datos.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_help_maintenance_plan**.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se proporciona información descriptiva acerca del plan de mantenimiento FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Vea también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Plan de mantenimiento de bases de datos almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
