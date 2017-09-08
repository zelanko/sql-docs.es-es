---
title: ERROR_MESSAGE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f15d9d23726f7558f0bf73aff3f8c3c5253cb24d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el texto del mensaje del error que ha provocado la ejecución del bloque CATCH de una construcción TRY…CATCH.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>Valor devuelto  
 Cuando se ha llamado en un bloque CATCH, devuelve el texto completo del mensaje de error que ha provocado la ejecución del bloque CATCH. El texto incluye los valores proporcionados para los parámetros sustituibles, como las longitudes, nombres de objeto o tiempos.  
  
 Devuelve NULL si se le llama desde fuera del ámbito del bloque CATCH.  
  
## <a name="remarks"></a>Comentarios  
 Puede llamarse a ERROR_MESSAGE desde cualquier lugar del ámbito de un bloque CATCH.  
  
 ERROR_MESSAGE devuelve el mensaje de error con independencia de cuántas veces se haya ejecutado, o en qué parte del ámbito del bloque CATCH se ejecute. Esto difiere de las funciones como @@ERROR, que sólo devuelve un número de error en la instrucción inmediatamente posterior a la que se produzca un error o bloquear la primera instrucción de un bloque CATCH.  
  
 En bloques CATCH anidados, ERROR_MESSAGE devuelve el mensaje de error específico del ámbito del bloque CATCH en el que se hace referencia a él. Por ejemplo, el bloque CATCH de una construcción TRY...CATCH externa podría tener una construcción TRY...CATCH anidada. En el bloque CATCH anidado, ERROR_MESSAGE devuelve el mensaje del error que ha invocado el bloque CATCH anidado. Si se ejecuta ERROR_MESSAGE en el bloque CATCH externo, devuelve el mensaje del error que ha invocado el bloque CATCH.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. Usar ERROR_MESSAGE en un bloque CATCH  
 El siguiente ejemplo de código muestra una instrucción `SELECT` que genera un error de división por cero. Se devuelve el mensaje de error.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>B. Usar ERROR_MESSAGE en un bloque CATCH con otras herramientas de control de errores.  
 El siguiente ejemplo de código muestra una instrucción `SELECT` que genera un error de división por cero. Además del mensaje de error, se devuelve información relacionada con el error.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errormessage-in-a-catch-block"></a>C. Usar ERROR_MESSAGE en un bloque CATCH  
 El siguiente ejemplo de código muestra una instrucción `SELECT` que genera un error de división por cero. Se devuelve el mensaje de error.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>D. Usar ERROR_MESSAGE en un bloque CATCH con otras herramientas de control de errores.  
 El siguiente ejemplo de código muestra una instrucción `SELECT` que genera un error de división por cero. Además del mensaje de error, se devuelve información relacionada con el error.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


