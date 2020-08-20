---
description: syspolicy_system_health_state (Transact-SQL)
title: syspolicy_system_health_state (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_system_health_state_TSQL
- syspolicy_system_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_system_health_state view
ms.assetid: 00815106-9fe4-481d-a9e1-a256101887f4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 66a99f117b9c6d8de7a92d328da812869a594f73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493783"
---
# <a name="syspolicy_system_health_state-transact-sql"></a>syspolicy_system_health_state (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Muestra una fila para cada combinación de expresión de consulta de destino y directiva de administración basada en directivas. Utilice la vista syspolicy_system_health_state para comprobar mediante programación el estado de directivas del servidor. En la tabla siguiente se describen las columnas de la vista syspolicy_system_health_state.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|health_state_id|**bigint**|Identificador del registro de estado de la directiva de mantenimiento.|  
|policy_id|**int**|Identificador de la directiva.|  
|last_run_date|**datetime**|Fecha y hora en que la directiva se ejecutó por última vez.|  
|target_query_expression_with_id|**nvarchar(400)**|Expresión de destino, con los valores asignados a las variables de identidad, que define el destino con el que se evalúa la directiva.|  
|target_query_expression|**nvarchar(max)**|Expresión que define el destino con el que se evalúa la directiva.|  
|resultado|**bit**|Estado de mantenimiento de este destino con respecto a la directiva:<br /><br /> 0 = Error<br /><br /> 1 = Correcto|  
  
## <a name="remarks"></a>Observaciones  
 La vista syspolicy_system_health_state muestra el estado más reciente de la expresión de consulta de destino para cada directiva activa (habilitada). El Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y la página Detalles del Explorador de objetos agregan el estado de la directiva de mantenimiento en esta vista para mostrar el estado crítico.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar servidores mediante la administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Vistas de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
