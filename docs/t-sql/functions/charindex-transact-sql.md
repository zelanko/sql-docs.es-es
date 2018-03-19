---
title: CHARINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- CHARINDEX
- CHARINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], pattern searching
- CHARINDEX function
- pattern searching [SQL Server]
- starting point of expression in character string
ms.assetid: 78c10341-8373-4b30-b404-3db20e1a3ac4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ed2f5334c0c76288ca31cf07857a87f2d1c72033
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Busca otra expresión y devuelve su posición inicial si se encuentra.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*expressionToFind*  
Es una [expression](../../t-sql/language-elements/expressions-transact-sql.md) de caracteres que contiene la secuencia que se va a buscar. *expressionToFind* tiene un límite de 8000 caracteres.
  
*expressionToSearch*  
Expresión de caracteres que se va a buscar.
  
*start_location*  
Es una expresión **integer** o **bigint** donde empieza la búsqueda. Si no se especifica *start_location*, es un número negativo o es igual a cero, la búsqueda empieza al principio de *expressionToSearch*.
  
## <a name="return-types"></a>Tipos de valores devueltos
**bigint** si *expressionToSearch* es de los tipos de datos **varchar(max)**, **nvarchar(max)** o **varbinary(max)**; en caso contrario, es **int**.
  
## <a name="remarks"></a>Notas  
Si *expressionToFind* o *expressionToSearch* son de un tipo de datos Unicode (**nvarchar** o **nchar**) y el otro no lo es, el otro se convertirá a un tipo de datos Unicode. CHARINDEX no se puede usar con tipos de datos **text**, **ntext** e **image**.
  
Si *expressionToFind* o *expressionToSearch* son NULL, CHARINDEX devuelve NULL.
  
Si *expressionToFind* no se encuentra dentro de *expressionToSearch*, CHARINDEX devuelve 0.
  
CHARINDEX realiza comparaciones basadas en la intercalación de la entrada. Para realizar una comparación de una intercalación especificada, puede utilizar COLLATE para aplicar una intercalación explícita a la entrada.
  
La posición inicial devuelta es de base 1, no de base 0.
  
0x0000 (**char(0)**) es un carácter no definido en las intercalaciones de Windows y no se puede incluir en CHARINDEX.
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
Al usar intercalaciones de SC, *start_location* y el valor devuelto cuentan los pares suplentes como un carácter, no como dos. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-starting-position-of-an-expression"></a>A. Devolver la posición inicial de una expresión  
El siguiente ejemplo devuelve la posición en la que empieza la secuencia de caracteres `bicycle` en la columna `DocumentSummary` de la tabla `Document` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
DECLARE @document varchar(64);  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bicycle', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
48            
```  
  
### <a name="b-searching-from-a-specific-position"></a>B. Buscar desde una posición concreta  
En este ejemplo se usa el parámetro opcional *start_location* para empezar la búsqueda de `vital` en el quinto carácter de la columna `DocumentSummary` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('vital', @document, 5);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
16            
  
(1 row(s) affected)  
```  
  
### <a name="c-searching-for-a-nonexistent-expression"></a>C. Buscar una expresión inexistente  
En este ejemplo se muestra el conjunto de resultados cuando el parámetro *expressionToFind* no se encuentra en *expressionToSearch*.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
  
(1 row(s) affected)
```
  
### <a name="d-performing-a-case-sensitive-search"></a>D. Realizar una búsqueda con distinción de mayúsculas y minúsculas  
En este ejemplo se realiza una búsqueda con distinción de mayúsculas y minúsculas de la cadena `'TEST'` en `'This is a Test``'`.
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
```  
  
En este ejemplo se realiza una búsqueda con distinción de mayúsculas y minúsculas de la cadena `'Test'` en `'This is a Test'`.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
### <a name="e-performing-a-case-insensitive-search"></a>E. Realizar una búsqueda sin distinción de mayúsculas y minúsculas  
En el siguiente ejemplo se realiza una búsqueda sin distinción de mayúsculas y minúsculas de la cadena `'TEST'` en `'This is a Test'`.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CI_AS);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. Buscar desde el principio de una expresión de cadena  
En este ejemplo se devuelve la primera ubicación de la cadena `is` en `This is a string`, empezando por la primera posición (el primer carácter) en la cadena.
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
3
```  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. Buscar desde una posición distinta de la primera posición  
En este ejemplo se devuelve la primera ubicación de la cadena `is` en `This is a string`, empezando por la cuarta posición.
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
 6
 ```  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. Resultados cuando no se encuentra la cadena  
En este ejemplo se muestra el valor devuelto cuando *string_pattern* no se encuentra en la cadena buscada.
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
0
```  
  
## <a name="see-also"></a>Vea también
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [+ &#40;String Concatenation&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  


