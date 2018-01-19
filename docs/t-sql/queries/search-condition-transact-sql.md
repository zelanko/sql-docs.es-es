---
title: "(Transact-SQL) de la condición de búsqueda | Documentos de Microsoft"
ms.custom: 
ms.date: 01/15/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- search
- Search Condition
- condition
dev_langs: TSQL
helpviewer_keywords:
- OR operator [Transact-SQL]
- CONTAINS predicate (Transact-SQL)
- ESCAPE keyword
- operators [Transact-SQL], search condition
- search conditions [SQL Server]
- WHERE clause, search conditions
- ALL keyword
- FREETEXT predicate (Transact-SQL)
- EXISTS keyword
- search conditions [SQL Server], about search conditions
- NOT operator [Transact-SQL]
- BETWEEN operator
- SOME | ANY keyword
- predicates [full-text search]
- AND, about search conditions
- logical operators [SQL Server], about search conditions
- precedence [SQL Server], logical operators
- logical operators [SQL Server], precedence
- LIKE comparisons
ms.assetid: 09974469-c5d2-4be8-bc5a-78e404660b2c
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e507b4e7e14c68f629708255a1cfd6ab06cadb5f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="search-condition-transact-sql"></a>Condiciones de búsqueda (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Es una combinación de uno o varios predicados que utilizan los operadores lógicos AND, OR y NOT.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<search_condition> ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '<contains_search_condition>' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery )     }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
< search_condition > ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | < | < = } expression   
    | string_expression [ NOT ] LIKE string_expression   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | expression [ NOT ] IN (subquery | expression [ ,...n ] )   
    | expression [ NOT ] EXISTS (subquery)     }   
```  
  
## <a name="arguments"></a>Argumentos  
 \<search_condition>  
 Especifica las condiciones de las filas devueltas en el conjunto de resultados de una instrucción SELECT, una expresión de consulta o una subconsulta. En una instrucción UPDATE, especifica las filas que se van a actualizar. En una instrucción DELETE, especifica las filas que se van a eliminar. No hay límite en el número de predicados que se pueden incluir en una condición de búsqueda de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 NOT  
 Niega la expresión booleana que especifica el predicado. Para obtener más información, vea [no &#40; Transact-SQL &#41; ](../../t-sql/language-elements/not-transact-sql.md).  
  
 y  
 Combina dos condiciones y se evalúa como TRUE cuando ambas condiciones son TRUE. Para obtener más información, vea [AND &#40; Transact-SQL &#41; ](../../t-sql/language-elements/and-transact-sql.md).  
  
 O BIEN  
 Combina dos condiciones y se evalúa como TRUE cuando alguna de las condiciones es TRUE. Para obtener más información, consulte [o &#40; Transact-SQL &#41; ](../../t-sql/language-elements/or-transact-sql.md).  
  
 \<predicado >  
 Es una expresión que devuelve TRUE, FALSE o UNKNOWN.  
  
 *expression*  
 Es un nombre de columna, una constante, una función, una variable, una subconsulta escalar o cualquier combinación de nombres de columna, constantes y funciones conectados mediante uno o varios operadores o una subconsulta. La expresión también puede contener la expresión CASE.  
  
> [!NOTE]  
>  Las variables y constantes de cadena no Unicode usan la página de códigos que se corresponde con la intercalación predeterminada de la base de datos. Pueden producirse can de conversiones de página de código cuando se trabaja con datos de caracteres no Unicode solo y hacer referencia a los tipos de datos de caracteres no Unicode **char**, **varchar**, y **texto**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Convierte las variables y constantes de cadena no Unicode en la página de códigos que corresponde a la intercalación de la columna que se hace referencia o se especificó utilizar COLLATE, si dicha página de códigos es diferente de la página de códigos que se corresponde con la intercalación predeterminada de la base de datos. Los caracteres no se encuentren en la nueva página de códigos se traducirá en un carácter similar, si un [asignación con ajuste perfecto](http://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/) puede encontrarse, o bien se convertirá en el carácter de reemplazo predeterminado de "?".  
>  
> Cuando se trabaja con varias páginas de códigos, las constantes de caracteres pueden llevar un prefijo con la letra mayúscula ' n ' y Unicode pueden utilizar las variables, para evitar las conversiones de páginas de código.  
  
 =  
 Es el operador que se utiliza para probar la igualdad entre dos expresiones.  
  
 <>  
 Es el operador que se utiliza para probar si dos expresiones no son iguales entre sí.  
  
 !=  
 Es el operador que se utiliza para probar si dos expresiones no son iguales entre sí.  
  
 \>  
 Es el operador que se utiliza para probar si una expresión es mayor que la otra.  
  
 \>=  
 Es el operador que se utiliza para probar si una expresión es mayor o igual que la otra expresión.  
  
 !>  
 Es el operador que se utiliza para probar si una expresión no es mayor que la otra expresión.  
  
 <  
 Es el operador que se utiliza para probar si una expresión es menor que la otra.  
  
 <=  
 Es el operador que se utiliza para probar si una expresión es menor o igual que la otra expresión.  
  
 !<  
 Es el operador que se utiliza para probar si una expresión no es menor que la otra expresión.  
  
 *string_expression*  
 Es una cadena de caracteres y caracteres comodín.  
  
 [ NOT ] LIKE  
 Indica que la siguiente cadena de caracteres se utilizará con la coincidencia de patrón. Para obtener más información, vea [como &#40; Transact-SQL &#41; ](../../t-sql/language-elements/like-transact-sql.md).  
  
 ESCAPE **'***escape_ caracteres***'**  
 Permite buscar un carácter comodín en una cadena de caracteres sin que funcione como carácter comodín. *escape_character* es el carácter que se coloca delante del carácter comodín para indicar su uso especial.  
  
 [ NOT ] BETWEEN  
 Especifica un intervalo inclusivo de valores. Utilice AND para separar los valores inicial y final. Para obtener más información, vea [BETWEEN &#40; Transact-SQL &#41; ](../../t-sql/language-elements/between-transact-sql.md).  
  
 IS [NOT] NULL  
 Especifica una búsqueda de valores NULL o de valores que no son NULL, en función de las palabras clave utilizadas. Una expresión que contenga un operador bit a bit o aritmético se evalúa como NULL si uno de los operandos es NULL.  
  
 CONTAINS  
 Busca en las columnas que contienen datos basados en caracteres coincidencias precisas o menos precisas (*aproximada*) coincide con palabras simples o frases, la proximidad de las palabras que se encuentran a cierta distancia de entre sí y coincidencias ponderadas. Esta opción solo puede usarse con instrucciones SELECT. Para obtener más información, vea [CONTAINS &#40; Transact-SQL &#41; ](../../t-sql/queries/contains-transact-sql.md).  
  
 FREETEXT  
 Proporciona una forma sencilla de realizar consultas en lenguaje natural al buscar, en columnas con datos basados en caracteres, valores que coincidan con el significado en lugar de con las palabras exactas del predicado. Esta opción solo puede usarse con instrucciones SELECT. Para obtener más información, vea [FREETEXT &#40; Transact-SQL &#41; ](../../t-sql/queries/freetext-transact-sql.md).  
  
 [ NOT ] IN  
 Especifica la búsqueda de una expresión, basada en si la expresión está incluida en una lista o excluida de ella. La expresión de búsqueda puede ser una constante o un nombre de columna, y la lista puede ser un conjunto de constantes o, más normalmente, una subconsulta. Encierre la lista de valores entre paréntesis. Para obtener más información, vea [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md).  
  
 *subquery*  
 Puede considerarse como una instrucción SELECT restringida y es similar a \<query_expresssion > en la instrucción SELECT. No se permiten la cláusula ORDER BY ni la palabra clave INTO. Para obtener más información, vea [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
 ALL  
 Se utiliza con un operador de comparación y una subconsulta. Devuelve TRUE para \<predicado > cuando todos los valores obtenidos de la subconsulta satisfacen la operación de comparación, o FALSE si no todos los valores satisfacen la comparación o cuando la subconsulta no devuelve filas a la instrucción externa. Para obtener más información, vea [todos &#40; Transact-SQL &#41; ](../../t-sql/language-elements/all-transact-sql.md).  
  
 { SOME | ANY }  
 Se utiliza con un operador de comparación y una subconsulta. Devuelve TRUE para \<predicado > cuando se recupera cualquier valor de la subconsulta satisface la operación de comparación, o FALSE si ningún valor de la subconsulta satisfacen la comparación o cuando la subconsulta no devuelve filas a la instrucción externa. En caso contrario, la expresión es UNKNOWN. Para obtener más información, vea [algunos &#124; CUALQUIER &#40; Transact-SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 EXISTS  
 Se utiliza con una subconsulta para probar la existencia de filas devueltas por la subconsulta. Para obtener más información, vea [EXISTS &#40; Transact-SQL &#41; ](../../t-sql/language-elements/exists-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 El orden de prioridad de los operadores lógicos es NOT (el más alto), seguido de AND y OR. Se pueden utilizar paréntesis para invalidar esta prioridad en una condición de búsqueda. El orden de evaluación de los operadores lógicos puede variar dependiendo de las opciones elegidas por el optimizador de consultas. Para obtener más información acerca de cómo funcionan los operadores lógicos con valores lógicos, consulte [AND &#40; Transact-SQL &#41; ](../../t-sql/language-elements/and-transact-sql.md), [o &#40; Transact-SQL &#41; ](../../t-sql/language-elements/or-transact-sql.md), y [no &#40; Transact-SQL &#41; ](../../t-sql/language-elements/not-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-where-with-like-and-escape-syntax"></a>A. Usar WHERE con la sintaxis de LIKE y ESCAPE  
 En el ejemplo siguiente se busca filas en las que el `LargePhotoFileName` columna tiene los caracteres `green_`y utiliza el `ESCAPE` opción porque _ es un carácter comodín. Sin especificar la `ESCAPE` opción, la consulta buscaría los valores de descripción que contengan la palabra `green` seguido de cualquier carácter individual diferente del carácter _.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT *   
FROM Production.ProductPhoto  
WHERE LargePhotoFileName LIKE '%greena_%' ESCAPE 'a' ;  
```  
  
### <a name="b-using-where-and-like-syntax-with-unicode-data"></a>B. Usar la sintaxis de WHERE y LIKE con datos Unicode  
 En el siguiente ejemplo se utiliza la cláusula `WHERE` para recuperar la dirección de correo de una empresa que está fuera de los Estados Unidos (`US`) y en una ciudad cuyo nombre empieza con `Pa`.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT AddressLine1, AddressLine2, City, PostalCode, CountryRegionCode    
FROM Person.Address AS a  
JOIN Person.StateProvince AS s ON a.StateProvinceID = s.StateProvinceID  
WHERE CountryRegionCode NOT IN ('US')  
AND City LIKE N'Pa%' ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-where-with-like"></a>C. Usar WHERE con LIKE  
 En el ejemplo siguiente se busca filas en las que el `LastName` columna tiene los caracteres `and`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE '%and%';  
```  
  
### <a name="d-using-where-and-like-syntax-with-unicode-data"></a>D. Usar la sintaxis de WHERE y LIKE con datos Unicode  
 En el ejemplo siguiente se usa el `WHERE` cláusula para realizar una búsqueda de Unicode en la `LastName` columna.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE N'%and%';  
```  
  
## <a name="see-also"></a>Vea también  
 [Las funciones de agregado &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

