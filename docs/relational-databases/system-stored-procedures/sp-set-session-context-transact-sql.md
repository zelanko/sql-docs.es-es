---
title: sp_set_session_context (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d1396ef79eb69b96a40f075c50cd38b6ad77d24
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spsetsessioncontext-transact-sql"></a>sp_set_session_context (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Establece un par clave-valor en el contexto de la sesión.  
  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_set_session_context [ @key= ] 'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @key=] 'key'  
 La clave que se va a establecer, de tipo **sysname**. El tamaño de clave máximo es de 128 bytes.  
  
 [ @value=] 'value'  
 El valor de la clave especificada, de tipo **sql_variant**. Establecer un valor NULL, libera la memoria. El tamaño máximo es 8.000 bytes.  
  
 [ @read_only= ] { 0 | 1 }  
 Un indicador de tipo **bits**. Si es 1, a continuación, el valor de la clave especificada no se podrá cambiar en esta conexión lógica. Si 0 (valor predeterminado) y, a continuación, el valor se puede cambiar.  
  
## <a name="permissions"></a>Permissions  
 Cualquier usuario puede establecer un contexto de sesión para la sesión.  
  
## <a name="remarks"></a>Comentarios  
 Al igual que otros procedimientos almacenados, solo literales y variables (no expresiones o llamadas a funciones) se pueden pasar como parámetros.  
  
 El tamaño total del contexto de sesión está limitado a 256 kb. Si el conjunto un valor que hace que se ha superado este límite, la instrucción produce un error. Puede supervisar el uso de memoria en [sys.dm_os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 Puede supervisar el uso de memoria por consulta [sys.dm_os_memory_cache_counters &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) como se indica a continuación: `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo establecer y, a continuación, devolver una clave de contexto de las sesiones con el nombre de idioma con un valor de inglés.  
  
```  
EXEC sp_set_session_context 'language', 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 En el ejemplo siguiente se muestra el uso de la marca opcional de solo lectura.  
  
```  
EXEC sp_set_session_context 'user_id', 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
