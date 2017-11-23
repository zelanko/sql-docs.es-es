---
title: "Eliminar suscripción de notificación de consulta (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bcb57bef390c6aa6e3debd5592ee7030c5c6b645
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita las suscripciones de notificación de consulta de la instancia. Esta instrucción puede quitar una suscripción específica o todas las suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>Argumentos  
 ALL  
 Quita todas las suscripciones de la instancia.  
  
 *subscription_id*  
 Quita la suscripción con el identificador de suscripción *subscription_id*.  
  
## <a name="remarks"></a>Comentarios  
 La instrucción KILL QUERY NOTIFICATION SUBSCRIPTION quita las suscripciones de notificación de consulta sin generar ningún mensaje de notificación.  
  
 *subscription_id* es el identificador de la suscripción como se muestra en la vista de administración dinámica [sys.dm_qn_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 Si el Id. de suscripción especificado no existe, la instrucción genera un error.  
  
## <a name="permissions"></a>Permissions  
 El permiso para ejecutar esta instrucción está restringido a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>A. Quitar todas las suscripciones de notificación de consulta de la instancia  
 En el siguiente ejemplo se quitan todas las suscripciones de notificación de consulta de la instancia  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. Quitar una sola suscripción de notificación de consulta  
 En el siguiente ejemplo se quita la suscripción de notificación de consulta con el Id. `73`.  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.dm_qn_subscriptions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
