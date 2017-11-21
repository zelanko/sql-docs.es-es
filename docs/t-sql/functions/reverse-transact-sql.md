---
title: REVERSE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REVERSE_TSQL
- REVERSE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], reverse
- REVERSE function
- reverse character expressions
ms.assetid: 555d8877-7cc7-4955-ae2c-6215aca313b7
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 86c7d027057c851ae52d3627aa5ff2591f95bf8a
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="reverse-transact-sql"></a>REVERSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el orden inverso de un valor de cadena.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
REVERSE ( string_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 *string_expression* es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de un tipo de datos binario o de cadena. *string_expression* puede ser una constante, variable o columna de caracteres o datos binarios.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varchar** o **nvarchar**  
  
## <a name="remarks"></a>Comentarios  
 *string_expression* debe ser de un tipo de datos que es implícitamente convertible a **varchar**. De lo contrario, utilice [conversión](../../t-sql/functions/cast-and-convert-transact-sql.md) para convertir explícitamente *string_expression*.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 Al utilizar las intercalaciones de SC, la función REVERSE no invertirá el orden de dos mitades de un par suplente.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelven los nombres de todos los contactos con los caracteres invertidos. En este ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
SELECT FirstName, REVERSE(FirstName) AS Reverse  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstName      Reverse
-------------- --------------
Ken            neK
Rob            boR
Roberto        otreboR
Terri          irreT

(4 row(s) affected)
```  
  
 En el ejemplo siguiente se invierten los caracteres de una variable.  
  
```  
DECLARE @myvar varchar(10);  
SET @myvar = 'sdrawkcaB';  
SELECT REVERSE(@myvar) AS Reversed ;  
GO  
```  
  
 En el ejemplo siguiente se realiza una conversión implícita de un **int** de tipo de datos en **varchar** tipo de datos y, a continuación, se invierte el resultado.  
  
```  
SELECT REVERSE(1234) AS Reversed ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El ejemplo siguiente devuelve los nombres de todas las bases de datos y los nombres con los caracteres invierten.  
  
```  
SELECT name, REVERSE(name) FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


