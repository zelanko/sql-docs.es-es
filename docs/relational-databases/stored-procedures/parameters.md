---
title: "Parámetros | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- user-defined functions [SQL Server], parameters
ms.assetid: c1f9bd93-3271-4098-a23b-7bd7a19ab65b
caps.latest.revision: 2
author: pmasl
ms.author: pelopes
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 64617ddd4922e7217ac905e92e5d9dfd6ffff7e4
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="parameters"></a>Parámetros
Los parámetros se usan para intercambiar datos entre las funciones y los procedimientos almacenados y la aplicación o la herramienta que llamó a la función o al procedimiento almacenados: 

*  Los parámetros de entrada permiten a quien realiza la llamada pasar un valor de datos a la función o al procedimiento almacenado.
*  Los parámetros de salida permiten al procedimiento almacenado devolver un valor de datos o variable de cursor a quien realizó la llamada. Las funciones definidas por el usuario no pueden especificar parámetros de salida.
*  Cada procedimiento almacenado devuelve un código de retorno de tipo entero a quien realiza la llamada. Si el procedimiento almacenado no establece explícitamente un valor para el código de retorno, éste es 0.

En el siguiente procedimiento almacenado de ejemplo se muestra el uso de un parámetro de entrada, un parámetro de salida y un código de retorno:
```
-- Create a procedure that takes one input parameter and returns one output parameter and a return code.
CREATE PROCEDURE SampleProcedure @EmployeeIDParm INT,
         @MaxTotal INT OUTPUT
AS
-- Declare and initialize a variable to hold @@ERROR.
DECLARE @ErrorSave INT
SET @ErrorSave = 0

-- Do a SELECT using the input parameter.
SELECT FirstName, LastName, JobTitle
FROM HumanResources.vEmployee
WHERE EmployeeID = @EmployeeIDParm

-- Save any nonzero @@ERROR value.
IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Set a value in the output parameter.
SELECT @MaxTotal = MAX(TotalDue)
FROM Sales.SalesOrderHeader;

IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Returns 0 if neither SELECT statement had an error; otherwise, returns the last error.
RETURN @ErrorSave
GO
```

Cuando se ejecuta una función o un procedimiento almacenado, los parámetros de entrada pueden tener establecido su valor a una constante o usar el valor de una variable. Los parámetros de salida y los códigos de retorno deben devolver sus valores en una variable. Los parámetros y los códigos de retorno pueden intercambiar valores de datos con las variables de Transact-SQL o con variables de aplicación.

Si se llama a un procedimiento almacenado desde un lote o un script, los valores de los parámetros y del código de retorno pueden usar las variables de Transact-SQL definidas en el mismo lote. En el siguiente ejemplo se muestra un lote en el que se ejecuta el procedimiento creado anteriormente. El parámetro de entrada se especifica como una constante, y el parámetro de salida y el código de retorno colocan sus valores en variables de Transact-SQL:
```
-- Declare the variables for the return code and output parameter.
DECLARE @ReturnCode INT
DECLARE @MaxTotalVariable INT

-- Execute the stored procedure and specify which variables
-- are to receive the output parameter and return code values.
EXEC @ReturnCode = SampleProcedure @EmployeeIDParm = 19,
   @MaxTotal = @MaxTotalVariable OUTPUT

-- Show the values returned.
PRINT ' '
PRINT 'Return code = ' + CAST(@ReturnCode AS CHAR(10))
PRINT 'Maximum Quantity = ' + CAST(@MaxTotalVariable AS CHAR(10))
GO
```

Una aplicación puede usar marcadores de parámetro enlazados a variables de programa para intercambiar datos entre variables de aplicación, parámetros y códigos de retorno.

## <a name="see-also"></a>Vea también
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [Sección Parámetros y reutilización de un plan de ejecución](../../relational-databases/query-processing-architecture-guide.md)   
 [Variables (Transact-SQL)](../../t-sql/language-elements/variables-transact-sql.md)
