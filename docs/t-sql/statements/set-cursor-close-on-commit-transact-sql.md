---
title: SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURSOR_CLOSE_ON_COMMIT
- SET CURSOR_CLOSE_ON_COMMIT
- CURSOR_CLOSE_ON_COMMIT_TSQL
- SET_CURSOR_CLOSE_ON_COMMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CURSOR_CLOSE_ON_COMMIT option
- transactions [SQL Server], cursors
- closing cursors
- cursors [SQL Server], closing
- SET CURSOR_CLOSE_ON_COMMIT statement
ms.assetid: 7b976154-98ce-4a06-bbae-7e59c34211f7
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de736d329175fe44c8bf837a2a6ef0ca966666ee
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-cursorcloseoncommit-transact-sql"></a>SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Controla el comportamiento de la instrucción COMMIT TRANSACTION de [!INCLUDE[tsql](../../includes/tsql-md.md)]. El valor predeterminado de esta configuración es OFF. Indica que el servidor no cerrará los cursores cuando se confirme una transacción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentarios  
 Si SET CURSOR_CLOSE_ON_COMMIT es ON, este valor cierra cualquier cursor abierto al confirmar o revertir de conformidad con ISO. Si SET CURSOR_CLOSE_ON_COMMIT es OFF, no se cierra el cursor cuando se confirma una transacción.  
  
> [!NOTE]  
>  Si SET CURSOR_CLOSE_ON_COMMIT es ON, no se cierran los cursores abiertos al revertir si la reversión se aplica a savepoint_name desde una instrucción SAVE TRANSACTION.  
  
 Si SET CURSOR_CLOSE_ON_COMMIT es OFF, la instrucción ROLLBACK cierra solo los cursores asincrónicos que no se han terminado de llenar. Los cursores STATIC o INSENSITIVE abiertos después de realizar modificaciones ya no reflejarán el estado de los datos si las modificaciones se revierten.  
  
 SET CURSOR_CLOSE_ON_COMMIT controla el mismo comportamiento que la opción de base de datos CURSOR_CLOSE_ON_COMMIT. Si CURSOR_CLOSE_ON_COMMIT se establece en ON u OFF, esa configuración se utiliza en la conexión. Si no se ha especificado SET CURSOR_CLOSE_ON_COMMIT, el valor de la **is_cursor_close_on_commit_on** columna en el **sys.databases** se aplica la vista de catálogo.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client establece CURSOR_CLOSE_ON_COMMIT en OFF cuando se conectan. DB-Library no establece automáticamente el valor de CURSOR_CLOSE_ON_COMMIT.  
  
 Si SET ANSI_DEFAULTS es ON, se habilita SET CURSOR_CLOSE_ON_COMMIT.  
  
 La opción SET CURSOR_CLOSE_ON_COMMIT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @CURSOR_CLOSE VARCHAR(3) = 'OFF';  
IF ( (4 & @@OPTIONS) = 4 ) SET @CURSOR_CLOSE = 'ON';  
SELECT @CURSOR_CLOSE AS CURSOR_CLOSE_ON_COMMIT;  
```  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se define un cursor en una transacción y se intenta utilizar después de confirmar la transacción.  
  
```  
-- SET CURSOR_CLOSE_ON_COMMIT  
-------------------------------------------------------------------------------  
SET NOCOUNT ON;  
  
CREATE TABLE t1 (a INT);  
GO   
  
INSERT INTO t1   
VALUES (1), (2);  
GO  
  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT ON';  
GO  
SET CURSOR_CLOSE_ON_COMMIT ON;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT OFF';  
GO  
SET CURSOR_CLOSE_ON_COMMIT OFF;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
DROP TABLE t1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [Cerrar &#40; Transact-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  

