---
title: "+ (Concatenación de cadenas) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- concatenation
- +
- string
dev_langs:
- TSQL
helpviewer_keywords:
- concatenation [SQL Server]
- string concatenation operators
- + (string concatenation)
ms.assetid: 35cb3d7a-48f5-4b13-926c-a9d369e20ed7
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 1fd13b0b05dcb3b15d37d5a642a734b99ad004e5
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="-string-concatenation-transact-sql"></a>+ (Concatenación de cadenas) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Es un operador de una expresión de cadenas que concatena dos o más cadenas de caracteres o binarias, columnas o una combinación de nombres de columna y cadenas en una expresión (un operador de cadenas).  Por ejemplo `SELECT 'book'+'case';` devuelve `bookcase`.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression + expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de uno de los datos de tipos de los caracteres y la categoría de tipos de datos binarios, excepto el **imagen**, **ntext**, o **texto**tipos de datos. Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra.  
  
 Debe utilizarse una conversión explícita a datos caracteres cuando se concatenan cadenas binarias y cualesquiera caracteres entre las cadenas binarias. En el ejemplo siguiente se muestra cuándo `CONVERT`, o `CAST`, debe usarse con la concatenación binaria y cuándo `CONVERT`, o `CAST`, no tiene que usar.  
  
```  
DECLARE @mybin1 varbinary(5), @mybin2 varbinary(5)  
SET @mybin1 = 0xFF  
SET @mybin2 = 0xA5  
-- No CONVERT or CAST function is required because this example   
-- concatenates two binary strings.  
SELECT @mybin1 + @mybin2  
-- A CONVERT or CAST function is required because this example  
-- concatenates two binary strings plus a space.  
SELECT CONVERT(varchar(5), @mybin1) + ' '   
   + CONVERT(varchar(5), @mybin2)  
-- Here is the same conversion using CAST.  
SELECT CAST(@mybin1 AS varchar(5)) + ' '   
   + CAST(@mybin2 AS varchar(5))  
  
```  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con la mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 El operador + (Concatenación de cadenas) se comporta de modo distinto cuando trabaja con una cadena vacía de longitud cero que cuando trabaja con valores NULL o desconocidos. Se puede especificar una cadena de caracteres de longitud cero como dos comillas simples sin caracteres incluidos entre las comillas. Se puede especificar una cadena binaria de longitud cero como 0x sin ningún valor de byte especificado en la constante hexadecimal. La concatenación de una cadena de longitud cero siempre concatena las dos cadenas especificadas. Si trabaja con cadenas de valor NULL, el resultado de la concatenación depende de la configuración de la sesión. Al igual que en las operaciones aritméticas realizadas con valores NULL, si se agrega un valor NULL a un valor conocido, el resultado suele ser un valor desconocido y la operación de concatenación de cadenas que se realiza con un valor NULL también debe generar un resultado NULL. Sin embargo, puede cambiar este comportamiento si cambia la configuración de `CONCAT_NULL_YIELDS_NULL` para la sesión actual. Para obtener más información, vea [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
 Si el resultado de la concatenación de cadenas es superior al límite de 8.000 bytes, el resultado se trunca. Sin embargo, si una de las cadenas concatenadas como mínimo es un tipo de valor grande, no se produce el truncamiento.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-string-concatenation"></a>A. Usar la concatenación de cadenas  
 En el siguiente ejemplo se crea una sola columna en el encabezado de columna `Name` de varias columnas de caracteres, con el apellido de la persona seguido de una coma, un solo espacio y, a continuación, el nombre de la persona. El conjunto de resultados está en orden alfabético ascendente por el apellido y, a continuación, por el nombre.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM Person.Person  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="b-combining-numeric-and-date-data-types"></a>B. Combinar los tipos de datos numeric y date  
 En el ejemplo siguiente se usa el `CONVERT` función concatenar **numérico** y **fecha** tipos de datos.  
  
```  
-- Uses AdventureWorks  
  
SELECT 'The order is due on ' + CONVERT(varchar(12), DueDate, 101)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID = 50001;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------------------------------------------  
 The order is due on 04/23/2007  
 (1 row(s) affected)
 ```  
  
### <a name="c-using-multiple-string-concatenation"></a>C. Usar la concatenación de varias cadenas  
 En el siguiente ejemplo se concatenan varias cadenas para formar una cadena larga que muestra el apellido y la primera inicial de los vicepresidentes de [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]. Se agrega una coma después del apellido y un punto después de la primera inicial.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ',' + SPACE(1) + SUBSTRING(FirstName, 1, 1) + '.') AS Name, e.JobTitle  
FROM Person.Person AS p  
    JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle LIKE 'Vice%'  
ORDER BY LastName ASC;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name               Title  
 -------------      ---------------`  
 Duffy, T.          Vice President of Engineering  
 Hamilton, J.       Vice President of Production  
 Welcker, B.        Vice President of Sales  

 (3 row(s) affected)
 ```  
 
### <a name="d-using-large-strings-in-concatenation"></a>D. Usar cadenas grandes de concatenación
En el ejemplo siguiente se concatena varias cadenas para formar una cadena larga y, a continuación, intenta calcular la longitud de la cadena final. La longitud del final del conjunto de resultados es 16000, debe inicia la evaluación de expresión que queda es, @x + @z + @y = > (@x + @z) + @y. En este caso, el resultado de (@x + @z) se truncan a 8.000 bytes y, a continuación, @y se agrega al conjunto de resultados, lo que hace la longitud de la cadena final 16000. Puesto que @y es una cadena de tipo de valor grande, no producirse un truncamiento.

```
DECLARE @x varchar(8000) = replicate('x', 8000)
DECLARE @y varchar(max) = replicate('y', 8000)
DECLARE @z varchar(8000) = replicate('z',8000)
SET @y = @x + @z + @y
-- The result of following select is 16000
SELECT len(@y) AS y
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 y        
 -------  
 16000  
  
 (1 row(s) affected)
 ```  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-multiple-string-concatenation"></a>E. Usar la concatenación de varias cadenas  
 En el ejemplo siguiente se concatena varias cadenas para formar una cadena larga para mostrar el apellido y la primera inicial de los vicepresidentes dentro de una base de datos de ejemplo. Se agrega una coma después del apellido y un punto después de la primera inicial.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + SUBSTRING(FirstName, 1, 1) + '.') AS Name, Title  
FROM DimEmployee  
WHERE Title LIKE '%Vice Pres%'  
ORDER BY LastName ASC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name               Title                                           
-------------      ---------------  
Duffy, T.          Vice President of Engineering  
Hamilton, J.       Vice President of Production  
Welcker, B.        Vice President of Sales  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [+= &#40; Concatenación de cadenas &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)  
  
  




