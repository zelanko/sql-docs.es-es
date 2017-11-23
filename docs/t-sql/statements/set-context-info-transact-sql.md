---
title: SET CONTEXT_INFO (Transact-SQL) | Documentos de Microsoft
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
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs: TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a93e9f40690f37c0c161c635aea95589d47ef1e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Asocia hasta 128 bytes de información binaria con la sesión o la conexión actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>Argumentos  
 *binary_str*  
 Es un **binario** constante o una constante que es implícitamente convertible a **binario**, para asociarla a la sesión o conexión actual.  
  
 **@***binary_var*  
 Es un **varbinary** o **binario** variable que contiene un valor de contexto para asociarlo con la sesión o conexión actual.  
  
## <a name="remarks"></a>Comentarios  
 El modo preferido para recuperar la información de contexto para la sesión actual es utilizar la función CONTEXT_INFO. Información de contexto de sesión se almacena también en el **context_info** columnas en las vistas del sistema siguientes:  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 SET CONTEXT_INFO no se puede especificar en una función definida por el usuario. No puede proporcionar un valor NULL para SET CONTEXT_INFO porque las vistas que albergan los valores no permiten valores NULL.  
  
 SET CONTEXT_INFO no acepta expresiones distintas de nombres de constantes o variables. Para establecer la información de contexto en el resultado de una llamada de función, se debe incluir el resultado de la llamada de función en un **binario** o **varbinary** variable.  
  
 Cuando emite SET CONTEXT_INFO en un procedimiento almacenado o un desencadenador, a diferencia de otras instrucciones SET, los nuevos valores de la información de contexto persisten después de completarse el desencadenador o el procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>A. Establecer información de contexto utilizando una constante  
 El ejemplo siguiente muestra `SET CONTEXT_INFO` estableciendo el valor y mostrando los resultados. Tenga en cuenta que para consultar `sys.dm_exec_sessions` se requieren permisos SELECT y VIEW SERVER STATE, mientras que el uso de la función CONTEXT_INFO no los requiere.  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>B. Establecer información de contexto utilizando una función  
 En el ejemplo siguiente se muestra cómo utilizar el resultado de una función para establecer el valor de contexto, donde el valor de la función se debe colocar en primer lugar en un **binario** variable.  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Sys.dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Sys.dm_exec_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  
