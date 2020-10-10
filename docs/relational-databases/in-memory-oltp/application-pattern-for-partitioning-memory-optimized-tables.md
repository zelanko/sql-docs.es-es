---
title: 'Patrón de aplicación: creación de particiones de tablas optimizadas para memoria'
description: Obtenga información sobre el modelo de diseño de la aplicación OLTP en memoria que almacena los datos actuales y activos en una tabla optimizada para memoria y los datos más antiguos en una tabla con particiones.
ms.custom: seo-dt-2019,issue-PR=4700-14820
ms.date: 05/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 08fb58f77382dae2d6455cc181c983798c89050a
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529416"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>Patrón de aplicación para crear particiones de tablas con optimización para memoria

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[hek_2](../../includes/hek-2-md.md)] admite un modelo de diseño de aplicaciones muy completo en cuanto a recursos de rendimiento de datos relativamente actuales. Este modelo es adecuado cuando los datos actuales se leen o actualizan con mucha más frecuencia que los datos más antiguos. En este caso, se dice que los datos actuales son *activos* o *de acceso frecuente* y los datos más antiguos, *inactivos*.

La idea principal es almacenar los datos *de acceso frecuente*  en una tabla optimizada para memoria. Los datos más antiguos que han pasado a ser *inactivos* se trasladan a una tabla con particiones de forma semanal o mensual. Los datos de las tablas con particiones se almacenan en un disco o en otra unidad de disco duro, no en memoria.

Por lo general, este diseño usa una clave de **fecha y hora** para que el proceso de traslado de datos distinga eficazmente entre datos activos y datos inactivos.

## <a name="advanced-partitioning"></a>Particiones avanzadas

El diseño pretende emular que existe una tabla con particiones que también tiene una partición optimizada para memoria. Para que este diseño funcione, hay que asegurarse de que todas las tablas comparten un esquema común. En el ejemplo de código que aparece más adelante en este artículo se muestra esta técnica.

Por definición, se da por hecho que los datos nuevos son datos de acceso frecuente. Los datos de acceso frecuente se insertan y actualizan en la tabla optimizada para memoria, mientras que los datos inactivos se conservan en la tabla con particiones tradicional. Cada cierto tiempo, un procedimiento almacenado agrega una nueva partición. La partición contiene los datos inactivos más recientes que se han extraído de la tabla optimizada para memoria.

Si una operación necesita únicamente datos de acceso frecuente, puede usar procedimientos almacenados compilados de forma nativa para acceder a esos datos. Las operaciones con posibilidad de acceder a datos de acceso frecuente o inactivos deben usar [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado para combinar la tabla optimizada para memoria con la tabla con particiones.

### <a name="add-a-partition"></a>Adición de una partición

Los datos que recientemente han pasado a ser inactivos deben trasladarse a la tabla con particiones. Estos son los pasos para realizar este intercambio periódico de particiones:

1. En el caso de los datos de la tabla optimizada para memoria, determine el valor de fecha y hora que actúe como límite entre los datos de acceso frecuente y los datos inactivos.
2. Inserte los datos inactivos recientes desde la tabla OLTP en memoria a una tabla *cold\_staging*.
3. Elimine los mismos datos antiguos de la tabla optimizada para memoria.
4. Intercambie la tabla cold\_staging por una partición.
5. Agregue la partición.

#### <a name="maintenance-window"></a>Ventana de mantenimiento

Uno de los pasos anteriores es eliminar los datos inactivos recientes de la tabla optimizada para memoria. Existe un intervalo de tiempo entre esta eliminación y el paso final para agregar la nueva partición. Durante este intervalo, se producirá un error si alguna aplicación intenta leer los datos inactivos recientes.

Para obtener un ejemplo relacionado, vea [Creación de particiones en el nivel de aplicación](../../relational-databases/in-memory-oltp/application-level-partitioning.md).

## <a name="code-sample"></a>Ejemplo de código

El siguiente ejemplo de Transact-SQL se separa en una serie de bloques de código más pequeños para presentarlos de forma más sencilla, pero se pueden incluir todos en un bloque de código grande para realizar pruebas.

En conjunto, el ejemplo de T-SQL refleja cómo usar una tabla optimizada para memoria con una tabla basada en disco con particiones.

En las primeras fases del ejemplo de T-SQL se crea la base de datos, tras lo cual se crean objetos como, por ejemplo, tablas en la base de datos. En las fases subsiguientes se muestra cómo mover datos de una tabla optimizada para memoria a una tabla con particiones.

### <a name="create-a-database"></a>Crear una base de datos

En esta sección del ejemplo de T-SQL se crea una base de datos de prueba. La base de datos está configurada para admitir tanto tablas optimizadas para memoria como tablas con particiones.

```sql
CREATE DATABASE PartitionSample;
GO

-- Add a FileGroup, enabled for In-Memory OLTP.
-- Change file path as needed.

ALTER DATABASE PartitionSample
    ADD FILEGROUP PartitionSample_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE PartitionSample
    ADD FILE(
        NAME = 'PartitionSample_mod',
        FILENAME = 'c:\data\PartitionSample_mod')
    TO FILEGROUP PartitionSample_mod;
GO
```

### <a name="create-a-memory-optimized-table-for-hot-data"></a>Creación de una tabla optimizada para memoria para los datos de acceso frecuente

En esta sección se crea la tabla optimizada para memoria que va a contener los datos más recientes, que siguen siendo principalmente datos de acceso frecuente.

```sql
USE PartitionSample;
GO

-- Create a memory-optimized table for the HOT Sales Order data.
-- Notice the index that uses datetime2.

CREATE TABLE dbo.SalesOrders_hot (
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,
   so_total MONEY NOT NULL,
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) WITH (MEMORY_OPTIMIZED=ON);
GO
```

### <a name="create-a-partitioned-table-for-cold-data"></a>Creación de una tabla con particiones para los datos inactivos

En esta sección se crea la tabla con particiones que va a contener los datos inactivos.

```sql
-- Create a partition and table for the COLD Sales Order data.
-- Notice the index that uses datetime2.

CREATE PARTITION FUNCTION [ByDatePF](datetime2) AS RANGE RIGHT
   FOR VALUES();
GO

CREATE PARTITION SCHEME [ByDateRange]
   AS PARTITION [ByDatePF]
   ALL TO ([PRIMARY]);
GO

CREATE TABLE dbo.SalesOrders_cold (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) ON [ByDateRange](so_date);
GO
```

### <a name="create-a-table-to-store-cold-data-during-move"></a>Creación de una tabla donde almacenar los datos inactivos durante el traslado de datos

En esta sección se crea la tabla cold\_staging. También se crea una vista que une los datos de acceso frecuente y los datos inactivos de ambas tablas.

```sql
-- A table used to briefly stage the newly cold data, during moves to a partition.

CREATE TABLE dbo.SalesOrders_cold_staging (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date datetime2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')
);
GO

-- A view, for retrieving the aggregation of hot plus cold data.

CREATE VIEW dbo.SalesOrders
AS SELECT so_id,
          cust_id,
          so_date,
          so_total,
          1 AS 'is_hot'
       FROM dbo.SalesOrders_hot
   UNION ALL
   SELECT so_id,
          cust_id,
          so_date,
          so_total,
          0 AS 'is_cold'
       FROM dbo.SalesOrders_cold;
GO
```

### <a name="create-the-stored-procedure"></a>Creación del procedimiento almacenado

En esta sección se crea el procedimiento almacenado que se va a ejecutar periódicamente. El procedimiento traslada los datos inactivos recientes de la tabla optimizada para memoria a la tabla con particiones.

```sql
-- A stored procedure to move all newly cold sales orders data
-- to its staging location.

CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2
   AS
   BEGIN
      BEGIN TRANSACTION;

      -- Insert the cold data as a temporary heap.
      INSERT INTO dbo.SalesOrders_cold_staging WITH (TABLOCKX)
      SELECT so_id , cust_id , so_date , so_total
         FROM dbo.SalesOrders_hot WITH (serializable)
         WHERE so_date <= @splitdate;

      -- Delete the moved data from the hot table.
      DELETE FROM dbo.SalesOrders_hot WITH (SERIALIZABLE)
         WHERE so_date <= @splitdate;

      -- Update the partition function, and switch in the new partition.
      ALTER PARTITION SCHEME [ByDateRange] NEXT USED [PRIMARY];

      DECLARE @p INT = (
        SELECT MAX(partition_number)
            FROM sys.partitions
            WHERE object_id = OBJECT_ID('dbo.SalesOrders_cold'));

      EXEC sp_executesql
        N'ALTER TABLE dbo.SalesOrders_cold_staging
            SWITCH TO dbo.SalesOrders_cold partition @i',
        N'@i int',
        @i = @p;

      ALTER PARTITION FUNCTION [ByDatePF]()
      SPLIT RANGE( @splitdate);

      -- Modify a constraint on the cold_staging table, to align with new partition.
      ALTER TABLE dbo.SalesOrders_cold_staging
         DROP CONSTRAINT CHK_SalesOrders_cold_staging;

      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging 
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';
      PRINT @sql;
      EXEC sp_executesql @sql;

      COMMIT;
END;
GO
```

### <a name="prepare-sample-data-and-demo-the-stored-procedure"></a>Preparación de los datos de ejemplo y ejecución del procedimiento almacenado como demostración

En esta sección se generan e insertan datos de ejemplo y, tras ello, se ejecuta el procedimiento almacenado a modo de demostración.

```sql
-- Insert sample values into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO

-- Verify that the hot data is in the table, by selecting from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Treat all data in the hot table as cold data:
-- Run the stored procedure, to move (offload) all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Again, read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Retrieve the name of every partition.
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');

-- Insert more data into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, run the stored procedure, to move all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, retrieve the name of every partition.
-- The stored procedure can modify the partitions.
SELECT OBJECT_NAME( object_id) , partition_number , row_count
  FROM sys.dm_db_partition_stats ps
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold')
    AND index_id = 1;
```

### <a name="drop-all-the-demo-objects"></a>Eliminación de todos los objetos de demostración

No olvide limpiar la base de datos de prueba de demostración del sistema de prueba.

```sql
-- You must first leave the context of the PartitionSample database.

-- USE <A-Database-Name-Here>;
GO

DROP DATABASE PartitionSample;
GO
```

## <a name="see-also"></a>Consulte también

[Tablas optimizadas para la memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
