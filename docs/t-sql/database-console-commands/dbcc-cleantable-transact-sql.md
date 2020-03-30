---
title: DBCC CLEANTABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
author: pmasl
ms.author: umajay
ms.openlocfilehash: 8cb3c1c0eba5c39083b6a6b39b4040639909808c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68101975"
---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
Recupera el espacio de columnas de longitud variable quitadas de tablas o vistas indizadas.
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* | *database_id* | 0  
 Es la base de datos a la que pertenece la tabla que se va a limpiar. Si se especifica 0, se utiliza la base de datos actual. Los nombres de las bases de datos deben cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *table_name* | *table_id* | *view_name*| *view_id*  
 Es la tabla o la vista indizada que se va a limpiar.  
  
 *batch_size*  
 Es el número de filas procesadas por transacción. Si no se especifica, o si su valor es 0, la instrucción procesa toda la tabla en una transacción.  
  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Observaciones  
DBCC CLEANTABLE recupera el espacio que deja una columna de longitud variable quitada. Una columna de longitud variable puede tener uno de los siguientes tipos de datos: **varchar**, **nvarchar**, **varchar(max)** , **nvarchar(max)** , **varbinary**, **varbinary(max)** , **text**, **ntext**, **image**, **sql_variant** y **xml**. El comando no recupera espacio después de que se haya quitado una columna de longitud fija.
Si las columnas quitadas estuvieran almacenadas de manera consecutiva, DBCC CLEANTABLE recupera espacio de la unidad de asignación IN_ROW_DATA de la tabla. Si estuvieran almacenadas de manera no consecutiva, se recupera espacio de la unidad de asignación ROW_OVERFLOW_DATA o LOB_DATA en función del tipo de datos de la columna quitada. Si al recuperar espacio de una página ROW_OVERFLOW_DATA o LOB_DATA se crea una página vacía, DBCC CLEANTABLE la quita.
DBCC CLEANTABLE se ejecuta como una o varias transacciones. Si no se especifica un tamaño de proceso por lotes, el comando procesa toda la tabla en una transacción y la tabla se bloquea en modo exclusivo durante la operación. Para algunas tablas grandes, la longitud de una transacción y el espacio de registro necesario puede ser muy grande. Si se especifica un tamaño de proceso por lotes, el comando se ejecuta en una serie de transacciones; cada una de ellas incluye el número de filas especificado. DBCC CLEANTABLE no se puede ejecutar como una transacción dentro de otra transacción.
Esta operación se registra por completo.
DBCC CLEANTABLE no se admite para su uso en tablas del sistema, tablas temporales o la parte de índice de almacén de columnas optimizado en memoria xVelocity de una tabla.
  
## <a name="best-practices"></a>Prácticas recomendadas  
DBCC CLEANTABLE no debe ejecutarse como una tarea de mantenimiento rutinaria. En lugar de ello, debe utilizarse después de realizar cambios significativos en columnas de longitud variable de una tabla o vista indizada, y hay que recuperar inmediatamente el espacio sin utilizar. Como alternativa, puede volver a generar los índices en la tabla o vista; no obstante, esta operación consume más recursos.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC CLEANTABLE devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permisos  
 El que llama debe ser propietario de la tabla o vista indexada, o miembro del rol fijo de servidor **sysadmin**, del rol fijo de base de datos **db_owner** o del rol fijo de base de datos **db_ddladmin**.  
  
## <a name="examples"></a>Ejemplos  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. Utilizar DBCC CLEANTABLE para recuperar espacio  
En el ejemplo siguiente se ejecuta DBCC CLEANTABLE para la tabla `Production.Document` de la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. Usar DBCC CLEANTABLE y comprobar los resultados  
En el ejemplo siguiente se crea y llena una tabla con varias columnas de longitud variable. Después se quitan dos columnas y se ejecuta DBCC CLEANTABLE para recuperar el espacio sin usar. Se ejecuta una consulta para comprobar los valores del recuento de páginas y el espacio ocupado antes y después de ejecutar el comando DBCC CLEANTABLE.
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  
