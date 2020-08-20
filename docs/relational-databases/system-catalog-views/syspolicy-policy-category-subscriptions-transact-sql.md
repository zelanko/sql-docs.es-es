---
description: syspolicy_policy_category_subscriptions (Transact-SQL)
title: syspolicy_policy_category_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 99f95e323b88f6932a1f3af0ed3cf72d9bed964c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460521"
---
# <a name="syspolicy_policy_category_subscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Muestra una fila para cada suscripción de administración basada en directivas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada fila describe un par de destino y categoría de directiva. En la tabla siguiente se describen las columnas de la vista syspolicy_policy_groups_subscriptions.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|Identificador de este registro.|  
|target_type|**sysname**|Tipo de objeto de base de datos que es el destino de esta suscripción.|  
|target_object|**sysname**|Nombre del objeto de destino.|  
|policy_category_id|**int**|Identificador de la categoría de directiva que se aplica al destino.|  
  
## <a name="remarks"></a>Observaciones  
 Esta vista muestra los destinos que se suscriben a categorías de directiva.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar servidores mediante la administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Vistas de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
