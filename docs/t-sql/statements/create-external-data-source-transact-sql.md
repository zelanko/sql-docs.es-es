---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9da6613c69319197da22b9b4cee74e8ef0b289d6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Crea un origen de datos externo para PolyBase, o bien consultas de Elastic Database. Según el escenario, la sintaxis difiere significativamente. No se puede usar un origen de datos externo creado para PolyBase para las consultas de Elastic Database.  Del mismo modo, no se puede usar un origen de datos externos creado para consultas de Elastic Database para PolyBase, etc. 
  
> [!NOTE]  
>  PolyBase solo se admite en SQL Server 2016 (o superior), Azure SQL Data Warehouse y Almacenamiento de datos paralelos. Las consultas de Elastic Database solo se admiten en Azure SQL Database v12 o una versión posterior.  
  
 Para escenarios de PolyBase, el origen de datos externo es un Sistema de archivos de Hadoop (HDFS), un contenedor de Azure Storage Blob o Azure Data Lake Store. Para obtener más información, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 Para escenarios de consultas de Elastic Database, el origen externo es un Shard Map Manager (en Azure SQL Database) o una base de datos remota (en Azure SQL Database).  Use [sp_execute_remote &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) después de crear un origen de datos externo. Para obtener más información, vea [Elastic Database query](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) (Consulta de Elastic Database).  

  El origen de datos externo de Azure Blob Storage admite la sintaxis de `BULK INSERT` y `OPENROWSET`, y es diferente a Azure Blob Storage para PolyBase.
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016 and Azure SQL Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, JOB_TRACKER_LOCATION = 'JobTracker_URI[:port]' ]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source 
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP,
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
    )
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_source_name* especifica el nombre definido por el usuario para el origen de datos. El nombre debe ser único dentro de la base de datos en SQL Server, Azure SQL Database y Azure SQL Data Warehouse. El nombre debe ser único dentro del servidor en Almacenamiento de datos paralelos.
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Especifica el tipo del origen de datos. Use HADOOP cuando el origen de datos externo sea Hadoop o Azure Storage Blob para Hadoop. Use SHARD_MAP_MANAGER al crear un origen de datos externo para la consulta de Elastic Database para el particionamiento en Azure SQL Database. Use RDBMS con orígenes de datos externos para consultas entre bases de datos con consultas de Elastic Database en Azure SQL Database.  Use BLOB_STORAGE al realizar operaciones masivas mediante [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
LOCATION = \<location_path> **HADOOP**    
Para HADOOP, especifica el identificador uniforme de recursos (URI) para un clúster de Hadoop.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: nombre de equipo o dirección IP del NameNode de clúster de Hadoop.  
port: puerto IPC de NameNode. Esto se indica mediante el parámetro de configuración fs.default.name en Hadoop. Si no se especifica el valor, se usará 8020 de forma predeterminada.  
Ejemplo: `LOCATION = 'hdfs://10.10.10.10:8020'`

Para Azure Blob Storage con Hadoop, especifica el URI para conectarse a Azure Blob Storage.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb[s]: especifica el protocolo para Azure Blob Storage. [s] es opcional y especifica una conexión SSL segura; los datos enviados desde SQL Server se cifran de forma segura a través del protocolo SSL. Se recomienda encarecidamente usar "wasbs" en lugar de "wasb". Tenga en cuenta que en la ubicación se puede usar asv[s] en lugar de wasb[s]. La sintaxis asv[s] ha quedado en desuso y se retirará en versiones posteriores.  
container: especifica el nombre del contenedor de Azure Blob Storage. Para especificar el contenedor raíz de la cuenta de almacenamiento de un dominio, use el nombre de dominio en lugar del nombre de contenedor. Los contenedores raíz son de solo lectura, por lo que no se pueden volver a escribir datos en el contenedor.  
account_name: el nombre de dominio completo (FQDN) de la cuenta de Azure Storage.  
Ejemplo: `LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Para Azure Data Lake Store, la ubicación especifica el URI para conectarse a Azure Data Lake Store.



**SHARD_MAP_MANAGER**   
 Para SHARD_MAP_MANAGER, especifica el nombre del servidor lógico que hospeda el administrador de mapa de particiones en Azure SQL Database o una base de datos de SQL Server en una máquina virtual de Azure.
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

Para obtener un tutorial paso a paso, vea [Getting started with elastic queries for sharding (horizontal partitioning)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/) [Introducción a las consultas elásticas para particionamiento (creación de particiones horizontales)].
  
**RDBMS**   
Para RDBMS, especifica el nombre del servidor lógico de la base de datos remota en Azure SQL Database.  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
Para obtener un tutorial paso a paso sobre RDBMS, vea [Introducción a las consultas entre bases de datos (particiones verticales)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Solo para operaciones masivas, `LOCATION` debe ser la dirección URL válida para Azure Blob Storage y el contenedor de blobs de Azure. No coloque **/**, el nombre de archivo o parámetros de firma de acceso compartido al final de la dirección URL de `LOCATION`.   
La credencial usada debe crearse mediante el uso de `SHARED ACCESS SIGNATURE` como identidad. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para obtener un ejemplo de acceso al almacenamiento de blobs, vea el ejemplo F de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 Especifica la ubicación del administrador de recursos de Hadoop. Cuando se especifica, el optimizador de consultas puede adoptar una decisión basada en el costo para realizar el procesamiento previo de los datos de una consulta de PolyBase mediante el uso de las funciones de cálculo de Hadoop con MapReduce. Esta técnica, denominada aplicación de predicado, puede reducir significativamente el volumen de datos transferidos entre Hadoop y SQL y, por tanto, mejorar el rendimiento de las consultas.  
  
 Cuando no se especifica, se deshabilita la inserción de cálculo en Hadoop para las consultas de PolyBase.  
 
Si no se especifica el puerto, el valor predeterminado se determina con el valor actual de la configuración de "conectividad de Hadoop".

|Conectividad de Hadoop|Puerto predeterminado del administrador de recursos|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Para obtener una lista completa de las distribuciones de Hadoop y las versiones admitidas por cada valor de conectividad, vea [Configuración de conectividad de PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  El valor RESOURCE_MANAGER_LOCATION es una cadena y no se valida cuando se crea el origen de datos externo. Si se especifica un valor incorrecto se pueden producir retrasos futuros al tener acceso a la ubicación.  
  
 Ejemplos de Hadoop:  
  
-   Hortonworks HDP 2.0, 2.1, 2.2. 2.3 en Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 en Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2, 2.3 en Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Hortonworks HDP 1.3 en Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Cloudera 4.3 en Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Cloudera 5.1 - 5.11 en Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = *credential_name*  
 Especifica una credencial de ámbito de base de datos para la autenticación en el origen de datos externo. Para obtener un ejemplo, vea [C. Creación de un origen de datos externos de Azure Blob Storage](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Para crear una credencial, vea [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Tenga en cuenta que CREDENTIAL no es obligatorio para los conjuntos de datos públicos en los que se permite el acceso anónimo. 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 El nombre de la base de datos que actúa como administrador de mapa de particiones (para SHARD_MAP_MANAGER) o la base de datos remota (para RDBMS).  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 Solo para SHARD_MAP_MANAGER. El nombre del mapa de particiones. Para obtener más información sobre cómo crear un mapa de particiones, vea [Getting started with Elastic Database query](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/) (Introducción a la consulta de Elastic Database)  
  
## <a name="polybase-specific-notes"></a>Notas específicas de PolyBase  
Para obtener una lista completa de los orígenes de datos externos compatibles, vea [Configuración de conectividad de PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Para usar PolyBase, debe crear estos tres objetos:  
  
-   Un origen de datos externo.  
  
-   Un formato de archivo externo.  
  
-   Una tabla externa que haga referencia al origen de datos externo y al formato de archivo externo.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en la base de datos en SQL DW, SQL Server, APS 2016 y SQL DB.

> [!IMPORTANT]  
>  En versiones anteriores de PDW, la creación del origen de datos externo requería los permisos ALTER ANY EXTERNAL DATA SOURCE.
  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si los orígenes de datos externos de Hadoop no son coherentes respecto a la definición de RESOURCE_MANAGER_LOCATION, se producirá un error de tiempo de ejecución. Es decir, no se pueden especificar dos orígenes de datos externos que hagan referencia el mismo clúster de Hadoop y después proporcionar la ubicación del administrador de recursos de uno y no del otro.  
  
 El motor de SQL no comprueba la existencia del origen de datos externo cuando crea el objeto de origen de datos externo. Si el origen de datos no existe durante la ejecución de la consulta, se producirá un error.  
  
## <a name="general-remarks"></a>Notas generales  
Para PolyBase, el origen de datos externo tiene ámbito de base de datos en SQL Server y SQL Data Warehouse. En Almacenamiento de datos paralelos tiene ámbito de servidor.
  
Para PolyBase, cuando se define RESOURCE_MANAGER_LOCATION o JOB_TRACKER_LOCATION, el optimizador de consultas considerará la optimización de cada consulta iniciando un trabajo de asignación/reducción en el origen externo de Hadoop e insertando el cálculo. Esta es una decisión basada totalmente en el costo.  

Para asegurarse de que las consultas de PolyBase son correctas en caso de conmutación por error del NameNode de Hadoop, considere la posibilidad de usar una dirección IP virtual para el NameNode de clúster de Hadoop. Si no usa una dirección IP virtual para el NameNode de Hadoop, en el caso de una conmutación por error del NameNode de Hadoop tendrá que apuntar el objeto ALTER EXTERNAL DATA SOURCE a la nueva ubicación.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Todos los orígenes de datos definidos en la misma ubicación de clúster de Hadoop deben usar la misma configuración de RESOURCE_MANAGER_LOCATION o JOB_TRACKER_LOCATION. Si hay incoherencias, se producirá un error en tiempo de ejecución.  
  
 Si el clúster de Hadoop se configura con un nombre y el origen de datos externo usa la dirección IP para la ubicación de clúster, PolyBase todavía debe ser capaz de resolver el nombre del clúster cuando se use el origen de datos. Para resolver el nombre, debe habilitar un reenviador DNS.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto EXTERNAL DATA SOURCE.  
  
##  <a name="examples"></a> Ejemplos: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Creación de un origen de datos externo para hacer referencia a Hadoop  
Para crear un origen de datos externo para hacer referencia al clúster de Hortonworks o Cloudera Hadoop, especifique el nombre de equipo o la dirección IP del NameNode y puerto de Hadoop.  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. Creación de un origen de datos externo para hacer referencia a Hadoop con la inserción habilitada  
Especifique la opción RESOURCE_MANAGER_LOCATION para habilitar la inserción de cálculo en Hadoop para las consultas de PolyBase. Una vez habilitada, PolyBase usa una decisión basada en costos para determinar si el cálculo de la consulta se debe aplicar en Hadoop o se deben mover todos los datos para procesar la consulta en SQL Server.
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Creación de un origen de datos externo para hacer referencia a Hadoop con protección de Kerberos  
Para comprobar si el clúster de Hadoop está protegido con Kerberos, compruebe el valor de la propiedad hadoop.security.authentication en core-site.xml de Hadoop. Para hacer referencia a un clúster de Hadoop protegido con Kerberos, debe especificar una credencial con ámbito de base de datos que contenga el nombre de usuario y la contraseña de Kerberos. La clave maestra de base de datos se usa para cifrar el secreto de la credencial de ámbito de base de datos. 
  
```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Creación de un origen de datos externo para hacer referencia a Azure Blob Storage
Para crear un origen de datos externo para hacer referencia al contenedor de Azure Blob Storage, especifique el URI de Azure Blob Storage y una credencial de ámbito de base de datos que contenga la clave de la cuenta de Azure Storage.

En este ejemplo, el origen de datos externo es un contenedor de Azure Blob Storage denominado dailylogs bajo la cuenta de Azure Storage denominada myaccount. El origen de datos externo de Azure Storage es solo para la transferencia de datos y no admite la aplicación del predicado.

En este ejemplo se muestra cómo crear la credencial de ámbito de base de datos para la autenticación en Azure Storage. Especifique la clave de la cuenta de Azure Storage en el secreto de la credencial de base de datos. Especifique cualquier cadena en la identidad de la credencial de ámbito de base de datos; no se usará para la autenticación en Azure Storage. Después, la credencial se usa en la instrucción que crea un origen de datos externo.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = BLOB_STORAGE, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>Ejemplos: Azure SQL Database

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Creación de un origen de datos externo de Administrador de mapa de particiones
Para crear un origen de datos externo para hacer referencia a un SHARD_MAP_MANAGER, especifique el nombre del servidor lógico que hospeda el administrador de mapa de particiones en Azure SQL Database o una base de datos de SQL Server en una máquina virtual de Azure.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>F. Creación de un origen de datos externo de RDBMS
Para crear un origen de datos externo para hacer referencia a RDBMS, especifique el nombre del servidor lógico de la base de datos remota en Azure SQL Database.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>Ejemplos: Azure SQL Data Warehouse

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. Creación de un origen de datos externo para hacer referencia a Azure Data Lake Store
La conectividad de Azure Data Lake Store se basa en el URI de ADLS y en la entidad de servicio de la aplicación de Azure Active Directory. La documentación para crear esta aplicación se puede encontrar en [Autenticación entre servicios: Data Lake Store con Azure Active Directory](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>Ejemplos: Almacenamiento de datos paralelos

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. Creación de un origen de datos externo para hacer referencia a Hadoop con la inserción habilitada
Especifique la opción JOB_TRACKER_LOCATION para habilitar la inserción de cálculo en Hadoop para las consultas de PolyBase. Una vez habilitada, PolyBase usa una decisión basada en costos para determinar si el cálculo de la consulta se debe aplicar en Hadoop o se deben mover todos los datos para procesar la consulta en SQL Server. 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. Creación de un origen de datos externo para hacer referencia a Azure Blob Storage
Para crear un origen de datos externo para hacer referencia al contenedor de Azure Blob Storage, especifique el URI de Azure Blob Storage como valor LOCATION del origen de datos externo. Agregue la clave de la cuenta de Azure Storage al archivo de core-site.xml de PDW para la autenticación.

En este ejemplo, el origen de datos externo es un contenedor de Azure Blob Storage denominado dailylogs bajo la cuenta de Azure Storage denominada myaccount. El origen de datos externo de Azure Storage es solo para la transferencia de datos y no admite la aplicación del predicado.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Ejemplos: operaciones masivas   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. Creación de un origen de datos externo para operaciones masivas de recuperación de datos desde Azure Blob Storage.   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Use el origen de datos siguiente para las operaciones masivas con [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). La credencial usada debe crearse mediante el uso de `SHARED ACCESS SIGNATURE` como identidad. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
Para ver este ejemplo en uso, vea [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md).
  
## <a name="see-also"></a>Ver también
[ALTER EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

