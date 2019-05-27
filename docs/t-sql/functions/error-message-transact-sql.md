---
title: ERROR_MESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 060c6baeca58e2952e1cebeae95b6d969e484947
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948854"
---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve el texto del mensaje del error que ha provocado la ejecución del bloque CATCH de una construcción TRY…CATCH.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>Valor devuelto  
Cuando se llama en un bloque CATCH, `ERROR_MESSAGE` devuelve el texto completo del mensaje de error que ha provocado la ejecución del bloque `CATCH`. En el texto se incluyen los valores proporcionados para los parámetros sustituibles, como las longitudes, los nombres de objeto o las horas.  
  
`ERROR_MESSAGE` devuelve NULL si se llama desde fuera del ámbito de un bloque CATCH.  
  
## <a name="remarks"></a>Notas  
`ERROR_MESSAGE` admite llamadas en cualquier lugar del ámbito de un bloque CATCH.  
  
`ERROR_MESSAGE` devuelve un mensaje de error relevante, con independencia de cuántas veces se ejecute o de dónde se ejecute dentro del ámbito del bloque `CATCH`. Esto contrasta con funciones como @@ERROR, que solo devuelve un número de error en la instrucción inmediatamente posterior a la que produjo el error.  
  
En los bloques `CATCH` anidados, `ERROR_MESSAGE` devuelve el mensaje de error específico del ámbito del bloque `CATCH` al que hace referencia ese bloque `CATCH`. Por ejemplo, el bloque `CATCH` de una construcción TRY...CATCH externa podría tener una construcción `TRY...CATCH` interna. Dentro de ese bloque interno `CATCH`, `ERROR_MESSAGE` devuelve el mensaje de error que invocó el bloque `CATCH` interno. Si `ERROR_MESSAGE` se ejecuta en el bloque `CATCH` externo, devuelve el mensaje de error que invocó ese bloque `CATCH` externo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. Usar ERROR_MESSAGE en un bloque CATCH  
En este ejemplo se muestra una instrucción `SELECT` que genera un error de división por cero. El bloque `CATCH` devuelve el mensaje de error.  
  
```sql   
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 
```
-----------

(0 row(s) affected)

ErrorMessage
----------------------------------
Divide by zero error encountered.

(1 row(s) affected)

```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>B. Usar ERROR_MESSAGE en un bloque CATCH con otras herramientas de control de errores.  
En este ejemplo se muestra una instrucción `SELECT` que genera un error de división por cero. Junto con el mensaje de error, el bloque `CATCH` devuelve información sobre ese error.  
  
```sql  
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
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 
```
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine  ErrorMessage
----------- ------------- ----------- --------------- ---------- ----------------------------------
8134        16            1           NULL            4          Divide by zero error encountered.

(1 row(s) affected)

```
  
## <a name="see-also"></a>Consulte también  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)     
 [Referencia de errores y eventos &#40;Motor de base de datos&#41;](../../relational-databases/errors-events/errors-and-events-reference-database-engine.md)     
  
    

