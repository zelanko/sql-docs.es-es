---
title: ELSE (IF... ELSE) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18adc4f441fddecdb3cd96c2a253268a16daea46
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="else-ifelse-transact-sql"></a>ELSE (IF...ELSE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Impone condiciones en la ejecución de una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)]. El [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción (*sql_statement*) siguiente la *Boolean_expression*se ejecuta si la *Boolean_expression* se evalúa como TRUE. La palabra clave opcional ELSE es una alternativa [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción que se ejecuta cuando *Boolean_expression* se evalúa como FALSE o NULL.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Boolean_expression*  
 Es una expresión que devuelve TRUE o FALSE. Si el *Boolean_expression* contiene una instrucción SELECT, la instrucción SELECT debe ir entre paréntesis.  
  
 { *sql_statement* | *bloqueInstrucción* }  
 Se trata de cualquier instrucción o grupo de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] válidas definidas con un bloque de instrucciones. Para definir un bloque de instrucciones (proceso por lotes), utilice las palabras clave de lenguaje de control de flujo BEGIN y END. Aunque todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] son válidas en un bloque BEGIN...END, ciertas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] no deben agruparse en el mismo lote (bloque de instrucciones).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. Utilizar una expresión booleana simple  
 El ejemplo siguiente tiene una expresión booleana simple (`1=1`) que es true y, por lo tanto, se imprime la primera instrucción.  
  
```  
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 En el ejemplo siguiente hay una expresión booleana simple (`1=2`) que es FALSE y, por tanto, se imprime la segunda instrucción.  
  
```  
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>B. Utilizar una consulta en una expresión booleana  
 En el ejemplo siguiente se ejecuta una consulta en la expresión booleana. Dado que hay 10 bicicletas en la tabla `Product` que cumplen la cláusula `WHERE`, se ejecutará la primera instrucción de impresión. Cambie `> 5` por `> 15` para ver cómo podría ejecutarse la segunda parte de la instrucción.  
  
```  
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. Utilizar un bloque de instrucciones  
 En el ejemplo siguiente se ejecuta una consulta en la expresión booleana y, a continuación, se ejecutan bloques de instrucciones con pequeñas diferencias que dependen del resultado de la expresión booleana. Cada bloque de instrucciones comienza con `BEGIN` y finaliza con `END`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight decimal(8,2), @BikeCount int  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS varchar(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. Utilizar instrucciones IF...ELSE anidadas  
 En el ejemplo siguiente se muestra cómo una IF... ELSE (instrucción) se puede anidar dentro de otra. Establezca la variable `@Number` en `5`, `50` y `500` para probar cada instrucción.  
  
```  
DECLARE @Number int;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E: mediante una consulta como parte de una expresión booleana  
 En el ejemplo siguiente se utiliza `IF…ELSE` determinar cuál de las dos respuestas para mostrar al usuario, en función del peso de un elemento en el `DimProduct` tabla.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Lenguaje de control de flujo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  



