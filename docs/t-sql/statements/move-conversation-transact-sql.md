---
title: MOVE CONVERSATION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
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
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs: TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: "28"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd8c5e548bf45fe4a2fc6bf0638ebb5282981263
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mueve una conversación a otro grupo de conversación diferente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *conversation_handle*  
 Es una variable o una constante que contiene el identificador de conversación de la conversación que se va a mover. *conversation_handle* debe ser de tipo **uniqueidentifier**.  
  
 TO *conversation_group_id*  
 Es una variable o una constante que contiene el identificador del grupo de conversación donde se va a mover la conversación. *conversation_group_id* debe ser de tipo **uniqueidentifier**.  
  
## <a name="remarks"></a>Comentarios  
 La instrucción MOVE CONVERSATION mueve la conversación especificada por *conversation_handle* para el grupo de conversación identificado por *conversation_group_id*. Los diálogos solo se pueden redirigir entre grupos de conversación que están asociados a la misma cola.  
  
> [!IMPORTANT]  
>  Si la instrucción MOVE CONVERSATION no es la primera instrucción de un lote o procedimiento almacenado, la instrucción anterior debe terminarse con punto y coma (**;**), el [!INCLUDE[tsql](../../includes/tsql-md.md)] terminador de instrucción.  
  
 La instrucción MOVE CONVERSATION bloquea el grupo de conversación asociado *conversation_handle* y el grupo de conversación especificado por *conversation_group_id* hasta que la transacción que contiene la instrucción se confirma o revierte.  
  
 MOVE CONVERSATION no es válido en una función definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Para mover una conversación, el usuario actual debe ser el propietario de la conversación y el grupo de conversación, o miembro del rol fijo de servidor sysadmin o miembro del rol fijo de base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se mueve una conversación a otro grupo de conversación.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>Vea también  
 [EMPEZAR conversación de diálogo &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [Finalizar conversación &#40; Transact-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
