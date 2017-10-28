---
title: "Especificar parámetros | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: e1b3e7db23ce9435b5d57156f2dcfd920d4d3e11
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="specify-parameters"></a>Especificar parámetros
  Al especificar parámetros de procedimiento, los programas de llamada pueden pasar valores en el cuerpo del procedimiento. Estos valores se pueden usar para distintos fines durante la ejecución del procedimiento. Los parámetros de procedimiento también pueden devolver valores al programa de llamada si el parámetro se marca como OUTPUT.  
  
 Un procedimiento puede tener un máximo de 2100 parámetros; cada uno con un nombre, un tipo de datos y una dirección asignados. Opcionalmente, a los parámetros se les pueden asignar valores predeterminados.  
  
 En la siguiente sección se proporciona información acerca de cómo pasar valores en parámetros y cómo se usa cada uno de los atributos de parámetro durante una llamada a procedimiento.  
  
## <a name="passing-values-into-parameters"></a>Pasar valores en parámetros  
 Los valores de parámetro suministrados con una llamada a procedimiento deben ser constantes o una variable; no se puede usar un nombre de función como valor de parámetro. Las variables pueden ser definidas por el usuario o ser variables del sistema, como @@spid.  
  
 En los siguientes ejemplos se muestra cómo se pasan valores de parámetros al `uspGetWhereUsedProductID`del procedimiento. Ilustran cómo pasar parámetros como constantes y variables y también cómo usar una variable para pasar el valor de una función.  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>Especificar nombres de parámetro  
 Al crear un procedimiento y declarar un nombre de parámetro, dicho nombre debe comenzar con un único carácter @ y debe ser único en el ámbito del procedimiento.  
  
 La asignación de nombres de forma explícita a los parámetros y la asignación de los valores adecuados para cada uno en una llamada a procedimiento permite proporcionar los parámetros en cualquier orden. Por ejemplo, si el procedimiento **my_proc** espera tres parámetros llamados **@first**, **@second**y **@third**, los valores pasados al procedimiento pueden asignarse a los nombres de los parámetros; por ejemplo: `EXECUTE my_proc @second = 2, @first = 1, @third = 3;`  
  
> [!NOTE]  
>  Si un valor de parámetro se proporciona con el formato **@parameter =***valor*, todos los parámetros posteriores se deben proporcionar de esta manera. Si los valores de parámetro no se pasan con el formato **@parameter =***valor*, los valores se deben proporcionar en el orden idéntico (de izquierda a derecha) en el que los parámetros se enumeran en la instrucción CREATE PROCEDURE.  
  
> [!WARNING]  
>  Cualquier parámetro pasado con el formato **@parameter =***valor* con el parámetro mal escrito, provocará que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un error e impida la ejecución del procedimiento.  
  
## <a name="specifying-parameter-data-types"></a>Especificar los tipos de datos de parámetro  
 Los parámetros se deben definir con un tipo de datos cuando se declaran en una instrucción CREATE PROCEDURE. El tipo de datos de un parámetro determina el tipo y el rango de valores que se aceptan para él cuando se llama al procedimiento. Por ejemplo, si define un parámetro con un tipo de datos **tinyint** , solo se aceptan valores numéricos del intervalo comprendido entre 0 y 255 cuando se pasan en dicho parámetro. Se devuelve un error si, para ejecutar un procedimiento, se usa un valor incompatible con el tipo de datos.  
  
## <a name="specifying-parameter-default-values"></a>Especificar valores predeterminados de parámetro  
 Un parámetro se considera opcional si tiene un valor predeterminado especificado cuando se declara. No es necesario proporcionar un valor para un parámetro opcional de una llamada a procedimiento.  
  
 El valor predeterminado de un parámetro se usa cuando:  
  
-   No existe ningún valor especificado en la llama a procedimiento.  
  
-   Se especifica la palabra clave DEFAULT como valor en la llamada a procedimiento.  
  
> [!NOTE]  
>  Si el valor predeterminado es una cadena de caracteres con signos de puntuación o espacios en blanco incrustados, o bien si empieza por un número (por ejemplo, 6xxx), deberá estar delimitado por comillas simples y rectas.  
  
 Si no se puede especificar ningún valor correctamente como predeterminado para el parámetro, especifique NULL como el valor predeterminado. Es aconsejable que el procedimiento devuelva un mensaje personalizado si el procedimiento se ejecuta sin un valor para el parámetro.  
  
 En el ejemplo siguiente se crea el procedimiento `uspGetSalesYTD` con un parámetro de entrada, `@SalesPerson`. Se asigna NULL como valor predeterminado para el parámetro y se usa en las instrucciones de control de errores para devolver un mensaje de error personalizado en los casos en que se ejecute el procedimiento sin que el parámetro `@SalesPerson` tenga un valor.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 En el ejemplo siguiente se ejecuta el procedimiento. La primera instrucción ejecuta el procedimiento sin especificar ningún valor de entrada. Esto hace que las instrucciones de control de errores del procedimiento devuelvan el mensaje de error personalizado. La segunda instrucción proporciona un valor de entrada y devuelve el conjunto de resultados esperado.  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.uspGetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.uspGetSalesYTD N'Blythe';  
GO  
```  
  
 Aunque los parámetros para los que se hayan especificado valores predeterminados se pueden omitir, solo se puede truncar la lista de parámetros. Por ejemplo, si un procedimiento tiene cinco parámetros, los parámetros cuarto y quinto se pueden omitir. Sin embargo, el cuarto parámetro no puede omitirse cuando se incluye el quinto parámetro, a menos que los parámetros se proporcionen con el formato **@parameter =***valor*.  
  
## <a name="specifying-parameter-direction"></a>Especificar la dirección de parámetro  
 La dirección de un parámetro es de entrada, el valor se pasa al cuerpo del procedimiento, o de salida, el procedimiento devuelve un valor al programa de llamada. El valor predeterminado es un parámetro de entrada.  
  
 Para especificar un parámetro de salida, se debe indicar la palabra clave OUTPUT en la definición del parámetro en la instrucción CREATE PROCEDURE. El procedimiento devuelve el valor actual del parámetro de salida al programa de llamada cuando se abandona el procedimiento. El programa de llamada también debe usar la palabra clave OUTPUT al ejecutar el procedimiento, a fin de guardar el valor del parámetro en una variable que se pueda usar en el programa de llamada.  
  
 En el siguiente ejemplo se crea el procedimiento `Production.usp_GetList`, que devuelve una lista de productos con precios que no superan un importe especificado. El ejemplo muestra la utilización de varias instrucciones SELECT y varios parámetros OUTPUT. Los parámetros OUTPUT permiten a un procedimiento externo, un proceso por lotes o más de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] tener acceso a un conjunto de valores durante la ejecución del procedimiento.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 Ejecute `usp_GetList` para obtener una lista de los productos de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] (Bicicletas) que cuestan menos de 700 USD. Los parámetros OUTPUT **@cost** y **@compareprices** se usan con el lenguaje de control de flujo para devolver un mensaje en la ventana **Messages** .  
  
> [!NOTE]  
>  La variable OUTPUT debe definirse durante la creación del procedimiento y también durante el uso de la variable. El nombre del parámetro y de la variable no tienen por qué coincidir. Pero el tipo de datos y la posición de los parámetros deben coincidir (a menos que se use **@listprice=** *variable*).  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 Éste es el conjunto de resultados parciales:  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  

