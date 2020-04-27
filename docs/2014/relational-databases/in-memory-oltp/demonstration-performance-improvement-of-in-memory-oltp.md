---
title: 'Demostración: mejora de rendimiento de OLTP en memoria | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c9477a318d2cb4f9886d67da8a4f8b5967cc180
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63071790"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Demostración: mejora de rendimiento de OLTP en memoria
  En este ejemplo se muestran las mejoras de rendimiento al usar OLTP en memoria al hacer una comparación de las diferencias en la respuesta el tiempo de espera cuando se ejecuta una consulta de Transact-SQL idéntica en tablas optimizadas en memoria y basadas en disco tradicionales. Además, también se crea un procedimiento almacenado compilado de forma nativa (basado en la misma consulta) y luego se ejecuta para demostrar que se suelen obtener los mejores tiempos de respuesta al consultar una tabla optimizada en memoria con un procedimiento almacenado compilado de forma nativa. En este ejemplo solo se muestra un aspecto de las mejoras de rendimiento al acceder a los datos en tablas optimizadas en memoria; la eficacia del acceso a datos al realizar inserciones. Este ejemplo es de un solo subproceso y no aprovecha las ventajas de simultaneidad de OLTP en memoria. Una carga de trabajo que utiliza simultaneidad verá mayor mejora de rendimiento.  
  
> [!NOTE]  
>  Está disponible otro ejemplo que muestra las tablas optimizadas para memoria en [Ejemplo de OLTP en memoria de SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Para completar este ejemplo, realizará las acciones siguientes:  
  
1.  Crear una base de datos denominada **imoltp** y modificar sus detalles de archivo con el fin de configurarla para usar OLTP en memoria.  
  
2.  Crear los objetos de base de datos para nuestro ejemplo: tres tablas y un procedimiento almacenado compilado de forma nativa.  
  
3.  Ejecutar las distintas consultas y mostrar los tiempos de respuesta para cada una de ellas.  
  
 Para configurar la base de datos **imoltp** en nuestro ejemplo, primero cree una carpeta vacía: **c:\imoltp_data**y luego ejecute el siguiente código:  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 A continuación, ejecute el siguiente código para crear la tabla basada en disco, dos (2) tablas optimizadas en memoria y el procedimiento almacenado compilado de forma nativa que se usará para mostrar los distintos métodos de acceso a datos:  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 La instalación se completa y estamos preparados para ejecutar las consultas que mostrarán los tiempos de respuesta al hacer una comparación del rendimiento entre los métodos de acceso de datos.  
  
 Para completar el ejemplo, ejecute el siguiente código varias veces. Omita los resultados de la primera ejecución que se ve afectado negativamente por la asignación de memoria inicial.  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 Los resultados esperados proporcionan tiempos de respuesta reales que muestran cómo el uso de tablas optimizadas en memoria y procedimientos almacenados compilados de forma nativa suele proporcionar tiempos de respuesta sistemáticamente más rápidos que las mismas cargas de trabajo que se ejecutan en tablas basadas en disco tradicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Extensiones de AdventureWorks para mostrar OLTP en memoria](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [&#40;de optimización en memoria de OLTP en memoria&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Tablas con optimización para memoria](memory-optimized-tables.md)   
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)   
 [Requisitos para usar tablas optimizadas para memoria](requirements-for-using-memory-optimized-tables.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Opciones File y filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [CREAR procedimientos y tablas optimizadas para memoria](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
