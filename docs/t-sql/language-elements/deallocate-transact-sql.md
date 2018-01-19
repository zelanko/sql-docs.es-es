---
title: DEALLOCATE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DEALLOCATE
- DEALLOCATE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- locking [SQL Server], cursors
- DEALLOCATE statement
- deallocations [SQL Server]
- deleting cursor references
- removing cursor references
ms.assetid: c75cf73d-0268-4c57-973d-b8a84ff801fa
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7dd1a4deca2a3c6db7db7596c94f0def97934da
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita una referencia a un cursor. Cuando se cancela la asignación de la última referencia al cursor, se liberan las estructuras de datos que componen el cursor por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor_name*  
 Es el nombre de un cursor ya declarado. Si hay tanto un cursor global y otro local con *cursor_name* como su nombre, *cursor_name* hace referencia al cursor global si se especifica GLOBAL y al cursor local si no se especifica GLOBAL.  
  
 @*cursor_variable_name*  
 Es el nombre de un **cursor** variable. @*cursor_variable_name* debe ser de tipo **cursor**.  
  
## <a name="remarks"></a>Comentarios  
 Las instrucciones que realizan operaciones sobre cursores utilizan un nombre de cursor o una variable de cursor para hacer referencia al cursor. DEALLOCATE quita la asociación existente entre un cursor y el nombre del cursor o la variable de cursor. Si un nombre o variable es el último que hace referencia a un cursor, se quita el cursor y se liberan los recursos que utiliza. Los bloqueos de desplazamiento utilizados para proteger el aislamiento de las capturas se liberan en DEALLOCATE. Los bloqueos de transacciones utilizados para proteger las actualizaciones, incluidas las actualizaciones posicionadas creadas a través del cursor, se mantienen hasta el final de la transacción.  
  
 La instrucción DECLARE CURSOR asigna y asocia un cursor a un nombre de cursor.  
  
```  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
 Después de asociar un nombre de cursor a un cursor, ningún otro cursor del mismo ámbito (GLOBAL o LOCAL) puede utilizar el nombre hasta que se haya cancelado la asignación al cursor.  
  
 Una variable de cursor se puede asociar a un cursor mediante uno de estos dos métodos:  
  
-   Por nombre con una instrucción SET que asocia un cursor a una variable de cursor.  
  
    ```  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   También se puede crear y asociar un cursor a una variable sin necesidad de definir un nombre de cursor.  
  
    ```  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 DEALLOCATE @*variableDeCursor* instrucción solo quita la referencia de la variable mencionada al cursor. No se desasigna la variable hasta que sale de ámbito al final del proceso por lotes, procedimiento almacenado o desencadenador. Después de DEALLOCATE @*variableDeCursor* instrucción, la variable puede asociarse a otro cursor mediante la instrucción SET.  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
  
DEALLOCATE @MyCursor;  
  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesTerritory;  
GO  
```  
  
 No es necesario cancelar explícitamente la asignación de una variable de cursor. La asignación de la variable se cancela implícitamente cuando sale de ámbito.  
  
## <a name="permissions"></a>Permissions  
 Los permisos para utilizar DEALLOCATE pertenecen de manera predeterminada a cualquier usuario válido.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente script muestra cómo los cursores se mantienen hasta que se ha desasignado el último nombre o variable que hace referencia a ellos.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create and open a global named cursor that  
-- is visible outside the batch.  
DECLARE abc CURSOR GLOBAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
OPEN abc;  
GO  
-- Reference the named cursor with a cursor variable.  
DECLARE @MyCrsrRef1 CURSOR;  
SET @MyCrsrRef1 = abc;  
-- Now deallocate the cursor reference.  
DEALLOCATE @MyCrsrRef1;  
-- Cursor abc still exists.  
FETCH NEXT FROM abc;  
GO  
-- Reference the named cursor again.  
DECLARE @MyCrsrRef2 CURSOR;  
SET @MyCrsrRef2 = abc;  
-- Now deallocate cursor name abc.  
DEALLOCATE abc;  
-- Cursor still exists, referenced by @MyCrsrRef2.  
FETCH NEXT FROM @MyCrsrRef2;  
-- Cursor finally is deallocated when last referencing  
-- variable goes out of scope at the end of the batch.  
GO  
-- Create an unnamed cursor.  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
SELECT * FROM Sales.SalesTerritory;  
-- The following statement deallocates the cursor  
-- because no other variables reference it.  
DEALLOCATE @MyCursor;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
