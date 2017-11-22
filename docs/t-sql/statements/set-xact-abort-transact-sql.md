---
title: SET XACT_ABORT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server 2016 Preview
f1_keywords:
- XACT_ABORT_TSQL
- XACT_ABORT
- SET XACT_ABORT
- SET_XACT_ABORT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- XACT_ABORT option
- automatic transaction roll backs
- transactions [SQL Server], rolling back
- rolling back transactions, SET XACT_ABORT
- roll back transactions [SQL Server]
- SET XACT_ABORT statement
ms.assetid: cbcaa433-58f2-4dc3-a077-27273bef65b5
caps.latest.revision: "50"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c12ab84986210f559fe5d3b1a8842b70a885108e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="set-xactabort-transact-sql"></a>SET XACT_ABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

    
> [!NOTE]  
>  El **THROW** instrucción respeta **establecer XACT_ABORT RAISERROR** no lo hace. Las aplicaciones nuevas deben utilizar **THROW** en lugar de **RAISERROR**.  
  
 Especifica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revierte automáticamente la transacción actual cuando una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] genera un error en tiempo de ejecución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET XACT_ABORT { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET XACT_ABORT ON   
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando SET XACT_ABORT es ON, si una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] genera un error en tiempo de ejecución, se termina toda la transacción y se revierte.  
  
 Cuando SET XACT_ABORT es OFF, en algunos casos solo se revierte la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que generó el error y la transacción continúa procesándose. Dependiendo de la gravedad del error, se puede revertir toda la transacción aun cuando SET XACT_ABORT sea OFF. OFF es el valor predeterminado.  
  
 Los errores de compilación, como los de sintaxis, no se ven afectados por SET XACT_ABORT.  
  
 XACT_ABORT debe estar establecida en ON para las instrucciones de modificación de datos en una transacción implícita o explícita para la mayoría de proveedores OLE DB, incluyendo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El único caso donde no se requiere esta opción es si el proveedor acepta transacciones anidadas.  
  
 Cuando ANSI_WARNINGS=OFF, las infracciones de los permisos hacen que se anulen las transacciones.  
  
 La opción SET XACT_ABORT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @XACT_ABORT VARCHAR(3) = 'OFF';  
IF ( (16384 & @@OPTIONS) = 16384 ) SET @XACT_ABORT = 'ON';  
SELECT @XACT_ABORT AS XACT_ABORT;  
  
```  
  
## <a name="examples"></a>Ejemplos  
 El siguiente código de ejemplo genera un error de infracción de clave externa en una transacción que tiene otras instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. En el primer conjunto de instrucciones se genera el error, pero las demás instrucciones se ejecutan correctamente y la transacción se confirma también correctamente. En el segundo conjunto de instrucciones, `SET XACT_ABORT` se establece en `ON`. Esto hace que el error en la instrucción suspenda el lote y revierta la transacción.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't2', N'U') IS NOT NULL  
    DROP TABLE t2;  
GO  
IF OBJECT_ID(N't1', N'U') IS NOT NULL  
    DROP TABLE t1;  
GO  
CREATE TABLE t1  
    (a INT NOT NULL PRIMARY KEY);  
CREATE TABLE t2  
    (a INT NOT NULL REFERENCES t1(a));  
GO  
INSERT INTO t1 VALUES (1);  
INSERT INTO t1 VALUES (3);  
INSERT INTO t1 VALUES (4);  
INSERT INTO t1 VALUES (6);  
GO  
SET XACT_ABORT OFF;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (1);  
INSERT INTO t2 VALUES (2); -- Foreign key error.  
INSERT INTO t2 VALUES (3);  
COMMIT TRANSACTION;  
GO  
SET XACT_ABORT ON;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (4);  
INSERT INTO t2 VALUES (5); -- Foreign key error.  
INSERT INTO t2 VALUES (6);  
COMMIT TRANSACTION;  
GO  
-- SELECT shows only keys 1 and 3 added.   
-- Key 2 insert failed and was rolled back, but  
-- XACT_ABORT was OFF and rest of transaction  
-- succeeded.  
-- Key 5 insert error with XACT_ABORT ON caused  
-- all of the second transaction to roll back.  
SELECT *  
    FROM t2;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [THROW &#40; Transact-SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
