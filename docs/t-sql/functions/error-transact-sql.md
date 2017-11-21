---
title: '@@ERROR (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 08/29/2017
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
- '@@ERROR'
- '@@ERROR_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ERROR function'
- errors [SQL Server], Transact-SQL
- error numbers [SQL Server]
ms.assetid: c8b43477-b6c0-49bf-a608-394a0b6cc7a2
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ef3f7b2f0b051fd79dd59325af7900aefff95a9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40error-transact-sql"></a>&#x40;&#x40; ERROR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el número de error de la última instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecutada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@ERROR  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 integer  
  
## <a name="remarks"></a>Comentarios  
 Devuelve 0 si la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] anterior no encontró errores.  
  
 Devuelve un número de error si la instrucción anterior encontró un error. Si el error era uno de los errores en la vista de catálogo sys.messages, a continuación,@ERROR contiene el valor de la columna sys.Messages.message_id Column para dicho error. Puede ver el texto asociado con un @@ERROR número de error en sys.messages.  
  
 Dado que @@ERROR se borra y restablece con cada instrucción ejecutada, comprobarlo inmediatamente después de la instrucción que se está comprueba o guardarlo en una variable local que se pueden comprobar más adelante.  
  
 Use la construcción TRY...CATCH para controlar errores. El bloque TRY... CATCH también crear funciones de sistema adicionales admite (ERROR_LINE, ERROR_MESSAGE, ERROR_PROCEDURE, ERROR_SEVERITY y ERROR_STATE) que devuelven más información de error que @@ERROR . TRY...CATCH también admite una función ERROR_NUMBER que no se limita a devolver el número de error en la instrucción inmediatamente después de la instrucción que generó el error. Para obtener más información, vea [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-error-to-detect-a-specific-error"></a>A. Usar@ERROR para detectar un error específico  
 En el ejemplo siguiente se utiliza `@@ERROR` para comprobar si se infringe una restricción CHECK (error nº 547) en una instrucción `UPDATE`.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.EmployeePayHistory  
    SET PayFrequency = 4  
    WHERE BusinessEntityID = 1;  
IF @@ERROR = 547  
    PRINT N'A check constraint violation occurred.';  
GO  
```  
  
### <a name="b-using-error-to-conditionally-exit-a-procedure"></a>B. Usar@ERROR para salir condicionalmente de un procedimiento  
 En el ejemplo siguiente se utiliza `IF...ELSE` instrucciones para probar `@@ERROR` después de un `INSERT` instrucción en un procedimiento almacenado. El valor de la variable `@@ERROR` determina el código devuelto enviado al programa que llamó, lo que indica si el procedimiento se realizó correcta o incorrectamente.  
  
```  
USE AdventureWorks2012;  
GO  
-- Drop the procedure if it already exists.  
IF OBJECT_ID(N'HumanResources.usp_DeleteCandidate', N'P') IS NOT NULL  
    DROP PROCEDURE HumanResources.usp_DeleteCandidate;  
GO  
-- Create the procedure.  
CREATE PROCEDURE HumanResources.usp_DeleteCandidate   
    (  
    @CandidateID INT  
    )  
AS  
-- Execute the DELETE statement.  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = @CandidateID;  
-- Test the error value.  
IF @@ERROR <> 0   
    BEGIN  
        -- Return 99 to the calling program to indicate failure.  
        PRINT N'An error occurred deleting the candidate information.';  
        RETURN 99;  
    END  
ELSE  
    BEGIN  
        -- Return 0 to the calling program to indicate success.  
        PRINT N'The job candidate has been deleted.';  
        RETURN 0;  
    END;  
GO  
```  
  
### <a name="c-using-error-with-rowcount"></a>C. Usar@ERROR con @@ROWCOUNT   
 En el ejemplo siguiente se utiliza `@@ERROR` con `@@ROWCOUNT` para validar la operación de una instrucción `UPDATE`. Se comprueba el valor de `@@ERROR` para ver si hay un error y se utiliza `@@ROWCOUNT` para asegurarse de que la actualización se aplica correctamente a una fila de la tabla.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Purchasing.usp_ChangePurchaseOrderHeader',N'P')IS NOT NULL  
    DROP PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader;  
GO  
CREATE PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader  
    (  
    @PurchaseOrderID INT  
    ,@BusinessEntityID INT  
   )  
AS  
-- Declare variables used in error checking.  
DECLARE @ErrorVar INT;  
DECLARE @RowCountVar INT;  
  
-- Execute the UPDATE statement.  
UPDATE PurchaseOrderHeader   
    SET BusinessEntityID = @BusinessEntityID   
    WHERE PurchaseOrderID = @PurchaseOrderID;  
  
-- Save the @@ERROR and @@ROWCOUNT values in local   
-- variables before they are cleared.  
SELECT @ErrorVar = @@ERROR  
    ,@RowCountVar = @@ROWCOUNT;  
  
-- Check for errors. If an invalid @BusinessEntityID was specified,  
-- the UPDATE statement returns a foreign key violation error #547.  
IF @ErrorVar <> 0  
    BEGIN  
        IF @ErrorVar = 547  
            BEGIN  
                PRINT N'ERROR: Invalid ID specified for new employee.';  
                 RETURN 1;  
            END  
        ELSE  
            BEGIN  
                PRINT N'ERROR: error '  
                    + RTRIM(CAST(@ErrorVar AS NVARCHAR(10)))  
                    + N' occurred.';  
                RETURN 2;  
            END  
    END  
  
-- Check the row count. @RowCountVar is set to 0   
-- if an invalid @PurchaseOrderID was specified.  
IF @RowCountVar = 0  
    BEGIN  
        PRINT 'Warning: The BusinessEntityID specified is not valid';  
        RETURN 1;  
    END  
ELSE  
    BEGIN  
        PRINT 'Purchase order updated with the new employee';  
        RETURN 0;  
    END;  
GO  
```  

  
## <a name="see-also"></a>Vea también  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [Sys.Messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  


