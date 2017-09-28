---
title: USER_NAME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_NAME
- USER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- IDs [SQL Server], databases
- USER_NAME function
- users [SQL Server], database username
- names [SQL Server], database users
- identification numbers [SQL Server], databases
- database usernames [SQL Server]
ms.assetid: ab32d644-4228-449a-9ef0-5a975c305775
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5179a5d031dbc654f1624f4d64c3e94bf28efe40
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="username-transact-sql"></a>USER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un nombre de usuario de base de datos a partir de un número de identificación especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
USER_NAME ( [ id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *id*  
 Es el número de identificación asociado a un usuario de la base de datos. *Id. de*es **int**. Es obligatorio utilizar paréntesis.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar(256)**  
  
## <a name="remarks"></a>Comentarios  
 Cuando *identificador* es se omite, se supone que el usuario actual en el contexto actual. Si el parámetro contiene la palabra que null, devolverá NULL. Cuando se llama a USER_NAME sin especificar un *identificador* después de una ejecución como instrucción, USER_NAME devuelve el nombre del usuario suplantado. Si una entidad de seguridad de Windows ha tenido acceso a la base de datos en forma de miembro de un grupo, USER_NAME devuelve el nombre de la entidad de seguridad de Windows en vez del nombre del grupo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-username"></a>A. Usar USER_NAME  
 En el siguiente ejemplo se devuelve el nombre de usuario del Id. de usuario `13`.  
  
```  
SELECT USER_NAME(13);  
GO  
```  
  
### <a name="b-using-username-without-an-id"></a>B. Usar USER_NAME sin un identificador  
 En el siguiente ejemplo se busca el nombre del usuario actual sin especificar un identificador.  
  
```  
SELECT USER_NAME();  
GO  
```  
  
 Este es el conjunto de resultados para un usuario que pertenezca al rol fijo de servidor sysadmin.  
  
 `------------------------------`  
  
 `dbo`  
  
 `(1 row(s) affected)`  
  
### <a name="c-using-username-in-the-where-clause"></a>C. Usar USER_NAME en la cláusula WHERE  
 En el siguiente ejemplo se busca la fila en `sysusers` en la que el nombre sea igual al resultado de aplicar la función del sistema `USER_NAME` al número de identificador de usuario `1`.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `name`  
  
 `------------------------------`  
  
 `dbo`  
  
 `(1 row(s) affected)`  
  
### <a name="d-calling-username-during-impersonation-with-execute-as"></a>D. Llamar a USER_NAME durante la suplantación con EXECUTE AS  
 En el siguiente ejemplo se muestra cómo se comporta `USER_NAME` durante la suplantación.  
  
```  
SELECT USER_NAME();  
GO  
EXECUTE AS USER = 'Zelig';  
GO  
SELECT USER_NAME();  
GO  
REVERT;  
GO  
SELECT USER_NAME();  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DBO`  
  
 `Zelig`  
  
 `DBO`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-username"></a>E. Usar USER_NAME  
 En el siguiente ejemplo se devuelve el nombre de usuario del Id. de usuario `13`.  
  
```  
SELECT USER_NAME(13);  
```  
  
### <a name="f-using-username-without-an-id"></a>F. Usar USER_NAME sin un identificador  
 En el siguiente ejemplo se busca el nombre del usuario actual sin especificar un identificador.  
  
```  
SELECT USER_NAME();  
```  
  
 Este es el conjunto de resultados para un usuario ha iniciado sesión actualmente.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------------------------   
User7                              
```  
  
### <a name="g-using-username-in-the-where-clause"></a>G. Usar USER_NAME en la cláusula WHERE  
 En el siguiente ejemplo se busca la fila en `sysusers` en la que el nombre sea igual al resultado de aplicar la función del sistema `USER_NAME` al número de identificador de usuario `1`.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
name                             
------------------------------   
User7                              
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40; Transact-SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40; Transact-SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40; Transact-SQL &#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SYSTEM_USER &#40; Transact-SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)  
  
  


