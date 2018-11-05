---
title: Configurar PolyBase para acceder a datos externos en SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 90b535714eea3a00ecffd2cf010187fbcd676a82
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806645"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar PolyBase para acceder a datos externos en SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En el artículo se explica cómo usar PolyBase en una instancia de SQL Server para consultar datos externos en otra instancia de SQL Server.

## <a name="prerequisites"></a>Prerequisites

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md). En el artículo de instalación se explican los requisitos previos.

## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos de un origen de datos de SQL Server, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear estas tablas externas. 
 
Se recomienda crear estadísticas en las columnas de tabla externa, sobre todo en las que se usan para las combinaciones, filtros y agregados, para obtener un rendimiento óptimo de las consultas.

En esta sección se crearán estos objetos:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. Cree una clave maestra en la base de datos. Esto es necesario para cifrar el secreto de credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
     ```

1. Cree una credencial de ámbito de base de datos.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials   
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). Especifique la ubicación de origen de datos externos y las credenciales para SQL Server.

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
    WITH ( 
    LOCATION = sqlserver://SqlServer,
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = SQLServerCredentials
    );

     ```

1. Crear esquemas para datos externos

     ```sql
     CREATE SCHEMA sqlserver;
     GO
     ```

1.  Cree tablas externas que representen los datos almacenados en la instancia externa de SQL Server [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: sql server table/view in 'database_name.schema_name.object_name' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE sqlserver.customer(
     C_CUSTKEY INT NOT NULL,
     C_NAME VARCHAR(25) NOT NULL,
     C_ADDRESS VARCHAR(40) NOT NULL,
     C_NATIONKEY INT NOT NULL,
     C_PHONE CHAR(15) NOT NULL,
     C_ACCTBAL DECIMAL(15,2) NOT NULL,
     C_MKTSEGMENT CHAR(10) NOT NULL,
     C_COMMENT VARCHAR(117) NOT NULL
      )
      WITH (
      LOCATION='tpch_10.dbo.customer',
      DATA_SOURCE=SqlServerInstance
     );
      ```

1. Cree estadísticas en una tabla externa.

     ```sql
      CREATE STATISTICS CustomerCustKeyStatistics ON sqlserver.customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="sql-server-connector-compatible-types"></a>Tipos compatibles con el Conector de SQL Server

Es posible realizar una conexión con otros orígenes de datos que reconozca una conexión de SQL Server. Con el conector de SQL Server PolyBase puede crear una tabla externa de **Azure SQL Data Warehouse y Azure SQL Database**. Esto se consigue mediante los mismos pasos indicados arriba. Asegúrese de que la credencial de ámbito de base de datos, la dirección del servidor, el puerto y la cadena de ubicación se correspondan con los del origen de datos compatible al que quiere conectarse.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
