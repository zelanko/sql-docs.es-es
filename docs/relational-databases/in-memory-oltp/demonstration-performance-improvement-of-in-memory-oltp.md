---
title: "Demostración: mejora de rendimiento de OLTP en memoria | Microsoft Docs"
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 030764b39018049a729496177f967f659fb5b08c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Demostración: mejora de rendimiento de OLTP en memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  En el ejemplo de código de este tema se muestra el rápido funcionamiento de las tablas optimizadas para memoria. La mejora del rendimiento es evidente cuando el acceso a los datos de una tabla optimizada para memoria se realiza desde [!INCLUDE[tsql](../../includes/tsql-md.md)]tradicional interpretado. Esta mejora del rendimiento es incluso mayor cuando el acceso a los datos de una tabla optimizada para memoria se realiza a través de un procedimiento almacenado compilado de forma nativa (NCSProc).  
 
Para una demostración más completa de las posibles mejoras de rendimiento de OLTP en memoria, consulte [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)(Demostración de rendimiento de OLTP en memoria v1.0). 
  
 El ejemplo de código del presente artículo es de un solo subproceso y no aprovecha las ventajas de simultaneidad de OLTP en memoria. Una carga de trabajo que utiliza simultaneidad verá mayor mejora de rendimiento. El ejemplo de código muestra solo un aspecto de mejora del rendimiento, la eficacia de acceso a datos para la operación INSERT.  
  
 La mejora del rendimiento que ofrecen las tablas optimizadas para memoria se percibe totalmente cuando el acceso a los datos de una tabla optimizada para memoria se realiza a través de un NCSProc.  
  
## <a name="code-example"></a>Ejemplo de código  
 En las siguientes subsecciones se describe cada paso.  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>Paso 1a: requisito previo si se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Los pasos de la primera subsección solo se aplican si se está ejecutando en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero no si se está ejecutando en [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Realice lo siguiente:  
  
1.  Use SQL Server Management Studio (SSMS.exe) para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cualquier herramienta similar a SSMS.exe también está bien.  
  
2.  Cree manualmente un directorio denominado **C:\data\\**. El código de ejemplo de Transact-SQL espera que el directorio ya exista.  
  
3.  Ejecute el T-SQL corto para crear la base de datos y su grupo de archivos optimizados para memoria.  
  
```sql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>Paso 1b: requisito previo si se usa [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
 Esta subsección es válida solo si se está usando [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Realice lo siguiente:  
  
1.  Decida qué base de datos de prueba existente usará para el ejemplo de código.  
  
2.  Si decide crear una nueva base de datos de prueba, use el [portal de Azure](http://portal.azure.com) para crear una base de datos denominada **imoltp**.  
  
 Si desea obtener instrucciones para usar el portal de Azure para esto, consulte [Get Started with Azure SQL Database (Introducción a Base de datos SQL de Azure)](http://azure.microsoft.com/documentation/articles/sql-database-get-started).  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>Paso 2: crear tablas con optimización para memoria y un NCSProc.  
 En este paso se crean tablas optimizadas para memoria y un procedimiento almacenado compilado de forma nativa (NCSProc). Realice lo siguiente:  
  
1.  Use SSMS.exe para conectarse a la nueva base de datos.  
  
2.  Ejecute el siguiente T-SQL en la base de datos.  
  
```sql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>Paso 3: ejecutar el código  
 Ahora se pueden ejecutar las consultas que mostrarán el rendimiento de las tablas optimizadas para memoria. Realice lo siguiente:  
  
1.  Use SSMS.exe para ejecutar el siguiente T-SQL en la base de datos.  
  
     No haga caso de los datos de velocidad u otros datos de rendimiento que se generen durante esta primera ejecución. La primera ejecución garantiza la realización de varias operaciones que se efectúan una sola vez, como las asignaciones iniciales de memoria.  
  
2.  Vuelva a usar SSMS.exe para ejecutar el siguiente T-SQL en la base de datos.  
  
```sql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 A continuación se muestran las estadísticas de tiempo de salida generadas por la segunda ejecución de prueba.  
  
```sql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>Ver también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
