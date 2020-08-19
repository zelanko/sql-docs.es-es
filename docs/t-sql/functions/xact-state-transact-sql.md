---
description: XACT_STATE (Transact-SQL)
title: XACT_STATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e871be5e42ff16f16b5f13152cc20fd18bb8dbcb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422549"
---
# <a name="xact_state-transact-sql"></a>XACT_STATE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Función escalar que notifica el estado de la transacción de usuario de una solicitud que se está ejecutando actualmente. XACT_STATE indica si la solicitud tiene una transacción de usuario activa y si se puede confirmar la transacción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql  
XACT_STATE()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>Tipo de valor devuelto  
 **smallint**  
  
## <a name="remarks"></a>Observaciones  
 XACT_STATE devuelve los siguientes valores.  
  
|Valor devuelto|Significado|  
|------------------|-------------|  
|1|La solicitud actual tiene una transacción de usuario activa. La solicitud puede realizar cualquier acción, incluida la escritura de datos y la confirmación de la transacción.|  
|0|No hay ninguna transacción de usuario activa para la solicitud actual.|  
|-1|La solicitud actual tiene una transacción de usuario activa, pero se ha producido un error por el cual la transacción se clasificó como no confirmable. La solicitud no puede confirmar la transacción o revertirla a un punto de retorno; solo puede solicitar que la transacción se revierta completamente. Tampoco puede realizar operaciones de escritura hasta que se revierta la transacción. Mientras tanto, solo puede realizar operaciones de lectura. Una vez que la transacción se ha revertido, la solicitud puede realizar operaciones de lectura y escritura, y puede iniciar transacciones nuevas.<br /><br /> Cuando finalice la ejecución del lote más exterior, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] revertirá automáticamente todas las transacciones no confirmables activas. Si no se envió ningún mensaje de error cuando la transacción entró en un estado no confirmable, cuando finalice la ejecución del lote se enviará un mensaje de error a la aplicación cliente. Este mensaje indica que se detectó y revirtió una transacción no confirmable.|  
  
 Las funciones XACT_STATE y @@TRANCOUNT pueden usarse para detectar si la solicitud actual tiene o no una transacción de usuario activa. No se puede usar @@TRANCOUNT para determinar si esa transacción se ha clasificado como no confirmable. No se puede utilizar XACT_STATE para determinar si hay transacciones anidadas.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `XACT_STATE` en el bloque `CATCH` de una construcción `TRY...CATCH` para determinar si se debe confirmar o revertir una transacción. Como `SET XACT_ABORT` está en el estado `ON`, el error de infracción de restricción hace que la transacción pase a un estado no  confirmable.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
