---
title: Configurar PolyBase para acceder a datos externos en MongoDB | Microsoft Docs
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
ms.openlocfilehash: a51842a1682b5e02db4ea216bddefbabbf0a7f56
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874313"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>Configurar PolyBase para acceder a datos externos en MongoDB

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En el artículo se explica cómo usar PolyBase en una instancia de SQL Server para consultar datos externos en MongoDB.

## <a name="prerequisites"></a>Prerequisites

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md). En el artículo de instalación se explican los requisitos previos.

## <a name="configure-an-external-table"></a>Configurar una tabla externa

Para consultar los datos de un origen de datos de MongoDB, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear estas tablas externas.

Se recomienda crear estadísticas en las columnas de tabla externa, sobre todo en las que se usan para las combinaciones, filtros y agregados, para obtener un rendimiento óptimo de las consultas.

En esta sección se crearán estos objetos:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL)
- CREATE EXTERNAL TABLE (Transact-SQL)
- CREATE STATISTICS (Transact-SQL)

1.    Cree una clave maestra en la base de datos. Esto es necesario para cifrar el secreto de credencial.

      ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
      ```

1.   Cree una credencial de ámbito de base de datos.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL MongoDBCredentials 
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1.  Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). Especifique la ubicación del origen de datos externos y las credenciales del origen de datos de MongoDB.

     ```sql
     /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE MongoInstance
    WITH (
    LOCATION = mongodb://MongoServer,
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = MongoDBCredentials
    );
     ```

1. Crear esquemas para datos externos

     ```sql
     CREATE SCHEMA MongoDB;
     GO
     ```

1.  Cree tablas externas que representen los datos almacenados en el sistema de MongoDB externo [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

     ```sql
     /*  LOCATION: MongoDB table/view in '<database_name>.<schema_name>.<object_name>' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE MongoDB.orders(
     [O_ORDERKEY] DECIMAL(38) NOT NULL,
     [O_CUSTKEY] DECIMAL(38) NOT NULL,
     [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
     [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
     [O_ORDERDATE] DATETIME2(0) NOT NULL,
     [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
     LOCATION='TPCH..ORDERS',
     DATA_SOURCE= MongoDBInstance
     );
     ```

1. Cree estadísticas en una tabla externa para un rendimiento optimizado.

     ```sql
      CREATE STATISTICS OrdersOrderKeyStatistics ON MongoDB.orders(O_ORDERKEY) WITH FULLSCAN;
     ```

## <a name="flattening"></a>Acoplamiento
 El acoplamiento está habilitado para los datos anidados y los datos repetidos de las colecciones de documentos de MongoDB. El usuario debe habilitar la creación de una tabla externa y especificar explícitamente un esquema relacional mediante colecciones de documentos de MongoDB que podrían tener datos anidados o repetidos. En hitos futuros se habilitará la detección automática de esquemas mediante colecciones de documentos de MongoDB.
Los tipos de datos JSON anidados o repetidos se acoplarán del siguiente modo:

* Objeto: colección de pares clave-valor sin ordenar delimitada por llaves (anidadas)

   - Se creará una columna de tabla para cada clave de objeto

     * Nombre de columna: objectname_keyname

* Matriz: valores ordenados, separados por comas, entre corchetes (repetidos)

   - Se agregará una nueva fila de tabla para cada elemento de matriz

   - Se creará una columna por matriz para almacenar el índice del elemento de matriz

     * Nombre de columna: arrayname_index

     * Tipo de datos: bigint

Hay varios problemas potenciales con esta técnica. Dos de ellos son los siguientes:

* Un campo vacío repetido enmascarará de forma eficaz los datos contenidos en los campos planos del mismo registro.

* La presencia de varios campos repetidos puede dar lugar a un aumento considerable del número de filas generadas.

Como ejemplo, vamos a evaluar la serie de restaurantes del conjunto de datos de ejemplo de MongoDB almacenada en formato JSON no relacional. Cada restaurante tiene un campo de dirección anidado y una matriz de calificaciones asignada en días diferentes. En la siguiente ilustración se muestra un restaurante típico con una dirección anidada y calificaciones anidadas que se repiten.

![Acoplamiento de MongoDB](../../relational-databases/polybase/media/mongo-flattening.png "Acoplamiento de restaurantes de MongoDB")

La dirección del objeto se acoplará de la siguiente manera:

* El campo anidado restaurant.address.building se convierte en restaurant.address_building
* El campo anidado restaurant.address.coord se convierte en restaurant.address_coord
* El campo anidado restaurant.address.street se convierte en restaurant.address_street
* El campo anidado restaurant.address.zipcode se convierte en restaurant.address_zipcode

Las calificaciones de la matriz se acoplará de la siguiente manera:
| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |Un |2|
|1378857600000|Un |6|
|135898560000 |Un |10|
|1322006400000|Un |9|
|1299715200000 |B |14|

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
