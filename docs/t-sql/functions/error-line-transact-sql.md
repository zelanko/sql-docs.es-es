---
title: ERROR_LINE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ce725d492c0f777f27198a3c686de7a80307e2ee
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "80216216"
---
# <a name="error_line-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve el número de línea de la repetición de un error que provocó la ejecución del bloque CATCH de una construcción TRY…CATCH.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>Tipo de valor devuelto  
**int**  
  
## <a name="return-value"></a>Valor devuelto  
Cuando se llama en un bloque CATCH, `ERROR_LINE` devuelve  
  
-   el número de línea donde se produjo el error.    
-   el número de línea de una rutina, si el error se produjo en un procedimiento almacenado o desencadenador.  
-   NULL, si se llamó desde fuera del ámbito del bloque CATCH.  
  
## <a name="remarks"></a>Observaciones  
Una llamada a `ERROR_LINE` se puede producir en cualquier lugar del ámbito de un bloque CATCH.  
  
`ERROR_LINE` devuelve el número de línea en que se produjo el error. Esto ocurre independientemente de la ubicación de la llamada a `ERROR_LINE` dentro del ámbito del bloque CATCH y del número de llamadas a `ERROR_LINE`. Esto contrasta con las funciones, como @@ERROR. @@ERROR devuelve el número de error en la instrucción inmediatamente posterior a la que produjo el error o en la primera instrucción de un bloque CATCH.  
  
En los bloques CATCH anidados, `ERROR_LINE` devuelve el número de línea del error específico del ámbito del bloque CATCH en el que se hace referencia al mismo. Por ejemplo, el bloque CATCH de una construcción TRY...CATCH podría contener una construcción TRY...CATCH anidada. Dentro del bloque CATCH anidado, `ERROR_LINE` devuelve el número de línea del error que invocó el bloque CATCH anidado. Si `ERROR_LINE` se ejecuta en el bloque CATCH externo, devuelve el número de línea del error que invocó ese bloque CATCH específico.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-error_line-in-a-catch-block"></a>A. Utilizar ERROR_LINE en un bloque CATCH  
En este ejemplo de código se muestra una instrucción `SELECT` que genera un error de división por cero. `ERROR_LINE` devuelve el número de línea donde se produjo el error.  
  
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
  
### <a name="b-using-error_line-in-a-catch-block-with-a-stored-procedure"></a>B. Utilizar ERROR_LINE en un bloque CATCH con un procedimiento almacenado  
En este ejemplo se muestra un procedimiento almacenado que genera un error de división por cero. `ERROR_LINE` devuelve el número de línea donde se produjo el error.  
  
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


### <a name="c-using-error_line-in-a-catch-block-with-other-error-handling-tools"></a>C. Utilizar ERROR_LINE en un bloque CATCH con otras herramientas de control de errores  
En este ejemplo de código se muestra una instrucción `SELECT` que genera un error de división por cero. `ERROR_LINE` devuelve el número de línea donde se produjo el error y la información relacionada con el error propiamente dicho.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
