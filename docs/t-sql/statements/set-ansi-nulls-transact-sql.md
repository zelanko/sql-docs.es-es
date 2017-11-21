---
title: SET ANSI_NULLS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_ANSI_NULLS_TSQL
- ANSI_NULLS
- SET ANSI_NULLS
- ANSI_NULLS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULLS statement
- not equal to operator (<>)
- ANSI_NULLS option
- equals operator (=)
- null values [SQL Server], comparison operators
- comparison operators [SQL Server], null values
ms.assetid: aae263ef-a3c7-4dae-80c2-cc901e48c755
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 285803fe112cc0370b8af6049f48846c7ba55cab
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="set-ansinulls-transact-sql"></a>SET ANSI_NULLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Especifica el comportamiento conforme a ISO de los operadores de comparación Es igual a (=) y No es igual a (<>) cuando se usan con valores NULL en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS siempre se establecerá en ON y cualquier aplicación que establezca de forma explícita la opción en OFF generará un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_NULLS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_NULLS ON;  
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando SET ANSI_NULLS es ON, una instrucción SELECT que utilice WHERE *column_name* = **NULL** devuelve cero filas incluso si no hay valores null en *column_name*. Una instrucción SELECT que utilice WHERE *column_name* <> **NULL** devuelve cero filas incluso si no hay valores distintos de NULL en *column_name*.  
  
 Cuando SET ANSI_NULLS se establece en OFF, los operadores de comparación Es igual a (=) y No es igual a (<>) no siguen el estándar ISO. Una instrucción SELECT que utilice WHERE *column_name* = **NULL** devuelve las filas que tienen valores null en *column_name*. Una instrucción SELECT que utilice WHERE *column_name* <> **NULL** devuelve las filas que tienen valores distintos de NULL en la columna. Además, una instrucción SELECT que utilice WHERE *column_name* <> *XYZ_value* devuelve todas las filas que no son *XYZ_value* y que no son NULL.  
  
 Cuando SET ANSI_NULLS es ON, todas las comparaciones con un valor NULL se evalúan como UNKNOWN. Cuando SET ANSI_NULLS es OFF, la comparación de cualquier dato con un valor NULL se evalúa como TRUE si el valor del dato es NULL. Si no se especifica SET ANSI_NULLS, se aplica el valor de la opción de base de datos ANSI_NULLS. Para obtener más información acerca de la opción de base de datos ANSI_NULLS, vea [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET ANSI_NULLS ON solo afecta a una comparación si uno de los operandos es una variable que es NULL o un NULL literal. Si ambos lados de la comparación son columnas o expresiones compuestas, la configuración no afecta a la comparación.  
  
 Para que un script funcione como se pretende, independientemente de la opción de base de datos ANSI_NULLS o de la opción SET ANSI_NULLS, use IS NULL e IS NOT NULL en las comparaciones que puedan contener valores NULL.  
  
 SET ANSI_NULLS debe ser ON para ejecutar consultas distribuidas.  
  
 SET ANSI_NULLS también debe ser ON al crear o cambiar índices en columnas calculadas o vistas indizadas. Si SET ANSI_NULLS es OFF, las instrucciones CREATE, UPDATE, INSERT y DELETE producirán errores en tablas con índices en columnas calculadas y vistas indizadas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un error que muestra todas las opciones SET que infringen los valores requeridos. Además, al ejecutar una instrucción SELECT, si SET ANSI_NULLS es OFF, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] omitirá los valores de índice en columnas calculadas o vistas y resolverá la operación de selección como si no hubiera tales índices en las tablas o vistas.  
  
> [!NOTE]  
>  ANSI_NULLS es una de las siete opciones SET a las que se deben asignar unos valores requeridos para tratar índices en columnas calculadas o vistas indizadas. Las opciones ANSI_PADDING, ANSI_WARNINGS, ARITHABORT, QUOTED_IDENTIFIER y CONCAT_NULL_YIELDS_NULL también se deben establecer en ON, y NUMERIC_ROUNDABORT se debe establecer en OFF.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente ANSI_NULLS en ON al conectarse. Esta opción se puede configurar en los orígenes de datos ODBC, en los atributos de conexión ODBC o en las propiedades de conexión OLE DB establecidas en la aplicación antes de conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado de SET ANSI_NULLS es OFF.  
  
 Cuando SET ANSI_DEFAULTS es ON, se habilita SET ANSI_NULLS.  
  
 La opción SET ANSI_NULLS se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @ANSI_NULLS VARCHAR(3) = 'OFF';  
IF ( (32 & @@OPTIONS) = 32 ) SET @ANSI_NULLS = 'ON';  
SELECT @ANSI_NULLS AS ANSI_NULLS;  
  
```  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utilizan los operadores de comparación Es igual a (`=`) y No es igual a (`<>`) para realizar comparaciones con valores `NULL` y distintos de NULL en una tabla. El ejemplo también muestra que `IS NULL` no se ve afectado por la `SET ANSI_NULLS` configuración.  
  
```  
-- Create table t1 and insert values.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 values (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [= &#40; Es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [IF... ELSE &#40; Transact-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [&#60; &#62; &#40; No igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  

