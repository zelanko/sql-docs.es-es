---
title: sp_syspolicy_unsubscribe_from_policy_category (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_unsubscribe_from_policy_category_TSQL
- sp_syspolicy_unsubscribe_from_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_unsubscribe_from_policy_category
ms.assetid: 47abab63-e605-40e8-a54e-2241e2e01afd
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c448584efd1921b7e88a84f17d2f53bb0596944
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spsyspolicyunsubscribefrompolicycategory-transact-sql"></a>sp_syspolicy_unsubscribe_from_policy_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina una suscripción de categoría de directiva para la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syspolicy_unsubscribe_from_policy_category [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@policy_category=** ] **'***categoría_de_directiva***'**  
 Es el nombre de la suscripción de categoría de directiva que se desea eliminar. *categoría_de_directiva* es **sysname**y es necesario.  
  
 Para obtener los valores de *categoría_de_directiva*, consulte la vista del sistema msdb.dbo.syspolicy_policy_categories.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_unsubscribe_from_policy_category en el contexto de la base de datos donde desee quitar una suscripción de categoría de directiva.  
  
## <a name="permissions"></a>Permissions  
 Requiere pertenencia al rol fijo de base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina una suscripción a la categoría de directiva 'Finance' para la base de datos especificada.  
  
```  
USE <database_name>;  
  
EXEC sys.sp_syspolicy_unsubscribe_from_policy_category @policy_category = N'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_subscribe_to_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql.md)  
  
  
