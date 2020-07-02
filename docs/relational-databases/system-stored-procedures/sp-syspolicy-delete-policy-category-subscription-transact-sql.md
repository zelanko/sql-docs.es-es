---
title: sp_syspolicy_delete_policy_category_subscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_delete_policy_category_subscription_TSQL
- sp_syspolicy_delete_policy_category_subscription
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_category_subscription
ms.assetid: eeab0120-c869-4c95-a79d-6dc418d0b23a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8b0060ea0bee5dc987f4f1188d7e4853c2d7e22c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633835"
---
# <a name="sp_syspolicy_delete_policy_category_subscription-transact-sql"></a>sp_syspolicy_delete_policy_category_subscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Elimina una suscripción de categoría de directiva para una base de datos concreta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syspolicy_delete_policy_category_subscription [ @policy_category_subscription_id = ] policy_category_subscription_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @policy_category_subscription_id = ] policy_category_subscription_id`Es el identificador de la suscripción de categoría de directiva. *policy_category_subscription_id* es de **tipo int**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_delete_policy_category_subscription en el contexto de la base de datos del sistema msdb.  
  
 No puede eliminar una suscripción de categoría de directiva cuando la suscripción está asignada.  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado se ejecuta en el contexto del propietario actual del procedimiento almacenado.  
  
 Para obtener los valores de *policy_category_subscription_id*, puede usar la siguiente consulta:  
  
```  
SELECT a.policy_category_subscription_id, a.target_object, b.name AS category_name  
FROM msdb.dbo.syspolicy_policy_category_subscriptions AS a  
INNER JOIN msdb.dbo.syspolicy_policy_categories AS b  
ON a.policy_category_id = b.policy_category_id;  
```  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina una suscripción de categoría de directiva con 1 como identificador.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_category_subscription @policy_category_subscription_id = 1;  
  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)  
  
  
