---
title: '@@ROWCOUNT (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 08/29/2017
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
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411dc7eb628ddff52eb2f9426488e05860c9d279
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40rowcount-transact-sql"></a>& #x 40; & #x 40; Recuento de filas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el número de filas afectadas por la última instrucción. Si el número de filas es más de 2 millones, use [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]las instrucciones pueden establecer el valor de @@ROWCOUNT de las maneras siguientes:  
  
-   Set @@ROWCOUNT para el número de filas afectadas o leídas. Las filas pueden o no enviarse al cliente.  
  
-   Conservar@ROWCOUNT desde la ejecución de la instrucción anterior.  
  
-   Restablecer@ROWCOUNT en 0, pero no devuelven el valor al cliente.  
  
 Las instrucciones que realizan una asignación simple siempre establecen el @@ROWCOUNT valor en 1. No se envían filas al cliente. Algunos ejemplos de estas instrucciones son: SET @*local_variable*, RETURN, READTEXT y select sin instrucciones de consulta como SELECT GETDATE() o SELECT **'***texto genérico* **'**.  
  
 Las instrucciones que realizan una asignación en una consulta o utilizan RETURN en un conjunto de consultas el @@ROWCOUNT valor para el número de filas afectadas o leídas por la consulta, por ejemplo: SELECT @*local_variable* = c1 FROM t1.  
  
 Conjunto de instrucciones de lenguaje (DML) de manipulación de datos el @@ROWCOUNT valor para el número de filas afectadas por la consulta y devuelve ese valor al cliente. Las instrucciones DML pueden no enviar ninguna fila al cliente.  
  
 DECLARE CURSOR y FETCH establecer el @@ROWCOUNT valor en 1.  
  
 Las instrucciones EXECUTE conservan anterior @@ROWCOUNT.  
  
 Las instrucciones como USE, establezca \<opción >, DEALLOCATE CURSOR, CLOSE CURSOR, BEGIN TRANSACTION o COMMIT TRANSACTION restablece el valor de ROWCOUNT en 0.  
  
 Los procedimientos almacenados compilados de forma nativa conservar anterior @@ROWCOUNT. [!INCLUDE[tsql](../../includes/tsql-md.md)]las instrucciones incluidas en procedimientos almacenados compilados de forma nativa no establecen@ROWCOUNT. Para obtener más información, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se ejecuta una instrucción `UPDATE` y se utiliza `@@ROWCOUNT` para detectar si ha cambiado alguna fila.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SET ROWCOUNT &#40; Transact-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  

