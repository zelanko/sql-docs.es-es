---
title: Configurar PolyBase para acceder a datos externos en SQL Server | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: e71fc7c603ad5ca975a3e55ee1bbd41601b85387
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816773"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar PolyBase para acceder a datos externos en SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se explica cómo usar PolyBase en una instancia de SQL Server para consultar datos externos en otra instancia de SQL Server.

## <a name="prerequisites"></a>Prerequisites

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md). En el artículo de instalación se explican los requisitos previos. Una vez instalado, asegúrese también de [habilitar PolyBase.](polybase-installation.md#enable)

Se debe crear una [Clave maestra](../../t-sql/statements/create-master-key-transact-sql.md) antes de crear una credencial de ámbito de base de datos. 

## <a name="configure-a-sql-server-external-data-source"></a>Configuración de un origen de datos externos de SQL Server

Para consultar los datos de un origen de datos de SQL Server, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear estas tablas externas. 
 
Para obtener un rendimiento óptimo de las consultas, cree estadísticas en las columnas de tabla externa, sobre todo en las que se usan para las combinaciones, los filtros y los agregados.

En esta sección se utilizan los siguientes comandos de Transact-SQL:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Cree una credencial de ámbito de base de datos para acceder al origen de SQL Server. En el ejemplo siguiente se crea una credencial para el origen de datos externo con `IDENTITY = 'username'` y `SECRET = 'password'`.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials
    WITH IDENTITY = 'username', SECRET = 'password';
    ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). En el ejemplo siguiente:

   - Se crea un origen de datos externo denominado `SQLServerInstance`.
   - Se identifica el origen de datos externo (`LOCATION = '<vendor>://<server>[:<port>]'`). En el ejemplo, se apunta a una instancia predeterminada de SQL Server.
   - Se identifica si el cálculo se debe insertar en el origen (`PUSHDOWN`). `PUSHDOWN` es `ON` de forma predeterminada.

   Por último, en el ejemplo se usa la credencial creada antes.

    ```sql
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
        WITH ( LOCATION = 'sqlserver://SqlServer',
        PUSHDOWN = ON,
        CREDENTIAL = SQLServerCredentials);
    ```

1. Opcionalmente, cree estadísticas en una tabla externa.

  Para obtener un rendimiento óptimo de las consultas, cree estadísticas en las columnas de tabla externa, sobre todo las que se usan para combinaciones, filtros y agregados.

  ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY)
    WITH FULLSCAN;
  ```

>[!IMPORTANT] 
>Una vez que se haya creado un origen de datos externos, se puede usar el comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para crear una tabla consultable a través de ese origen.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]


## <a name="sql-server-connector-compatible-types"></a>Tipos compatibles con el Conector de SQL Server

Puede realizar una conexión con otros orígenes de datos que reconozca una conexión de SQL Server. Use el conector de SQL Server PolyBase para crear una tabla externa de Azure SQL Data Warehouse y Azure SQL Database. Para realizar esta tarea, siga los mismos pasos indicados anteriormente. Asegúrese de que la credencial de ámbito de base de datos, la dirección del servidor, el puerto y la cadena de ubicación se correspondan con los del origen de datos compatible al que quiere conectarse.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
