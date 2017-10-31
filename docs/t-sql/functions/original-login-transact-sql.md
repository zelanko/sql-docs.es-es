---
title: ORIGINAL_LOGIN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1f97da47505e5c812e43f4481d9f36027bf14c9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el nombre del inicio de sesión que se conectó a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede utilizar esta función para devolver la identidad del inicio de sesión original en sesiones en las que hay varios cambios de contexto explícitos o implícitos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **sysname**  
  
## <a name="remarks"></a>Comentarios  
 Esta función puede resultar útil para la auditoría de la identidad del contexto de conexión original. Mientras que las funciones como [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) y [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md) devuelven el contexto de ejecución actual, ORIGINAL_LOGIN devuelve la identidad del inicio de sesión que se conectó por primera vez a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en esa sesión.  
  
 Devuelve NULL en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente cambia el contexto de ejecución de la sesión actual desde el solicitante de las instrucciones para `login1`. Las funciones `SUSER_SNAME` y `ORIGINAL_LOGIN` se utilizan para devolver el usuario de la sesión actual (el usuario al que se cambió el contexto), y la cuenta de inicio de sesión original.  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [EJECUTAR AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [REVERTIR &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  

