---
title: syspolicy_policies (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_policies_TSQL
- syspolicy_policies
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policies view
ms.assetid: aecf35bb-187e-4f80-870f-48081b88974e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 620a626b78521b23c015389ca635a95ebfe0cf33
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="syspolicypolicies-transact-sql"></a>syspolicy_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra una fila para cada directiva de administración basada en directivas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. syspolicy_policies que pertenece al esquema dbo en la base de datos msdb. En la tabla siguiente se describen las columnas de la vista syspolicy_policies.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|policy_id|**int**|Identificador de la directiva.|  
|name|**sysname**|Nombre de la directiva.|  
|condition_id|**int**|Identificador de la condición exigida o probada por esta directiva.|  
|root_condition_id|**int**|Exclusivamente para uso interno.|  
|date_created|**datetime**|Fecha y hora cuando se creó la directiva.|  
|execution_mode|**int**|Modo de evaluación para la directiva. Los valores posibles son los siguientes:<br /><br /> 0 = A petición<br /><br /> Este modo evalúa la directiva cuando lo especifica el usuario directamente.<br /><br /> 1 = Al cambiar: impedir<br /><br /> Este modo automatizado utiliza desencadenadores DDL para evitar infracciones de las directivas.<br /><br /> 2 = Al cambiar: solo registrar<br /><br /> Este modo automatizado utiliza la notificación de eventos para evaluar una directiva cuando se produce un cambio relevante y registra las infracciones de la directiva.<br /><br /> 4 = Al programar<br /><br /> Este modo automatizado utiliza un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para evaluar una directiva periódicamente. El modo registra las infracciones de la directiva.<br /><br /> Nota: El valor 3 no es un valor posible.|  
|policy_category|**int**|Identificador de la categoría de directivas de administración basada en directivas al que esta directiva pertenece. Es NULL si es el grupo de directivas predeterminado.|  
|schedule_uid|**uniqueidentifier**|Cuando execution_mode es Al programar, contiene el identificador de la programación; de lo contrario, es NULL.|  
|description|**nvarchar(max)**|Descripción de la directiva. La columna de descripción es opcional y puede ser NULL.|  
|help_text|**nvarchar(4000)**|Texto del hipervínculo que pertenece a help_link.|  
|help_link|**nvarchar(2083)**|Hipervínculo de ayuda adicional que el creador de la directiva asigna a la misma.|  
|object_set_id|**int**|Identificador del conjunto de objetos que la directiva evalúa.|  
|is_enabled|**bit**|Indica si la directiva está habilitada (1) o deshabilitada (0) actualmente.|  
|job_id|**uniqueidentifier**|Cuando execution_mode es Al programar, contiene el identificador del trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecuta la directiva.|  
|created_by|**sysname**|Inicio de sesión que creó la directiva.|  
|modified_by|**sysname**|Inicio de sesión que modificó la directiva por última vez. Es NULL si nunca se produjo una modificación.|  
|date_modified|**datetime**|Fecha y hora cuando se creó la directiva. Es NULL si nunca se produjo una modificación.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando está solucionando problemas de administración basada en directivas, consulte la [syspolicy_conditions](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md) vista para determinar si la directiva está habilitada. Esta vista también muestra quién creó la directiva o la cambió en último lugar.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Vistas de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
