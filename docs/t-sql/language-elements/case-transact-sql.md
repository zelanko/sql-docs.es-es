---
title: CASO (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CASE_TSQL
- CASE
dev_langs:
- TSQL
helpviewer_keywords:
- CASE expression [Transact-SQL]
- simple CASE expression
- comparing expressions
- searched CASE expression
ms.assetid: 658039ec-8dc2-4251-bc82-30ea23708cee
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b366f7b6d57adbed5f028171617abb7516f3260b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="case-transact-sql"></a>CASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Evalúa una lista de condiciones y devuelve una de las varias expresiones de resultado posibles.  
  
 La expresión CASE tiene dos formatos:  
  
-   La expresión CASE sencilla compara una expresión con un conjunto de expresiones sencillas para determinar el resultado.  
  
-   La expresión CASE buscada evalúa un conjunto de expresiones booleanas para determinar el resultado.  
  
 Ambos formatos admiten un argumento ELSE opcional.  
  
 CASE se puede utilizar en cualquier instrucción o cláusula que permite una expresión válida. Por ejemplo, puede utilizar CASE en instrucciones como SELECT, UPDATE, DELETE y SET, y en cláusulas como select_list, IN, WHERE, ORDER BY y HAVING.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
Simple CASE expression:   
CASE input_expression   
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END   
Searched CASE expression:  
CASE  
     WHEN Boolean_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CASE  
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
## <a name="arguments"></a>Argumentos  
 *input_expression*  
 Es la expresión evaluada cuando se utiliza el formato CASE sencillo. *input_expression* se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 Cuando *when_expression*  
 Es una expresión simple que *input_expression* se compara cuando se utiliza el formato CASE sencillo. *when_expression* es cualquier expresión válida. Los tipos de datos de *input_expression* y cada *when_expression* deben ser iguales o deben ser una conversión implícita.  
  
 A continuación, *result_expression*  
 Es la expresión devuelta cuando *input_expression* es igual a *when_expression* se evalúa como TRUE, o *Boolean_expression* se evalúa como TRUE. *expresión de resultado* se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 ELSE *else_result_expression*  
 Es la expresión que se devuelve si ninguna comparación se evalúa como TRUE. Si se omite este argumento y ninguna comparación se evalúa como TRUE, CASE devuelve NULL. *else_result_expression* es cualquier expresión válida. Los tipos de datos de *else_result_expression* y cualquier *result_expression* deben ser iguales o deben ser una conversión implícita.  
  
 Cuando *Boolean_expression*  
 Es la expresión booleana que se evalúa cuando se utiliza el formato CASE de búsqueda. *Boolean_expression* es cualquier expresión booleana válida.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el tipo de prioridad más alto del conjunto de tipos de *result_expressions* y opcional *else_result_expression*. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
### <a name="return-values"></a>Valores devueltos  
 **Expresión CASE simple:**  
  
 La expresión CASE simple compara la primera expresión con la expresión de cada cláusula WHEN para determinar si se da alguna equivalencia. Si estas expresiones son equivalentes, se devolverá la expresión de la cláusula THEN.  
  
-   Permite solo una comprobación de igualdad.  
  
-   En el orden especificado, evalúa input_expression = when_expression por cada cláusula WHEN.  
  
-   Devuelve el *result_expression* del primer *input_expression* = *when_expression* que se evalúa como TRUE.  
  
-   Si no hay ningún *input_expression* = *when_expression* se evalúa como TRUE, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] devuelve el *else_result_expression* si es una cláusula ELSE Especifica, o un valor NULL si no se especifica ninguna cláusula ELSE.  
  
 **Expresión CASE de búsqueda:**  
  
-   Da como resultado, en el orden especificado, *Boolean_expression* para cada cláusula WHEN.  
  
-   Devuelve *result_expression* del primer *Boolean_expression* que se evalúa como TRUE.  
  
-   Si no hay ningún *Boolean_expression* se evalúa como TRUE, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] devuelve el *else_result_expression* si se especifica una cláusula ELSE, o un valor NULL si no se especifica ninguna cláusula ELSE.  
  
## <a name="remarks"></a>Comentarios  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo permite 10 niveles de anidamiento en las expresiones CASE.  
  
 La expresión CASE no se puede utilizar para controlar el flujo de ejecución de los bloques de instrucciones, funciones definidas por el usuario, procedimientos almacenados e instrucciones de Transact-SQL. Para obtener una lista de métodos de control de flujo, vea [lenguaje de Control de flujo &#40; Transact-SQL &#41; ](~/t-sql/language-elements/control-of-flow.md).  
  
 La instrucción CASE devuelve las condiciones de forma secuencial y se detiene en la primera condición cuya condición se cumple. En algunas situaciones, se evalúa una expresión antes de que una instrucción CASE reciba los resultados de la expresión como entrada. Los errores de evaluación de estas expresiones son posibles. Las expresiones de agregado que aparecen en los argumentos WHEN para una instrucción CASE se evalúan primero y, a continuación, se proporcionan a la instrucción CASE. Por ejemplo, la siguiente consulta genera un error de división por cero al obtener el valor de agregado MAX. Esto ocurre antes de evaluar la expresión CASE.  
  
```tsql  
WITH Data (value) AS   
(   
SELECT 0   
UNION ALL   
SELECT 1   
)   
SELECT   
   CASE   
      WHEN MIN(value) <= 0 THEN 0   
      WHEN MAX(1/value) >= 100 THEN 1   
   END   
FROM Data ;  
```  
  
 Debe depender solo del orden de evaluación de las condiciones WHEN para las expresiones escalares (incluidas las subconsultas no correlacionadas que devuelven escalares), no para las expresiones de agregado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-a-select-statement-with-a-simple-case-expression"></a>A. Usar una instrucción SELECT con una expresión CASE sencilla  
 En una instrucción `SELECT`, una expresión `CASE` sencilla solo permite una comprobación de igualdad; no se pueden hacer otras comparaciones. En este ejemplo se utiliza la expresión `CASE` para cambiar la presentación de categorías de línea de productos con el fin de hacerla más comprensible.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   Name  
FROM Production.Product  
ORDER BY ProductNumber;  
GO  
  
```  
  
### <a name="b-using-a-select-statement-with-a-searched-case-expression"></a>B. Usar una instrucción SELECT con una expresión CASE de búsqueda  
 En una instrucción `SELECT`, la expresión `CASE` de búsqueda permite sustituir valores en el conjunto de resultados basándose en los valores de comparación. En el ejemplo siguiente se presenta el precio de venta como un comentario basado en el intervalo de precios de un producto.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Name, "Price Range" =   
      CASE   
         WHEN ListPrice =  0 THEN 'Mfg item - not for resale'  
         WHEN ListPrice < 50 THEN 'Under $50'  
         WHEN ListPrice >= 50 and ListPrice < 250 THEN 'Under $250'  
         WHEN ListPrice >= 250 and ListPrice < 1000 THEN 'Under $1000'  
         ELSE 'Over $1000'  
      END  
FROM Production.Product  
ORDER BY ProductNumber ;  
GO  
  
```  
  
### <a name="c-using-case-in-an-order-by-clause"></a>C. Usar CASE en una cláusula ORDER BY  
 En los ejemplos siguientes se utiliza la expresión CASE en una cláusula ORDER BY para determinar el criterio de ordenación de las filas según el valor de una columna dada. En el primer ejemplo se evalúe el valor de la columna `SalariedFlag` de la tabla `HumanResources.Employee`. Los empleados que tienen la columna `SalariedFlag` establecida en 1 se devuelven en orden descendente según el `BusinessEntityID`. Los empleados que tienen la columna `SalariedFlag` establecida en 0 se devuelven en orden ascendente según el `BusinessEntityID`. En el segundo ejemplo, el conjunto de resultados se ordena según la columna `TerritoryName` cuando la columna `CountryRegionName` es igual a 'United States' y según la columna `CountryRegionName` en las demás filas.  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
### <a name="d-using-case-in-an-update-statement"></a>D. Usar CASE en una instrucción UPDATE  
 En el ejemplo siguiente se usa la expresión CASE en una instrucción UPDATE para determinar el valor establecido en la columna `VacationHours` para los empleados con el valor de `SalariedFlag` establecido en 0. Al restar 10 horas de `VacationHours` da un valor negativo, `VacationHours` se incrementa en 40 horas; de lo contrario, `VacationHours` se incrementa en 20 horas. La cláusula OUTPUT se utiliza para mostrar los valores de las vacaciones antes y después.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)  
       END  
    )  
OUTPUT Deleted.BusinessEntityID, Deleted.VacationHours AS BeforeValue,   
       Inserted.VacationHours AS AfterValue  
WHERE SalariedFlag = 0;  
  
```  
  
### <a name="e-using-case-in-a-set-statement"></a>E. Usar CASE en una instrucción SET  
 En el ejemplo siguiente se usa la expresión CASE en una instrucción SET en la función con valores de tabla `dbo.GetContactInfo`. En la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], todos los datos relacionados con las personas están almacenados en la tabla `Person.Person`. Por ejemplo, la persona puede ser un empleado, el representante del proveedor o un cliente. La función devuelve el nombre y apellido de un determinado `BusinessEntityID` y el tipo de contacto para esa persona. La expresión CASE en la instrucción SET determina el valor para mostrar para la columna `ContactType` en función de la existencia de la `BusinessEntityID` columna en el `Employee`, `Vendor`, o `Customer` tablas.  
  
```  
  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.GetContactInformation(@BusinessEntityID int)  
    RETURNS @retContactInformation TABLE   
(  
BusinessEntityID int NOT NULL,  
FirstName nvarchar(50) NULL,  
LastName nvarchar(50) NULL,  
ContactType nvarchar(50) NULL,  
    PRIMARY KEY CLUSTERED (BusinessEntityID ASC)  
)   
AS   
-- Returns the first name, last name and contact type for the specified contact.  
BEGIN  
    DECLARE   
        @FirstName nvarchar(50),   
        @LastName nvarchar(50),   
        @ContactType nvarchar(50);  
  
    -- Get common contact information  
    SELECT   
        @BusinessEntityID = BusinessEntityID,   
@FirstName = FirstName,   
        @LastName = LastName  
    FROM Person.Person   
    WHERE BusinessEntityID = @BusinessEntityID;  
  
    SET @ContactType =   
        CASE   
            -- Check for employee  
            WHEN EXISTS(SELECT * FROM HumanResources.Employee AS e   
                WHERE e.BusinessEntityID = @BusinessEntityID)   
                THEN 'Employee'  
  
            -- Check for vendor  
            WHEN EXISTS(SELECT * FROM Person.BusinessEntityContact AS bec  
                WHERE bec.BusinessEntityID = @BusinessEntityID)   
                THEN 'Vendor'  
  
            -- Check for store  
            WHEN EXISTS(SELECT * FROM Purchasing.Vendor AS v            
                WHERE v.BusinessEntityID = @BusinessEntityID)   
                THEN 'Store Contact'  
  
            -- Check for individual consumer  
            WHEN EXISTS(SELECT * FROM Sales.Customer AS c   
                WHERE c.PersonID = @BusinessEntityID)   
                THEN 'Consumer'  
        END;  
  
    -- Return the information to the caller  
    IF @BusinessEntityID IS NOT NULL   
    BEGIN  
        INSERT @retContactInformation  
        SELECT @BusinessEntityID, @FirstName, @LastName, @ContactType;  
    END;  
  
    RETURN;  
END;  
GO  
  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(2200);  
GO  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(5);  
  
```  
  
### <a name="f-using-case-in-a-having-clause"></a>F. Usar CASE en una cláusula HAVING  
 En el ejemplo siguiente se utiliza la expresión CASE en una cláusula HAVING para restringir las filas devueltas por la instrucción SELECT. La instrucción devuelve el precio por hora máximo para cada puesto de trabajo en el `HumanResources.Employee` tabla. La cláusula HAVING restringe los títulos a aquellos que tienen los hombres con una tasa de pago máxima mayor que 40 dólares o las mujeres con una tasa de pago máxima mayor que 42 dólares.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, MAX(ph1.Rate)AS MaximumRate  
FROM HumanResources.Employee AS e  
JOIN HumanResources.EmployeePayHistory AS ph1 ON e.BusinessEntityID = ph1.BusinessEntityID  
GROUP BY JobTitle  
HAVING (MAX(CASE WHEN Gender = 'M'   
        THEN ph1.Rate   
        ELSE NULL END) > 40.00  
     OR MAX(CASE WHEN Gender  = 'F'   
        THEN ph1.Rate    
        ELSE NULL END) > 42.00)  
ORDER BY MaximumRate DESC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-using-a-select-statement-with-a-case-expression"></a>G. Usar una instrucción SELECT con una expresión CASE  
 Dentro de una instrucción SELECT, la expresión CASE permite valores que se pueden sustituir en el conjunto de resultados en función de los valores de comparación. En el ejemplo siguiente se usa la expresión CASE para cambiar la presentación de categorías de línea de productos para que resulten más comprensibles. Cuando no existe ningún valor, el texto "no para la venta ' se muestra.  
  
```  
-- Uses AdventureWorks  
  
SELECT   ProductAlternateKey, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   EnglishProductName  
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="h-using-case-in-an-update-statement"></a>H. Usar CASE en una instrucción UPDATE  
 En el ejemplo siguiente se usa la expresión CASE en una instrucción UPDATE para determinar el valor establecido en la columna `VacationHours` para los empleados con el valor de `SalariedFlag` establecido en 0. Al restar 10 horas de `VacationHours` da un valor negativo, `VacationHours` se incrementa en 40 horas; de lo contrario, `VacationHours` se incrementa en 20 horas.  
  
```  
-- Uses AdventureWorks   
  
UPDATE dbo.DimEmployee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)   
       END  
    )   
WHERE SalariedFlag = 0;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [COALESCE &#40; Transact-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [IIF &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [Elija &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  




