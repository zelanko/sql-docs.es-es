---
title: DROP TABLE (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_TABLE_TSQL
- DROP TABLE
dev_langs:
- TSQL
helpviewer_keywords:
- removing indexes
- table removal [SQL Server]
- deleting indexes
- dropping data
- deleting tables
- dropping indexes
- removing constraints
- removing permissions
- DROP TABLE statement
- removing tables
- deleting triggers
- removing data
- dropping tables
- deleting permissions
- dropping triggers
- deleting constraints
- removing triggers
- deleting data
- dropping constraints
- dropping permissions
ms.assetid: 0b6f2b6f-3aa3-4767-943f-43df3c3c5cfd
caps.latest.revision: 61
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22fa2a1da83dfef0743c089256fcd1e18af9b54c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-table-transact-sql"></a>DROP TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita una o varias definiciones de tabla y todos los datos, índices, desencadenadores, restricciones y especificaciones de permisos de esas tablas. Las vistas o procedimientos almacenados que hace referencia a la tabla quitada se deben quitar explícitamente mediante el uso de [DROP VIEW](../../t-sql/statements/drop-view-transact-sql.md) o [DROP PROCEDURE](../../t-sql/statements/drop-procedure-transact-sql.md). Para informar de las dependencias en una tabla, use [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP TABLE [ IF EXISTS ] [ database_name . [ schema_name ] . | schema_name . ]  
table_name [ ,...n ]  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos en la que se creó la tabla.  
  
 SQL Database de Microsoft Azure admite el formato de nombre de tres partes nombre_basededatos.[nombre_esquema].nombre_objeto cuando nombre_basededatos es la base de datos actual o tempdb y nombre_objeto comienza con #. SQL Database de Microsoft Azure no admite nombres de cuatro partes.  
  
 *IF EXISTE*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente quita la tabla solo si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la tabla.  
  
 *table_name*  
 Es el nombre de la tabla que se va a quitar.  
  
## <a name="remarks"></a>Comentarios  
 No se puede utilizar DROP TABLE para quitar una tabla a la que haga referencia una restricción FOREIGN KEY. Primero se debe quitar la restricción FOREIGN KEY o la tabla de referencia. Si la tabla de referencia y la tabla que tiene la clave principal se van a quitar en la misma instrucción DROP TABLE, la tabla de referencia debe aparecer primero.  
  
 Se pueden quitar varias tablas de cualquier base de datos. Si la tabla que se va a quitar hace referencia a la clave principal de otra tabla que también se va a quitar, la tabla de referencia con la clave externa debe aparecer antes que la tabla que tiene la clave principal a la que se hace referencia.  
  
 Cuando se quita la tabla, las reglas o valores predeterminados de la tabla pierden sus enlaces y se quitan automáticamente las restricciones o desencadenadores asociados con la tabla. Si vuelve a crear una tabla, debe volver a enlazar las reglas y valores predeterminados apropiados, volver a crear los desencadenadores y agregar todas las restricciones necesarias.  
  
 Si elimina todas las filas de una tabla mediante eliminar *tablename* o utilizar la instrucción TRUNCATE TABLE, la tabla existe hasta que se quite.  
  
 Los índices y las tablas grandes que utilizan más de 128 extensiones se quitan en dos fases independientes: lógica y física. En la fase lógica, las unidades de asignación existentes que utiliza la tabla se marcan para la cancelación de asignación y se bloquean hasta que se confirme la transacción. En la fase física, las páginas IAM marcadas para cancelación de asignación se quitan físicamente por lotes.  
  
 Si quita una tabla que contiene una columna de tipo VARBINARY(MAX) con el atributo FILESTREAM, los datos almacenados en el sistema de archivos no se quitarán.  
  
> [!IMPORTANT]  
>  DROP TABLE y CREATE TABLE no se deberían ejecutar en la misma tabla en el mismo lote. De lo contrario, podría producirse un error inesperado.  
  
## <a name="permissions"></a>Permissions  
 Se requiere el permiso ALTER en el esquema al que pertenece la tabla, el permiso CONTROL en la tabla o la pertenencia al rol fijo de base de datos **db_ddladmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-a-table-in-the-current-database"></a>A. Quitar una tabla de la base de datos actual  
 En el siguiente ejemplo se quita la tabla `ProductVendor1`, y sus datos e índices de la base de datos actual.  
  
```  
DROP TABLE ProductVendor1 ;  
```  
  
### <a name="b-dropping-a-table-in-another-database"></a>B. Quitar una tabla de otra base de datos  
 En el siguiente ejemplo se quita la tabla `SalesPerson2` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. El ejemplo se puede ejecutar desde cualquier base de datos de la instancia de servidor.  
  
```  
DROP TABLE AdventureWorks2012.dbo.SalesPerson2 ;  
```  
  
### <a name="c-dropping-a-temporary-table"></a>C. Quitar una tabla temporal  
 En el siguiente ejemplo se crea una tabla temporal, se comprueba si existe, se quita y se comprueba de nuevo si existe. En este ejemplo no utiliza la **IF EXISTS** sintaxis que está disponible a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
CREATE TABLE #temptable (col1 int);  
GO  
INSERT INTO #temptable  
VALUES (10);  
GO  
SELECT * FROM #temptable;  
GO  
IF OBJECT_ID(N'tempdb..#temptable', N'U') IS NOT NULL   
DROP TABLE #temptable;  
GO  
--Test the drop.  
SELECT * FROM #temptable;  
  
```  
  
### <a name="d-dropping-a-table-using-if-exists"></a>D. Quitar una tabla con IF EXISTS  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 En el ejemplo siguiente se crea una tabla denominada T1. A continuación, la segunda instrucción quita la tabla. La tercera instrucción no realiza ninguna acción porque ya se ha creado la tabla, sin embargo, esto no provoca un error.  
  
```  
CREATE TABLE T1 (Col1 int);  
GO  
DROP TABLE IF EXISTS T1;  
GO  
DROP TABLE IF EXISTS T1;  
```  
  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [TRUNCATE TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [Eliminar vista &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [DROP PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  

