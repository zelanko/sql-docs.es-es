---
title: 'Acceso a datos externos: Tipos genéricos de ODBC: PolyBase'
description: PolyBase en SQL Server permite conectarse a orígenes de datos compatibles por medio del conector ODBC. Instale el controlador ODBC y cree tablas externas.
ms.date: 02/19/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: c8bf01e39fb68d2315df2a441f7b2b4fefa81872
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246534"
---
# <a name="configure-polybase-to-access-external-data-with-odbc-generic-types"></a>Configuración de PolyBase para acceder a datos externos con tipos genéricos de ODBC

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

PolyBase en SQL Server 2019 permite conectarse a orígenes de datos compatibles con ODBC por medio del conector ODBC.

En este artículo se proporcionan algunos ejemplos del uso de un controlador ODBC. Consulte con el proveedor de ODBC para obtener ejemplos específicos. Consulte la documentación del controlador ODBC para el origen de datos con el fin de determinar las opciones de cadena de conexión apropiadas. Es posible que los ejemplos de este artículo no se apliquen a ningún controlador ODBC específico.

## <a name="prerequisites"></a>Prerrequisitos

>[!NOTE]
>Esta característica requiere SQL Server en Windows.

* [Instalación de PolyBase](polybase-installation.md).

* Se debe crear una [Clave maestra](../../t-sql/statements/create-master-key-transact-sql.md) antes de crear una credencial de ámbito de base de datos.

## <a name="install-the-odbc-driver"></a>Instalación del controlador ODBC

En primer lugar, descargue e instale el controlador ODBC del origen de datos al que quiere conectarse en cada uno de los nodos de PolyBase. Una vez que el controlador está instalado correctamente, puede verlo y probarlo desde el **Administrador de orígenes de datos ODBC**.

![Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

En el ejemplo anterior, el nombre del controlador aparece rodeado de un círculo rojo. Use este nombre al crear el origen de datos externo.

> [!IMPORTANT]
> Para mejorar el rendimiento de las consultas, habilite la agrupación de conexiones. Esto se puede hacer desde el **Administrador de orígenes de datos ODBC**.

## <a name="create-an-external-table"></a>Crear una tabla externa

Para consultar los datos de un origen de datos ODBC, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear tablas externas.

En esta sección se utilizan los siguientes comandos de Transact-SQL:

* [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
* [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Cree una credencial de ámbito de base de datos para acceder al origen de datos ODBC.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL <credential_name> WITH IDENTITY = '<username>', Secret = '<password>';
    ```

    Por ejemplo, en el ejemplo siguiente se crea una credencial denominada `credential_name`, con una identidad de `username` y una contraseña compleja.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'BycA4ZjrE#*2W%!';
    ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    CREATE EXTERNAL DATA SOURCE <external_data_source_name>
    WITH ( LOCATION = 'odbc://<ODBC server address>[:<port>]',
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = [ON] | OFF,
    CREDENTIAL = <credential_name> );
    ```

    En el ejemplo siguiente se crea un origen de datos externo:
    * Con el nombre `external_data_source_name`
    * Se encuentra en el `SERVERNAME` ODBC y el puerto `4444`
    * Se conecta con `CData ODBC Driver For SAP 2015`: es el controlador creado en [Instalación del controlador ODBC](#install-the-odbc-driver)
    * En `ServerNode` `sap_server_node`, puerto `5555`
    * Configurado para el procesamiento que se inserta en el servidor (`PUSHDOWN = ON`)
    * Mediante la credencial `credential_name`

    ```sql
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = 'odbc://SERVERNAME:4444',
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
    ```

1. **Opcional:** Cree estadísticas en una tabla externa.

    Para obtener un rendimiento óptimo de las consultas, se recomienda crear estadísticas en las columnas de tabla externa, sobre todo en las que se usan para combinaciones, filtros y agregados.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT]
>Una vez que se haya creado un origen de datos externo, use el comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para crear una tabla consultable a través de ese origen.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
