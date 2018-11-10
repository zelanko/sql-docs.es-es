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
ms.openlocfilehash: 7abd9873b3aeefb5644ade0497fe89c47d7cd343
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757960"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>Configurar PolyBase para obtener acceso a datos externos en Teradata

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo usar PolyBase en una instancia de SQL Server para consultar datos externos en Teradata.

## <a name="prerequisites"></a>Prerequisites

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md). En el artículo de instalación se explican los requisitos previos.

Para usar PolyBase en Teradata, se necesita VC++ Redistributable.
 
## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos de un origen de datos de Teradata, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear estas tablas externas. 

Estos objetos se crean en esta sección:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. Cree una clave maestra en la base de datos, si aún no hay ninguna. Se necesita una clave maestra para cifrar el secreto de credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    **Argumentos**

    PASSWORD ='password'

    Es la contraseña que se usa para cifrar la clave maestra en la base de datos. La contraseña debe cumplir los requisitos de la directiva de contraseñas de Windows del equipo que hospeda la instancia de SQL Server.

1. Cree una credencial de ámbito de base de datos.
 
     ```sql
     /*  specify credentials to external data source
      *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password'
     ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = teradata://<server address>[:<port>],
   -- PUSHDOWN = ON | OFF,
    CREDENTIAL =credential_name
    );

     ```

1.  Cree tablas externas que representen los datos almacenados en un sistema de Teradata externo con [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: Teradata table/view in '<database_name>.<object_name>' format
      *  DATA_SOURCE: the external data source, created above.
      */
     CREATE EXTERNAL TABLE customer(
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
     LOCATION='customer',
     DATA_SOURCE= external_data_source_name
     );
     ```

1. *Opcional:* cree estadísticas en una tabla externa.

    Para obtener un rendimiento óptimo de las consultas, cree estadísticas en las columnas de tabla externa, sobre todo las que se usan para las combinaciones, los filtros y los agregados.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
