---
title: DROP BROKER PRIORITY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs: TSQL
helpviewer_keywords: DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3724d9ad6724ef35b4514ab515b42a56ff9e8d43
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una prioridad de conversación de la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConversationPriorityName*  
 Especifica el nombre de la prioridad de conversación que se va a quitar.  
  
## <a name="remarks"></a>Comentarios  
 Al quitar una prioridad de conversación, cualquier conversación existente continúa funcionando con los niveles de prioridad asignados por la prioridad de conversación.  
  
## <a name="permissions"></a>Permissions  
 El permiso para crear una prioridad de conversación recae de forma predeterminada en los miembros de los roles fijos de base de datos db_ddladmin o db_owner, y en el rol fijo de servidor sysadmin. Requiere el permiso ALTER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita la prioridad de conversación denominada `InitiatorAToTargetPriority`.  
  
```  
DROP BROKER PRIORITY InitiatorAToTargetPriority;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [Sys.conversation_priorities &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
