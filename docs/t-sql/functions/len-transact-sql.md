---
title: LEN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/03/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 532b996c23a8f9746a52434d78783da2a24d1add
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el número de caracteres de la expresión de cadena especificada, excluidos los espacios en blanco finales.  
  
> [!NOTE]  
>  Para devolver el número de bytes utilizados para representar una expresión, use el [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) función.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 Es la cadena [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que se debe evaluar. *string_expression* puede ser una constante, variable o columna de caracteres o datos binarios.  
  
## <a name="return-types"></a>Tipos devueltos  
 **bigint** si *expresión* reviste la **varchar (max)**, **nvarchar (max)** o **varbinary (max)** tipos de datos; en caso contrario, **int**.  
  
 Si utiliza intercalaciones de SC, el valor entero devuelto cuenta los pares suplentes UTF-16 como un solo carácter. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="remarks"></a>Comentarios  
 LEN excluye los espacios en blanco. Si es un problema, considere la posibilidad de usar el [DATALENGTH &#40; Transact-SQL &#41; ](../../t-sql/functions/datalength-transact-sql.md) función que no recorte la cadena. Si se procesa una cadena unicode, DATALENGTH devolverá dos veces el número de caracteres. En el ejemplo siguiente se muestra LEN y DATALENGTH con un espacio final.  
  
```  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
  
```  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente selecciona el número de caracteres y los datos en `FirstName` para las personas que se encuentran en `Australia`. En este ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El ejemplo siguiente devuelve el número de caracteres en la columna `FirstName` y los nombres y apellidos de los empleados que se encuentran en `Australia`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [IZQUIERDA &#40; Transact-SQL &#41;](../../t-sql/functions/left-transact-sql.md)   
 [DERECHA &#40; Transact-SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
  
  



