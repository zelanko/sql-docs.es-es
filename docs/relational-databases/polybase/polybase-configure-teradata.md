---
title: Configurar PolyBase para obtener acceso a datos externos en Teradata | Microsoft Docs
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
ms.openlocfilehash: b1baf1655619a3bc4b61939e2de8310956c9678d
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874280"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>Configurar PolyBase para obtener acceso a datos externos en Teradata

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En el artículo se explica cómo usar PolyBase en una instancia de SQL Server para consultar datos externos en Teradata.

## <a name="prerequisites"></a>Prerequisites

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md). En el artículo de instalación se explican los requisitos previos.

Para usar PolyBase en Teradata, se requiere VC++ Redistributable. 
 
## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos de un origen de datos de Teradata, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear estas tablas externas. 
 
Se recomienda crear estadísticas en las columnas de tabla externa. Especialmente las que se usan para combinaciones, filtros y agregados, para obtener un rendimiento óptimo de las consultas.

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
     CREATE DATABASE SCOPED CREDENTIAL TeradataCredentials 
     WITH IDENTITY = 'username', Secret = 'password'
     ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). Especifique la ubicación de origen de datos externos y las credenciales para Teradata.

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE TeradataInstance
    WITH ( 
    LOCATION = teradata://TeradataServer,
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = TeradataCredentials
    );

     ```

1. Crear esquemas para datos externos

     ```sql
     CREATE SCHEMA teradata;
     GO
     ```

1.  Cree tablas externas que representen los datos almacenados en el sistema de Teradata externo [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: Teradata table/view in '<database_name>.<object_name>' format
      *  DATA_SOURCE: the external data source, created above.
      */
     CREATE EXTERNAL TABLE teradata.lineitem(
      L_ORDERKEY INT NOT NULL,
      L_PARTKEY INT NOT NULL,
     L_SUPPKEY INT NOT NULL,
     L_LINENUMBER INT NOT NULL,
     L_QUANTITY DECIMAL(15,2) NOT NULL,
     L_EXTENDEDPRICE DECIMAL(15,2) NOT NULL,
     L_DISCOUNT DECIMAL(15,2) NOT NULL,
     L_TAX DECIMAL(15,2) NOT NULL,
     L_RETURNFLAG CHAR NOT NULL,
     L_LINESTATUS CHAR NOT NULL,
     L_SHIPDATE DATE NOT NULL,
     L_COMMITDATE DATE NOT NULL,
     L_RECEIPTDATE DATE NOT NULL,
     L_SHIPINSTRUCT CHAR(25) NOT NULL,
     L_SHIPMODE CHAR(10) NOT NULL,
     L_COMMENT VARCHAR(44) NOT NULL
     )
     WITH (
     LOCATION='tpch.lineitem',
     DATA_SOURCE=TeradataInstance
     );
     ```

1. Cree estadísticas en una tabla externa para un rendimiento optimizado.

     ```sql
      CREATE STATISTICS LineitemOrderKeyStatistics ON teradata.lineitem(L_ORDERKEY) WITH FULLSCAN; 
      ```



## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
