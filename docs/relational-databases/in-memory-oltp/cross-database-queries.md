---
title: Consultas entre bases de datos | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 92ee900e67fc15542188e8606c4331775738252c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="cross-database-queries"></a>Consultas entre bases de datos
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], las tablas optimizadas para memoria no admiten las transacciones entre bases de datos. No puede tener acceso a otra base de datos desde la misma transacción o desde la misma consulta que tiene acceso también a una tabla optimizada para memoria. No puede copiar fácilmente los datos de una tabla de una base de datos en una tabla optimizada para memoria de otra base de datos.  
  
 Las variables de tabla no son transaccionales. Por tanto, se pueden utilizar las variables de tabla optimizada para memoria en consultas entre bases de datos y pueden así facilitar la migración de datos de una base de datos a tablas optimizadas para memoria de otra. Puede utilizar dos transacciones. En la primera transacción, inserte los datos de la tabla remota en la variable. En la segunda transacción, inserte los datos en la tabla optimizada para memoria local desde la variable.  Para más información sobre las variables de tabla optimizada para memoria, consulte [Tabla temporal y variante de tabla más rápidas utilizando la optimización para memoria](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).
  
## <a name="example"></a>Ejemplo
En este ejemplo se muestra un método para transferir datos desde una base de datos a una tabla optimizada para memoria en una tabla de datos distinta.

1. Cree objetos de prueba.  Ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  

    ```tsql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',   SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  Intente ejecutar una consulta a través de las bases de datos. Ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
  
    ```tsql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    Debería recibir el siguiente mensaje de error:
    > Mensaje 41317, nivel 16, estado 5  
    > Una transacción de usuario que accede a tablas con optimización para memoria o módulos compilados de forma nativa no puede acceder a más de una base de datos de usuario o a las bases de datos modelo y msdb, y no puede escribir en la base de datos maestra.

3.  Cree un tipo de tabla optimizada para memoria.  Ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

    ```tsql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  Vuelva a intentar ejecutar la consulta a través de las bases de datos.  Esta vez, los datos de origen se transmitirán primero a una variable de tabla optimizada para memoria.  Luego los datos de la variable de tabla se transferirán a la tabla optimizada para memoria.
    ```tsql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>Vea también  
 [Migrar a OLTP en memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
