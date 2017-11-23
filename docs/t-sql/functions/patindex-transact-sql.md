---
title: PATINDEX (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
caps.latest.revision: "53"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: fd0df5a4dba946748dc39c245fcd54d50f1e97e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la posición inicial de la primera repetición de un patrón en la expresión especificada, o ceros si el patrón no se encuentra, en todos los tipos de datos de texto y caracteres.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *patrón*  
 Es una expresión de carácter que contiene la secuencia que se va a buscar. Pueden utilizar caracteres comodín; Sin embargo, el carácter % debe preceder y seguir *patrón* (excepto cuando busque primer o último carácter). *patrón de* es una expresión de la categoría de tipo de datos de cadena de caracteres. *patrón de* está limitado a 8000 caracteres.  
  
 *expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md), normalmente una columna que se busca el patrón especificado. *expresión* es de la categoría de tipo de datos de cadena de caracteres.  
  
## <a name="return-types"></a>Tipos devueltos  
 **bigint** si *expresión* reviste la **varchar (max)** o **nvarchar (max)** tipos de datos; en caso contrario **int**.  
  
## <a name="remarks"></a>Comentarios  
 Si el valor *patrón* o *expresión* es NULL, PATINDEX devuelve NULL.  
  
 PATINDEX realiza comparaciones basadas en la intercalación de la entrada. Para realizar una comparación de una intercalación especificada, puede utilizar COLLATE para aplicar una intercalación explícita a la entrada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 Al utilizar intercalaciones de SC, el valor devuelto contará cualquier par suplente de UTF-16 en el *expresión* parámetro como un único carácter. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 0 x 0000 (**char(0)**) es un carácter no definido en las intercalaciones de Windows y no se pueden incluir en PATINDEX.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-patindex-example"></a>A. Ejemplo sencillo de PATINDEX  
 En el ejemplo siguiente se comprueba una cadena de caracteres corto (`interesting data`) para la ubicación inicial de los caracteres `ter`.  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. Utilizar un patrón con PATINDEX  
 En el siguiente ejemplo se busca la posición en que comienza el patrón `ensure` en una fila específica de la columna `DocumentSummary` de la tabla `Document` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
 Si no restringe las filas que se van a buscar mediante una cláusula `WHERE`, la consulta devuelve todas las filas de la tabla e informa de valores distintos de cero para las filas en las que se encontró el modelo, y cero para todas las filas en las que no se encontró el modelo.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. Utilizar caracteres comodín con PATINDEX  
 En el siguiente ejemplo se utilizan los caracteres comodín % y _ para buscar la posición en la que comienza el modelo `'en'` en la cadena especificada, seguido de cualquier carácter y `'ure'` (el índice comienza en 1):  
  
```  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
 `PATINDEX` funciona igual que `LIKE`, por lo que se puede usar cualquiera de los caracteres comodín. No es necesario incluir el patrón entre caracteres de porcentaje. `PATINDEX('a%', 'abc')` devuelve 1 y `PATINDEX('%a', 'cba')` devuelve 3.  
  
 A diferencia de `LIKE`, `PATINDEX` devuelve una posición, de forma similar a `CHARINDEX`.  
  
### <a name="d-using-collate-with-patindex"></a>D. Utilizar COLLATE con PATINDEX  
 En el siguiente ejemplo se utiliza la función `COLLATE` para especificar de forma explícita la intercalación de la expresión que se está buscando.  
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. Usar una variable para especificar el patrón  
 En el ejemplo siguiente se utiliza una variable para pasar un valor para el *patrón* parámetro. Este ejemplo se utiliza la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos.  
  
```  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------  
 22
 ```  
  

  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40; Carácter comodín - carácter &#40; s &#41; para la coincidencia &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40; Carácter comodín - carácter &#40; s &#41; No en la coincidencia &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40; Carácter comodín - coincidir un carácter &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [Carácter de porcentaje &#40; Carácter comodín - carácter &#40; s &#41; para la coincidencia &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


