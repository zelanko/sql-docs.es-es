---
title: DBCC INDEXDEFRAG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INDEXDEFRAG
- DBCC INDEXDEFRAG
- DBCC_INDEXDEFRAG_TSQL
- INDEXDEFRAG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- defragmenting indexes
- DBCC INDEXDEFRAG statement
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 3c7df676-4843-44d0-8c1c-a9ab7e593b70
caps.latest.revision: 49
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 0421192834696a0fb6b785b3a3387507a3b9d827
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262383"
---
# <a name="dbcc-indexdefrag-transact-sql"></a>DBCC INDEXDEFRAG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Desfragmenta los índices de la tabla o la vista especificada.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) en su lugar.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC INDEXDEFRAG  
(  
    { database_name | database_id | 0 }   
    , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } [ , { partition_number | 0 } ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* | *database_id* | 0  
 Es la base de datos que contiene el índice que se va a desfragmentar. Si se especifica 0, se utiliza la base de datos actual. Los nombres de las bases de datos deben cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *table_name* | *table_id* | *view_name* | *view_id*  
 Es la tabla o la vista que contiene el índice que se va a desfragmentar. Los nombres de las tablas y las vistas deben ajustarse a las reglas de los identificadores.  
  
 *index_name* | *index_id*  
 Es el nombre o Id. del índice que se va a desfragmentar. Si no se especifica, la instrucción desfragmenta todos los índices de la tabla o la vista especificada. Los nombres de los índices deben ajustarse a las reglas de los identificadores.  
  
 *número_de_partición* | 0  
 Es el número de partición del índice que se va a desfragmentar. Si no se especifica o se especifica 0, la instrucción desfragmenta todas las particiones del índice especificado.  
  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="remarks"></a>Notas  
DBCC INDEXDEFRAG desfragmenta el nivel hoja de un índice para que el orden físico de las páginas coincida con el orden lógico de izquierda a derecha de los nodos hoja, lo que mejora el rendimiento de recorrido del índice.
  
> [!NOTE]  
>  Si se ejecuta DBCC INDEXDEFRAG, la desfragmentación del índice se realiza en serie. Esto significa que la operación en un índice único se realiza con un solo subproceso. No se produce ningún paralelismo. Además, las operaciones en varios índices desde la misma instrucción DBCC INDEXDEFRAG se realizan en los índices de uno en uno.  
  
DBCC INDEXDEFRAG también compacta las páginas de un índice, teniendo en cuenta el factor de relleno especificado cuando se creó el índice. Las páginas vacías creadas como consecuencia de esta compactación se quitan. Para obtener más información, vea [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).
  
Si un índice abarca más de un archivo, DBCC INDEXDEFRAG desfragmenta los archivos de uno en uno. Las páginas no se migran entre archivos.
  
DBCC INDEXDEFRAG especifica el porcentaje completado estimado cada cinco minutos. DBCC INDEXDEFRAG puede terminarse en cualquier momento del proceso y se mantiene el trabajo finalizado.
  
A diferencia de DBCC DBREINDEX, o la operación de generación del índice en general, DBCC INDEXDEFRAG es una operación en línea. No mantiene bloqueos a largo plazo. Por consiguiente, DBCC INDEXDEFRAG no bloquea la ejecución de consultas o actualizaciones. Se puede tardar menos en desfragmentar un índice relativamente poco fragmentado que en generar un índice nuevo porque el tiempo de desfragmentación está relacionado con el volumen de la fragmentación. Un índice muy fragmentado puede tardar mucho más en desfragmentarse que en volver a generarse.
  
La desfragmentación siempre se registra por completo con independencia de la configuración del modelo de recuperación. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md). La desfragmentación de un índice muy fragmentado puede generar más información en el registro que la creación de un índice de registro completo. No obstante, la desfragmentación se realiza como una serie de transacciones cortas y, por tanto, no es necesario un registro grande si se realizan con frecuencia copias de seguridad de registros o si la configuración del modelo de recuperación es SIMPLE.
  
## <a name="restrictions"></a>Restrictions  
DBCC INDEXDEFRAG coloca las páginas hoja del índice en su lugar. Por lo tanto, si un índice se intercala con otros índices en el disco, la ejecución de DBCC INDEXDEFRAG en dicho índice no ordena las páginas hoja del índice de forma contigua. Para mejorar la agrupación en clústeres de páginas, vuelva a generar el índice.
No se puede utilizar DBCC INDEXDEFRAG para desfragmentar los índices siguientes:
-   Un índice deshabilitado.  
-   Un índice con bloqueo de página establecido en OFF.  
-   Un índice espacial.  
  
El uso de DBCC INDEXDEFRAG no se admite en las tablas del sistema.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC INDEXDEFRAG devuelve el siguiente conjunto de resultados (los valores pueden variar) si se especifica un índice en la instrucción (a menos que se especifique WITH NO_INFOMSGS):
  
```sql
Pages Scanned Pages Moved Pages Removed  
------------- ----------- -------------  
359           346         8  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permisos  
El autor de la llamada debe ser el propietario de la tabla, o bien un miembro del rol fijo de servidor **sysadmin** o de los roles fijos de base de datos **db_owner** o **db_ddladmin**.
  
## <a name="examples"></a>Ejemplos  
### <a name="a-using-dbcc-indexdefrag-to-defragment-an-index"></a>A. Usar DBCC INDEXDEFRAG para desfragmentar un índice  
En el siguiente ejemplo se desfragmentan todas las particiones del índice `PK_Product_ProductID` de la tabla `Production.Product` de la base de datos `AdventureWorks`.
  
```sql  
DBCC INDEXDEFRAG (AdventureWorks2012, 'Production.Product', PK_Product_ProductID);  
GO  
```  
  
### <a name="b-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>B. Usar DBCC SHOWCONTIG y DBCC INDEXDEFRAG para desfragmentar los índices de una base de datos  
 En el siguiente ejemplo se muestra una forma sencilla de desfragmentar todos los índices de una base de datos que están fragmentados por encima de un umbral declarado.  
  
```sql  
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
  
  

