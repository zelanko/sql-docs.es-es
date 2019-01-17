---
title: Configurar PolyBase para acceder a datos externos con tipos genéricos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 98e06e3199d4ce8750a4a5956aec6d97c141b33b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53214264"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar PolyBase para acceder a datos externos en SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

PolyBase en SQL Server 2019 permite conectarse a orígenes de datos compatibles con ODBC por medio del conector ODBC. 

## <a name="prerequisites"></a>Prerequisites

Nota: La característica solo funciona en SQL Server en Windows. 

Si no ha instalado PolyBase, consulte [Instalación de PolyBase](polybase-installation.md).

En primer lugar, descargue e instale el controlador ODBC del origen de datos al que quiere conectarse en cada uno de los nodos de PolyBase. Una vez que el controlador está instalado correctamente, puede verlo y probarlo desde el "Administrador de orígenes de datos ODBC".

![Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **IMPORTANTE:**
> 
> Para mejorar el rendimiento de las consultas, asegúrese de que el controlador tenga habilitada la agrupación de conexiones. Se puede hacer desde el "Administrador de orígenes de datos ODBC".
> 
> **Nota**
> 
> El nombre del controlador (ejemplo en un círculo arriba) debe especificarse al crear el origen de datos externo (paso 3 siguiente).

## <a name="create-an-external-table"></a>Crear una tabla externa

Para consultar los datos de un origen de datos ODBC, debe crear tablas externas que hagan referencia a los datos externos. En esta sección se proporciona código de ejemplo para crear tablas externas.

Estos objetos se crean en esta sección:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. Cree una clave maestra en la base de datos, si aún no hay ninguna. Esto es necesario para cifrar el secreto de credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>Argumentos
    PASSWORD ='password'

    Es la contraseña usada para cifrar la clave maestra de la base de datos. password debe cumplir los requisitos de la directiva de contraseñas de Windows del equipo que hospeda la instancia de SQL Server.

1. Cree una credencial de ámbito de base de datos para acceder al origen de datos ODBC.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. Cree un origen de datos externo con [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

     ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'SSL=0;sslAllowInvalidCertificates=1;Driver={<Name of Installed Driver>};HOST=%s;AUTHMECH=0',
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );

     ```


1.  Cree tablas externas que representen los datos de un origen de datos externo mediante [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: ODBC data source table/view
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customer(
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
      LOCATION='customer',
      DATA_SOURCE= external_data_source_name
     );
      ```

1. **Opcional:** Cree estadísticas en una tabla externa.

    Se recomienda crear estadísticas en las columnas de tabla externa, sobre todo en las que se usan para las combinaciones, filtros y agregados, para obtener un rendimiento óptimo de las consultas.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre PolyBase, consulte la [información general de SQL Server PolyBase](polybase-guide.md).
