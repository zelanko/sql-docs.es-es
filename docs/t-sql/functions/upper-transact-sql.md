---
title: SUPERIOR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPPER_TSQL
- UPPER
dev_langs:
- TSQL
helpviewer_keywords:
- UPPER function
- characters [SQL Server], lowercase
- converting lowercase to uppercase
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
ms.assetid: 5ced55f7-ac89-4cf2-9465-f63f4dc480db
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7572e82178b211fba9967a88cb16c20d059c7b52
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="upper-transact-sql"></a>UPPER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una expresión de caracteres con datos de caracteres en minúsculas convertidos a mayúsculas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de datos de caracteres. *character_expression* puede ser una constante, variable o columna de caracteres o datos binarios.  
  
 *character_expression* debe ser de un tipo de datos que es implícitamente convertible a **varchar**. De lo contrario, utilice [conversión](../../t-sql/functions/cast-and-convert-transact-sql.md) para convertir explícitamente *character_expression*.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varchar** o **nvarchar**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utilizan las funciones `UPPER` y `RTRIM` para devolver el apellido de las personas de la tabla `Person` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] de manera que aparezca en mayúsculas, recortado y concatenado con el nombre.  
  
```  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM Person.Person  
ORDER BY LastName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se usa el `UPPER` y `RTRIM` funciones para devolver el apellido de las personas de la `dbo.DimEmployee` para que esté en mayúsculas, recortado y concatenado con el nombre de tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM dbo.DimEmployee  
ORDER BY LastName;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
Name
------------------------------
ABBAS, Syed
ABERCROMBIE, Kim
ABOLROUS, Hazem
 ```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


