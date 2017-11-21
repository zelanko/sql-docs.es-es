---
title: SET ARITHABORT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ARITHABORT_TSQL
- ARITHABORT
- SET ARITHABORT
- SET_ARITHABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- terminating queries
- queries [SQL Server], terminating
- overflow errors [SQL Server]
- ARITHABORT option
- divide-by-zero errors
- SET ARITHABORT statement
- ending queries [SQL Server]
- stopping queries
ms.assetid: f938a666-fdd1-4233-b97f-719f27b1a0e6
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 97f65f734e68cc0a1ec4c019d50ce72b9c7e1bde
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-arithabort-transact-sql"></a>SET ARITHABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cancela una consulta cuando se produce un error de desbordamiento o división por cero durante su ejecución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ARITHABORT { ON | OFF }  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ARITHABORT ON   
[ ; ]  
```  
  
## <a name="remarks"></a>Comentarios  
 Debe establecer siempre ARITHABORT en ON en las sesiones de inicio de sesión. Establecer ARITHABORT en OFF puede afectar negativamente optimización de consultas de impacto dan lugar a problemas de rendimiento.  
  
> [!WARNING]  
>  La configuración predeterminada de ARITHABORT para [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] es ON. Las aplicaciones cliente que establecen ARITHABORT en OFF pueden recibir distintos planes de consulta, lo que dificulta la solución de problemas de consultas con un rendimiento bajo. Es decir, la misma consulta puede ejecutarse más deprisa en Management Studio y más despacio en la aplicación. Al solucionar problemas de consultas con [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use siempre la configuración de ARITHABORT del cliente.  
  
 Si SET ARITHABORT es ON y SET ANSI WARNINGS es ON, estas condiciones de error pueden cancelar una consulta.  
  
 Si SET ARITHABORT es ON y SET ANSI WARNINGS es OFF, estas condiciones de error pueden cancelar un lote. Si los errores se producen en una transacción, ésta se revierte. Si SET ARITHABORT es OFF y se produce uno de estos errores, aparece un mensaje de advertencia y se asigna el valor NULL al resultado de la operación aritmética.  
  
 Si SET ARITHABORT es OFF y SET ANSI WARNINGS es OFF y se produce uno de estos errores, aparece un mensaje de advertencia y se asigna el valor NULL al resultado de la operación aritmética.  
  
> [!NOTE]  
>  Si no se ha establecido SET ARITHABORT ni SET ARITHIGNORE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve NULL y muestra un mensaje de advertencia después de ejecutar la consulta.  
  
 Al establecer ANSI_WARNINGS en ON, ARITHABORT se establece de forma implícita en ON cuando el nivel de compatibilidad de base de datos está establecido en 90 o un valor superior. Si el nivel de compatibilidad de base de datos se establece en 80 o menos, la opción ARITHABORT debe establecerse explícitamente en ON.  
  
 Si al evaluar una expresión con SET ARITHABORT en OFF, una instrucción INSERT, DELETE o UPDATE encuentra un error aritmético, desbordamiento, división por cero o error de dominio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inserta o actualiza un valor NULL. Si la columna de destino no acepta valores NULL, no se puede efectuar la acción de inserción o actualización y el usuario recibe un error.  
  
 Si SET ARITHABORT o SET ARITHIGNORE es OFF y SET ANSI_WARNINGS es ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un mensaje de error cuando haya errores de división por cero o desbordamiento.  
  
 Si SET ARITHABORT es OFF y se produce un error de anulación durante la evaluación de una condición booleana de una instrucción IF, se ejecutará la rama FALSE.  
  
 SET ARITHABORT también debe ser ON al crear o cambiar índices en columnas calculadas o vistas indizadas. Si SET ARITHABORT es OFF, las instrucciones CREATE, UPDATE, INSERT y DELETE provocarán errores en tablas con índices en columnas calculadas y vistas indizadas.  
  
 La opción SET ARITHABORT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @ARITHABORT VARCHAR(3) = 'OFF';  
IF ( (64 & @@OPTIONS) = 64 ) SET @ARITHABORT = 'ON';  
SELECT @ARITHABORT AS ARITHABORT;  
  
```  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestran errores de división por cero y desbordamiento con las dos opciones de `SET ARITHABORT`.  
  
```  
-- SET ARITHABORT  
-------------------------------------------------------------------------------  
-- Create tables t1 and t2 and insert data values.  
CREATE TABLE t1 (  
   a TINYINT,   
   b TINYINT  
);  
CREATE TABLE t2 (  
   a TINYINT  
);  
GO  
INSERT INTO t1   
VALUES (1, 0);  
INSERT INTO t1   
VALUES (255, 1);  
GO  
  
PRINT '*** SET ARITHABORT ON';  
GO  
-- SET ARITHABORT ON and testing.  
SET ARITHABORT ON;  
GO  
  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab   
FROM t1;  
GO  
  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be no data';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Truncate table t2.  
TRUNCATE TABLE t2;  
GO  
  
-- SET ARITHABORT OFF and testing.  
PRINT '*** SET ARITHABORT OFF';  
GO  
SET ARITHABORT OFF;  
GO  
  
-- This works properly.  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab    
FROM t1;  
GO  
  
-- This works as if SET ARITHABORT was ON.  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be 0 rows';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Drop tables t1 and t2.  
DROP TABLE t1;  
DROP TABLE t2;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHIGNORE &#40; Transact-SQL &#41;](../../t-sql/statements/set-arithignore-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

