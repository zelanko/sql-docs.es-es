---
title: Configurar PolyBase para acceder a datos externos en MongoDB | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
ms.reviewer: mikeray
manager: craigg
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f255b2ed227bf1364a06a6b190eef5ac1793676b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730410"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>Configurar PolyBase para acceder a datos externos en MongoDB

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En el artículo se explica cómo usar PolyBase en una instancia de SQL Server para consultar datos externos en MongoDB.

## <a name="prerequisites"></a>Prerequisites

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md).

Se debe crear una [Clave maestra](../../t-sql/statements/create-master-key-transact-sql.md) antes de crear una credencial de ámbito de base de datos. 
    

## <a name="configure-a-mongodb-external-data-source"></a>Configuración de un origen de datos externos de MongoDB

Para consultar los datos de un origen de datos de MongoDB, se deben crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear estas tablas externas.

En esta sección se utilizan los siguientes comandos de Transact-SQL:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Cree una credencial de ámbito de base de datos para acceder al origen MongoDB.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```
1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = 'mongodb://<server>[:<port>]',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_name);
    ```

1. **Opcional:** Cree estadísticas en una tabla externa.

    Se recomienda crear estadísticas en las columnas de tabla externa, sobre todo en las que se usan para las combinaciones, filtros y agregados, para obtener un rendimiento óptimo de las consultas.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>Una vez que se haya creado un origen de datos externos, se puede usar el comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para crear una tabla consultable a través de ese origen. 

## <a name="flattening"></a>Acoplamiento
 El acoplamiento está habilitado para los datos anidados y repetidos de las colecciones de documentos de MongoDB. El usuario debe habilitar `create an external table` y especificar explícitamente un esquema relacional mediante colecciones de documentos de MongoDB que podrían tener datos anidados o repetidos. En hitos futuros se habilitará la detección automática de esquemas mediante colecciones de documentos de MongoDB.
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

## <a name="cosmos-db-connection"></a>Conexión de Cosmos DB

Con la API de Mongo de Cosmos DB y el conector de PolyBase de Mongo DB, puede crear una tabla externa de una **instancia de Cosmos DB**. Esto se consigue mediante los mismos pasos indicados arriba. Asegúrese de que la credencial de ámbito de base de datos, la dirección del servidor, el puerto y la cadena de ubicación reflejen los del servidor de Cosmos DB. 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
