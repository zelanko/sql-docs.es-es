---
title: syspolicy_policy_categories (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs: TSQL
helpviewer_keywords: syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f75d3b95c0c37fa9acf2a550651f34308d0e782
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syspolicypolicycategories-transact-sql"></a>syspolicy_policy_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra una fila para cada categoría de directiva de administración basada en directivas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Categorías de directivas le ayudarán a organizar las directivas cuando se tienen muchas directivas. En la tabla siguiente se describen las columnas de la vista syspolicy_policy_groups.  
 
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|Identificador de la categoría de directiva.|  
|name|**sysname**|Nombre de la categoría de directiva.|  
|mandate_database_subscriptions|**bit**|Indica si la categoría de directiva se aplica a todas las bases de datos en una instancia sin una suscripción explícita (1) o si se debe aplicar a una base de datos utilizando una suscripción explícita (0).|  
  
## <a name="remarks"></a>Comentarios  
 Muestra una lista de grupos de directivas de administración basada en directivas.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Vistas de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
