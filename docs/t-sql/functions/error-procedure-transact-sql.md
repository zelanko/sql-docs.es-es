---
title: ERROR_PROCEDURE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
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
- ERROR_PROCEDURE_TSQL
- ERROR_PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_PROCEDURE function
- messages [SQL Server], trigger where occurred
- errors [SQL Server], stored procedure where occurred
- TRY...CATCH [SQL Server]
- CATCH block
- messages [SQL Server], stored procedure where occurred
- errors [SQL Server], trigger where occurred
ms.assetid: b81edbf0-856a-498f-ba87-48ff1426d980
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e13d4201a9381ca80a700fdb04fc69cf1044b664
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="errorprocedure-transact-sql"></a>ERROR_PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el nombre del procedimiento almacenado o del desencadenador en el que se ha producido un error que ha causado la ejecución de un bloque CATCH de una construcción TRY…CATCH.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ERROR_PROCEDURE ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar (128)**  
  
## <a name="return-value"></a>Valor devuelto  
 Cuando se llama en un bloque CATCH, devuelve el nombre del procedimiento almacenado en el que se ha producido el error.  
  
 Devuelve NULL si el error no se ha producido en un procedimiento almacenado o un desencadenador.  
  
 Devuelve NULL si se le llama desde fuera del ámbito del bloque CATCH.  
  
## <a name="remarks"></a>Comentarios  
 ERROR_PROCEDURE se puede llamar en cualquier lugar dentro del ámbito de un bloque CATCH.  
  
 ERROR_PROCEDURE devuelve el nombre del procedimiento almacenado o desencadenador en el que se ha producido el error, independientemente del número de veces que se llame o del lugar desde el que se haga dentro del ámbito del bloque CATCH. Esto contrasta con las funciones, como@ERROR, que devuelve el número de error en la instrucción inmediatamente posterior a la que produjo el error o en la primera instrucción del bloque CATCH.  
  
 En los bloques CATCH anidados, ERROR_PROCEDURE devuelve el nombre del procedimiento almacenado o el desencadenador específico del ámbito del bloque CATCH en el que se hace referencia a él. Por ejemplo, el bloque CATCH de una construcción TRY…CATCH podría tener una TRY…CATCH anidada. En el bloque CATCH anidado, ERROR_PROCEDURE devuelve el nombre del procedimiento almacenado o el desencadenador en el que se ha producido el error y que ha llamado al bloque CATCH anidado. Si ERROR_PROCEDURE se ejecuta en el bloque CATCH externo, devuelve el nombre del procedimiento almacenado o el desencadenador en el que se ha producido el error y que ha llamado al bloque CATCH.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-errorprocedure-in-a-catch-block"></a>A. Utilizar ERROR_PROCEDURE en un bloque CATCH  
 En el siguiente ejemplo de código se muestra un procedimiento almacenado que genera un error de división por cero. `ERROR_PROCEDURE` devuelve el nombre del procedimiento almacenado en el que se produce el error.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>B. Utilizar ERROR_PROCEDURE en un bloque CATCH con otras herramientas de control de errores  
 En el siguiente ejemplo de código se muestra un procedimiento almacenado que genera un error de división por cero. Junto al nombre del procedimiento almacenado en el que se ha producido el error, se devuelve información relacionada con dicho error.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage,  
        ERROR_LINE() AS ErrorLine;  
        END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorprocedure-in-a-catch-block"></a>C. Utilizar ERROR_PROCEDURE en un bloque CATCH  
 En el siguiente ejemplo de código se muestra un procedimiento almacenado que genera un error de división por cero. `ERROR_PROCEDURE` devuelve el nombre del procedimiento almacenado en el que se produce el error.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>D. Utilizar ERROR_PROCEDURE en un bloque CATCH con otras herramientas de control de errores  
 En el siguiente ejemplo de código se muestra un procedimiento almacenado que genera un error de división por cero. Junto al nombre del procedimiento almacenado en el que se ha producido el error, se devuelve información relacionada con dicho error.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage;  
        END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

