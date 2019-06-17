---
title: sp_syspolicy_add_policy_category_subscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_add_policy_category_subscription
- sp_syspolicy_add_policy_category_subscription_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category_subscription
ms.assetid: 4284f550-9a3f-4726-8181-15e407fbf08f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3dca1196f986da94ed17b1efb6f4284362e68b84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63002646"
---
# <a name="spsyspolicyaddpolicycategorysubscription-transact-sql"></a>sp_syspolicy_add_policy_category_subscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega una suscripción de categoría de directiva a la base de datos especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syspolicy_add_policy_category_subscription [ @target_type = ] 'target_type'  
    , [ @target_object = ] 'target_object'  
    , [ @policy_category = ] 'policy_category'  
    [ , [ @policy_category_subscription_id = ] policy_category_subscription_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @target_type = ] 'target_type'` Es el tipo de destino de la suscripción de categoría. *target_type* es **sysname**, es obligatorio y debe establecerse en 'DATABASE'.  
  
`[ @target_object = ] 'target_object'` Es el nombre de la base de datos que se suscribirá a la categoría. *target_object* es **sysname**y es necesario.  
  
`[ @policy_category = ] 'policy_category'` Es el nombre de la categoría de directiva para suscribirse a. *categoría_de_directiva* es **sysname**y es necesario.  
  
 Para obtener los valores de *categoría_de_directiva*, consulte la vista del sistema msdb.dbo.syspolicy_policy_categories.  
  
`[ @policy_category_subscription_id = ] policy_category_subscription_id` Es el identificador de la suscripción de categoría. *policy_category_subscription_id* es **int**y se devuelve como OUTPUT.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_add_policy_category_subscription en el contexto de la base de datos del sistema msdb.  
  
 Si especifica una categoría de directiva que no existe, se crea una categoría de directiva nueva y la suscripción se asigna para todas las bases de datos al ejecutar el procedimiento almacenado. Si luego borra la suscripción asignada para la nueva categoría, la suscripción solo se aplicará para la base de datos que especificó como *target_object*. Para obtener más información sobre cómo cambiar una configuración de suscripción asignada, vea [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado se ejecuta en el contexto del propietario actual del procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se configura la base de datos especificada para suscribirse a una categoría de directiva que se denomina 'Table Naming Policies'.  
  
```  
EXEC msdb.dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
, @target_object = N'AdventureWorks2012'  
, @policy_category = N'Table Naming Policies';  
  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_unsubscribe_from_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
