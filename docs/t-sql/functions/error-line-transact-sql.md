---
title: ERROR_LINE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 83783fdaa950777ae0a8002182abc273e32c2ca0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="errorline-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el número de línea en que se produjo un error que provocó la ejecución del bloque CATCH de una construcción TRY…CATCH.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 **int**  
  
## <a name="return-value"></a>Valor devuelto  
 Cuando se llama en un bloque CATCH:  
  
-   Devuelve el número de línea en que se produjo el error.  
  
-   Devuelve el número de línea de una rutina si el error se produjo en un procedimiento almacenado o desencadenador.  
  
 Devuelve NULL si se le llama desde fuera del ámbito del bloque CATCH.  
  
## <a name="remarks"></a>Notas  
 Esta función se puede llamar desde cualquier lugar dentro del ámbito de un bloque CATCH.  
  
 ERROR_LINE devuelve el número de línea en que se produjo el error, independientemente de las veces que se llame o desde dónde se llame en el ámbito del bloque CATCH. En cambio, las funciones como @@ERROR solo devuelven el número de error en la instrucción inmediatamente posterior a la que produjo el error o en la primera instrucción de un bloque CATCH.  
  
 En los bloques CATCH anidados, ERROR_LINE devuelve el número de línea del error específico del ámbito del bloque CATCH en el que se hace referencia al mismo. Por ejemplo, el bloque CATCH de una construcción TRY...CATCH podría contener una construcción TRY...CATCH anidada. Dentro del bloque CATCH anidado, ERROR_LINE devuelve el número de línea del error que invocó el bloque CATCH anidado. Si ERROR_LINE se ejecuta en el bloque CATCH externo, devuelve el número de línea del error que invocó ese bloque CATCH.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-errorline-in-a-catch-block"></a>A. Utilizar ERROR_LINE en un bloque CATCH  
 El siguiente ejemplo de código muestra una instrucción `SELECT` que genera un error de división por cero. Se devuelve el número de línea en que se produjo el error.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>B. Utilizar ERROR_LINE en un bloque CATCH con un procedimiento almacenado  
 En el siguiente ejemplo de código se muestra un procedimiento almacenado que generará un error de división por cero. `ERROR_LINE` devuelve el número de línea del procedimiento almacenado en el que se produce el error.  
  
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
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>C. Utilizar ERROR_LINE en un bloque CATCH con otras herramientas de control de errores  
 El siguiente ejemplo de código muestra una instrucción `SELECT` que genera un error de división por cero. Además del número de línea en que se produjo el error, se devuelve información relacionada con el mismo.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
