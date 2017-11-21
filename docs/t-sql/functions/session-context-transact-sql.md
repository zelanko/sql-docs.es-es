---
title: SESSION_CONTEXT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23eea4b51009272ae06987ee2e9c1730750b3d6d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve el valor de la clave especificada en el contexto de la sesión actual. El valor se establece mediante el [sp_set_session_context &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) procedimiento.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>Argumentos  
 'key'  
 La clave (tipo sysname) del valor que se va a recuperar.  
  
## <a name="return-type"></a>Tipo devuelto  
 **sql_variant**  
  
## <a name="return-value"></a>Valor devuelto  
 El valor asociado con la clave especificada en el contexto de la sesión, o NULL si no se ha establecido ningún valor para esa clave.  
  
## <a name="permissions"></a>Permissions  
 Cualquier usuario puede leer el contexto de la sesión para la sesión.  
  
## <a name="remarks"></a>Comentarios  
 Comportamiento de MARS del SESSION_CONTEXT es similar de CONTEXT_INFO. Si un lote MARS establece un par de clave y valor, el nuevo valor no se devolverá en otras secciones de MARS en la misma conexión, a menos que inicien una vez completado el lote que estableció el valor nuevo. Si hay varios lotes de MARS activos en una conexión, no se puede establecer valores como "read_only." Esto evita que las condiciones de carrera y determinación sobre qué valor "gana".  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo establece el valor de contexto de sesión para la clave `user_id` a 4 y, a continuación, usa el **SESSION_CONTEXT** función para recuperar el valor.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40; Transact-SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  

