---
title: Devolver datos de un procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4f9ee8851ce00c429ba277dd6e0be3286284f548
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "74307984"
---
# <a name="return-data-from-a-stored-procedure"></a>Devolver datos de un procedimiento almacenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Existen tres formas de devolver datos de un procedimiento a un programa de llamada: conjuntos de resultados, parámetros de salida y códigos de retorno. En este tema se proporciona información sobre los tres enfoques.  
  
## <a name="returning-data-using-result-sets"></a>Devolución de datos con conjuntos de resultados
Si incluye una instrucción SELECT en el cuerpo de un procedimiento almacenado (pero que no sea SELECT ... INTO ni INSERT ... SELECT), las filas especificadas en la instrucción SELECT se enviarán directamente al cliente.  En el caso de conjuntos de resultados grandes, la ejecución del procedimiento almacenado no continuará a la siguiente instrucción hasta que el conjunto de resultados se haya enviado completamente al cliente.  En cuanto a los conjuntos de resultados pequeños, los resultados se pondrán en cola para su devolución al cliente y la ejecución continuará.  Si se ejecutan varias instrucciones SELECT durante la ejecución del procedimiento almacenado, se enviarán varios conjuntos de resultados al cliente.  Este comportamiento también se aplica a los lotes de TSQL anidados, los procedimientos almacenados anidados y los lotes de TSQL de nivel superior.
 
 
 ### <a name="examples-of-returning-data-using-a-result-set"></a>Ejemplos de devolución de datos con un conjunto de resultados 
  En el ejemplo siguiente se muestra un procedimiento almacenado que devuelve los valores LastName y SalesYTD para todas las filas SalesPerson que también aparecen en la vista vEmployee.
  
 ```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
AS    
  
    SET NOCOUNT ON;  
    SELECT LastName, SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    
RETURN  
GO  
  
```  

  
## <a name="returning-data-using-an-output-parameter"></a>Devolver datos mediante un parámetro de salida  
 Si especifica la palabra clave OUTPUT para un parámetro en la definición del procedimiento, este, al salir, podrá devolver el valor actual del parámetro al programa de llamada. Para guardar el valor del parámetro en una variable que pueda usarse en el programa de llamada, este último debe usar la palabra clave OUTPUT para ejecutar el procedimiento. Para obtener más información sobre los tipos de datos se pueden usar como parámetros de salida, vea [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
### <a name="examples-of-output-parameter"></a>Ejemplos de parámetros de salida  
 En el ejemplo siguiente se muestra un procedimiento con un parámetro de entrada y otro de salida. El parámetro `@SalesPerson` recibirá un valor de entrada especificado por el programa de llamada. La instrucción SELECT usa el último valor del parámetro de entrada para obtener el valor de `SalesYTD` correcto. La instrucción SELECT también asigna el valor al parámetro de salida `@SalesYTD` , que devuelve el valor al programa de llamada cuando finaliza el procedimiento.  
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 El ejemplo siguiente se llama al procedimiento creado en el primer ejemplo y guarda el valor de salida devuelto desde el procedimiento llamado en la variable `@SalesYTD` , que es local para el programa de llamada.  
  
```sql
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 También es posible especificar los valores de entrada para los parámetros OUTPUT cuando se ejecuta el procedimiento. Esto permite al procedimiento recibir un valor del programa de llamada, cambiarlo o realizar operaciones con él y, a continuación, devolver el nuevo valor al programa de llamada. En el ejemplo anterior, es posible asignar un valor a la variable `@SalesYTDBySalesPerson` antes de que el programa llame al procedimiento `Sales.uspGetEmployeeSalesYTD` . La instrucción de ejecución pasaría el valor de la variable `@SalesYTDBySalesPerson` en el parámetro OUTPUT `@SalesYTD` . Posteriormente, en el cuerpo del procedimiento, el valor se podría usar para realizar cálculos que generen un valor nuevo. El nuevo valor se devolvería al procedimiento mediante el parámetro OUTPUT, actualizando el valor de la variable `@SalesYTDBySalesPerson` cuando finaliza el procedimiento. A esto se le suele denominar "capacidad de paso por referencia".  
  
 Si especifica OUTPUT para un parámetro cuando llama a un procedimiento y dicho parámetro no está definido mediante OUTPUT en la definición del procedimiento, se emite un mensaje de error. No obstante, puede ejecutar un procedimiento con parámetros de salida y no especificar OUTPUT al ejecutar el procedimiento. No se devuelve ningún error, pero no podrá utilizar el valor de salida en el programa que realiza la llamada.  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>Usar el tipo de datos de cursor en parámetros OUTPUT  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] los procedimientos solo pueden usar el tipo de datos **cursor** para los parámetros OUTPUT. Si se especifica el tipo de datos **cursor** para un parámetro, deben especificarse las palabras clave VARYING y OUTPUT para ese parámetro en la definición del procedimiento. Un parámetro solo se puede especificar como OUTPUT, pero si se especifica la palabra clave VARYING en la declaración del parámetro, el tipo de datos debe ser **cursor** y también se debe especificar la palabra clave OUTPUT.  
  
> [!NOTE]  
>  El tipo de datos **cursor** no se puede enlazar a variables de aplicación a través de las API de bases de datos tales como OLE DB, ODBC, ADO y DB-Library. Debido a que los parámetros OUTPUT deben estar enlazados antes de que una aplicación pueda ejecutar un procedimiento, dichos procedimientos con parámetros **cursor** OUTPUT no pueden llamarse desde las API de bases de datos. Estos procedimientos solo pueden llamarse desde procesos por lotes, procedimientos o desencadenadores [!INCLUDE[tsql](../../includes/tsql-md.md)] cuando la variable **cursor** OUTPUT esté asignada a una variable [!INCLUDE[tsql](../../includes/tsql-md.md)] cursor **local de** .  
  
### <a name="rules-for-cursor-output-parameters"></a>Reglas para parámetros de salida de cursor  
 Las siguientes reglas se aplican a los parámetros **cursor** OUTPUT cuando se ejecuta el procedimiento:  
  
-   Para un cursor de solo avance, las filas devueltas en el conjunto de resultados del cursor son solo aquellas filas que estén en la posición del cursor y hacia delante al concluir la ejecución del procedimiento, por ejemplo:  
  
    -   En un procedimiento de un conjunto de resultados llamado RS de 100 filas, se abre un cursor no desplazable.  
  
    -   El procedimiento captura las primeras 5 filas del conjunto de resultados RS.  
  
    -   El procedimiento vuelve a quien le llamó.  
  
    -   El conjunto de resultados que RS devolvió a quien llamó está formado por las filas 6 a 100 de RS; el cursor del que llama se coloca antes de la primera fila de RS.  
  
-   Para un cursor de solo avance, si el cursor se coloca antes de la primera fila cuando finalice el procedimiento, el conjunto de resultados completo se devuelve al proceso por lotes, procedimiento o desencadenador de llamada. Cuando se devuelve, la posición del cursor se establece antes de la primera fila.  
  
-   Para un cursor de solo avance, si el cursor se coloca después del final de la última fila cuando finaliza el procedimiento almacenado, se devolverá un conjunto de resultados vacío al proceso por lotes, procedimiento o desencadenador de llamada.  
  
    > [!NOTE]  
    >  Un conjunto de resultados vacío no es lo mismo que un valor NULL.  
  
-   Para un cursor desplazable, todas las filas del conjunto de resultados se devuelven al proceso por lotes, procedimiento o desencadenador de llamada cuando finaliza el procedimiento. Cuando se devuelve, la posición del cursor se deja en la posición de la última captura ejecutada en el procedimiento.  
  
-   Para cualquier tipo de cursor, si se ha cerrado el cursor, se devuelve un valor NULL al proceso por lotes, procedimiento o desencadenador de llamada. Esto también ocurrirá si se ha asignado un cursor a un parámetro, pero ese cursor nunca se abre.  
  
    > [!NOTE]  
    >  El estado cerrado solo tiene importancia en el momento del retorno. Por ejemplo, es válido cerrar un cursor a mitad del procedimiento, volver a abrirlo posteriormente en el procedimiento y devolver el conjunto de resultados de ese cursor al proceso por lotes, procedimiento o desencadenador de llamada.  
  
### <a name="examples-of-cursor-output-parameters"></a>Ejemplos de parámetros de salida de cursor  
 En el siguiente ejemplo, se crea un procedimiento que especifica un parámetro de salida (`@currency_cursor`) con el tipo de datos **cursor**. A continuación, se llama al procedimiento desde un lote.  
 
 Primero, crea el procedimiento de declaración y, luego, abre un cursor en la tabla Currency.  
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 A continuación, se ejecuta un proceso por lotes que declara una variable cursor local, ejecuta el procedimiento para asignar el cursor a la variable local y, por último, captura las filas desde el cursor.  
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>Devolver datos con un código de retorno  
 Un procedimiento puede devolver un valor entero, denominado código de retorno, para indicar el estado de ejecución de un procedimiento. Se especifica el código de retorno para un procedimiento mediante la instrucción RETURN. Al igual que con los parámetros OUTPUT, debe guardar el código de retorno en una variable cuando se ejecute el procedimiento a fin de usar su valor en el programa de llamada. Por ejemplo, la variable de asignación `@result` del tipo de datos **int** se usa para almacenar el código de retorno del procedimiento `my_proc`, como:  
  
```sql
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 Los códigos de retorno suelen usarse en los bloques de control de flujo dentro de los procedimientos con el fin de establecer el valor del código de retorno para cada posible situación de error. Puede usar la función @@ERROR después de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] para detectar si se produjo un error durante la ejecución de la instrucción.  Antes de la introducción del control de errores TRY/CATCH/THROW en TSQL, a veces los códigos de devolución eran necesarios para determinar la correcta ejecución o los errores de los procedimientos almacenados.  Los procedimientos almacenados deben indicar siempre cualquier problema con un error (generado con THROW/RAISERROR en caso necesario) y no depender de un código de devolución para hacerlo.  También conviene evitar el uso del código de devolución para devolver datos de la aplicación.
  
### <a name="examples-of-return-codes"></a>Ejemplos de códigos de retorno  
 El ejemplo siguiente muestra el procedimiento `usp_GetSalesYTD` con control de errores que establece valores del código de retorno especiales para varios errores. La tabla siguiente muestra el valor entero que asigna el procedimiento a cada error posible y el significado correspondiente de cada valor.  
  
|Valor de código de retorno|Significado|  
|-----------------------|-------------|  
|0|Ejecución correcta.|  
|1|No se ha especificado el valor del parámetro requerido.|  
|2|El valor del parámetro especificado no es válido.|  
|3|Se ha producido un error al obtener el valor de venta.|  
|4|Valor de venta NULL encontrado para el vendedor.|  
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 El ejemplo siguiente crea un programa para controlar los códigos de retorno devueltos desde el procedimiento `usp_GetSalesYTD` .  
  
```sql
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'ERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
