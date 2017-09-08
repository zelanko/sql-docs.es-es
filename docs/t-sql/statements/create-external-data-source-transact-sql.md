---
title: Crear origen de datos externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.assetid: 75d8a220-0f4d-4d91-8ba4-9d852b945509
caps.latest.revision: 58
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 477d2f682da2c91ba8e4bfd42186c4b1b9735f85
ms.contentlocale: es-es
ms.lasthandoff: 09/06/2017

---
# <a name="create-external-data-source-transact-sql"></a>Crear origen de datos externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Crea un origen de datos externo para PolyBase, las consultas de base de datos elástica o almacenamiento de blobs de Azure. Según el escenario, la sintaxis difiere significativamente. No se puede usar un origen de datos creado para PolyBase para las consultas de base de datos elástica.  De forma similar, no se puede usar un origen de datos creado para las consultas de bases de datos elásticas de PolyBase, etcetera. 
  
> [!NOTE]  
>  PolyBase solo se admite en SQL Server 2016, almacenamiento de datos de SQL Azure y almacenamiento de datos paralelos. Consultas de bases de datos elásticas se admiten únicamente en la base de datos de SQL Azure v12 o posterior.  
  
 Para escenarios de PolyBase, el origen de datos externo es un sistema de archivos de Hadoop (HDFS), un contenedor de blobs de almacenamiento de Azure o almacén de Azure Data Lake. Para obtener más información, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 Para escenarios de consulta de base de datos elástica, el origen externo es un administrador de mapa de particiones (en la base de datos de SQL Azure) o una base de datos remoto (en la base de datos de SQL Azure).  Use [sp_execute_remote &#40; Base de datos SQL Azure &#41; ](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md) después de crear un origen de datos externo. Para obtener más información, consulte [consulta de base de datos elástica](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  

  Origen de los datos externos de almacenamiento de blobs de Azure admite `BULK INSERT` y `OPENROWSET` sintaxis y es diferente de almacenamiento de blobs de Azure para PolyBase.
    
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
 *data_source_name* especifica el nombre del origen de datos definido por el usuario. El nombre debe ser único dentro de la base de datos en SQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL Azure. El nombre debe ser único dentro del servidor de almacenamiento de datos paralelos.
  
 TIPO = [HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 Especifica el tipo de origen de datos. Utilice HADOOP cuando el origen de datos externo es Hadoop o blobs de almacenamiento de Azure para Hadoop. Use SHARD_MAP_MANAGER al crear un origen de datos externo para la consulta de base de datos elástico de particionamiento en base de datos de SQL Azure. Usar RDBMS con orígenes de datos externos para las consultas entre bases de datos con consultas de base de datos elástica en la base de datos de SQL Azure.  Utilizar BLOB_STORAGE al realizar operaciones masivas utilizando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
  
UBICACIÓN = \<location_path > **HADOOP**    
Para HADOOP, especifica el indicador de recursos uniforme (URI) para un clúster de Hadoop.  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: Nombre de equipo o dirección IP del clúster de Hadoop Namenode.  
puerto: puerto el IPC Namenode. Esto se indica mediante el parámetro de configuración fs.default.name en Hadoop. Si no se especifica el valor, 8020 se usará de forma predeterminada.  
Ejemplo:`LOCATION = 'hdfs://10.10.10.10:8020'`

Para el almacenamiento de blobs de Azure con Hadoop, especifica el URI para conectarse al almacenamiento de blobs de Azure.  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb [s]: especifica el protocolo para el almacenamiento de blobs de Azure. [S] es opcional y especifica una conexión SSL segura; datos enviados desde SQL Server se cifran de forma segura a través del protocolo SSL. Se recomienda encarecidamente usar 'wasbs' en lugar de 'wasb'. Tenga en cuenta que la ubicación puede usar asv [s] en lugar de wasb [s]. La sintaxis de asv [s] está en desuso y se quitará en futuras versiones.  
contenedor: especifica el nombre del contenedor de almacenamiento de blobs de Azure. Para especificar el contenedor raíz de la cuenta de almacenamiento de un dominio, use el nombre de dominio en lugar del nombre del contenedor. Contenedores de raíz son de solo lectura, por lo que no se escriben datos en el contenedor.  
account_name: el nombre de dominio completo (FQDN) de la cuenta de almacenamiento de Azure.  
Ejemplo:`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Para el almacén de Azure Data Lake, ubicación especifica el URI para conectarse a su almacén de Azure Data Lake.



**SHARD_MAP_MANAGER**   
 Para SHARD_MAP_MANAGER, especifica el nombre del servidor lógico que hospeda el Administrador de mapa de particiones de base de datos de SQL Azure o una base de datos de SQL Server en una máquina virtual de Azure.
 
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

Para obtener un tutorial paso a paso, consulte [introducción con consultas elásticas de particionamiento (creación de particiones horizontales)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/).
  
**RDBMS**   
Para RDBMS, especifica el nombre del servidor lógico de la base de datos remoto en la base de datos de SQL Azure.  

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
  
Para obtener un tutorial paso a paso en RDBMS, consulte [introducción con consultas entre bases de datos (creación de particiones verticales)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/).  

**BLOB_STORAGE**   
Para operaciones masivas, `LOCATION` debe ser válido la dirección URL para el almacenamiento de blobs de Azure y contenedor. No coloque  **/** , nombre de archivo o compartido parámetros de la firma de acceso al final de la `LOCATION` dirección URL.   
La credencial usada, debe crearse con `SHARED ACCESS SIGNATURE` como la identidad. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Para obtener un ejemplo de acceso al almacenamiento de blobs, vea el ejemplo F de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md). 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*puerto*]'  
 Especifica la ubicación del Administrador de recursos de Hadoop. Cuando se especifica, el optimizador de consultas puede tomar una decisión basada en costos para procesar previamente los datos de una consulta de PolyBase mediante el uso de las capacidades de cálculo de Hadoop con MapReduce. Llama a la aplicación del predicado, esto puede reducir significativamente el volumen de datos transferidos entre Hadoop y SQL y, por tanto, mejorar el rendimiento de las consultas.  
  
 Cuando no se especifica, realiza la inserción de cálculo en Hadoop está deshabilitada para las consultas de PolyBase.  
 
Si no se especifica el puerto, el valor predeterminado se determina mediante la configuración actual para la configuración de la "conectividad de hadoop".

|Conectividad de Hadoop|Puerto de administrador de recursos predeterminado|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

Para obtener una lista completa de las distribuciones de Hadoop y versiones admitidas por cada valor de conectividad, consulte [configuración de PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).
  
> [!IMPORTANT]  
>  El valor RESOURCE_MANAGER_LOCATION es una cadena y no se valida cuando se crea el origen de datos externo. Si se especifica un valor incorrecto puede producirse retrasos futuros al tener acceso a la ubicación.  
  
 Ejemplos de Hadoop:  
  
-   Hortonworks HDP 2.0, 2.1 y 2.2. 2.3 en Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 en Windows:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0, 2.1, 2.2 y 2.3 en Linux:   
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
  
-   Cloudera 5.1 5.11 en Linux:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENCIAL = *credential_name*  
 Especifica una credencial de ámbito de base de datos para la autenticación en el origen de datos externo. Para obtener un ejemplo, vea [C. crear un origen de datos externos de almacenamiento de blobs de Azure](../../t-sql/statements/create-external-data-source-transact-sql.md#credential). Para crear una credencial, vea [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md). Tenga en cuenta que no se requiere para los conjuntos de datos públicos que permite el acceso anónimo CREDENCIAL. 
  
 Database_name = *'QueryDatabaseName'*  
 El nombre de la base de datos que funciona como el Administrador de mapa de particiones (para SHARD_MAP_MANAGER) o la base de datos remoto (para RDBMS).  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 Para SHARD_MAP_MANAGER solo. El nombre de la asignación de particiones. Para obtener más información acerca de cómo crear un mapa de particiones, vea [Introducción a la consulta de base de datos elástica](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>Notas específicas de PolyBase  
Para obtener una lista completa de los orígenes de datos externos compatibles, consulte [configuración de PolyBase (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

 Para usar PolyBase, debe crear estos tres objetos:  
  
-   Un origen de datos externo.  
  
-   Un formato de archivo externo, y  
  
-   Una tabla externa que hace referencia al origen de datos externo y el formato de archivo externo.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en la base de datos de almacenamiento de datos de SQL, SQL Server, APS 2016 y base de datos SQL.

> [!IMPORTANT]  
>  En versiones anteriores de PDW, crear permisos de ALTER ANY EXTERNAL DATA SOURCE de requiere el origen de datos externos.
  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si los orígenes de datos de Hadoop externos no son coherentes respecto al RESOURCE_MANAGER_LOCATION definido, se producirá un error de tiempo de ejecución. Es decir, no puede especificar dos orígenes de datos externos que hacen referencia el mismo clúster de Hadoop y, a continuación, proporcionar la ubicación del Administrador de recursos en uno y no en el otro.  
  
 El motor de SQL no comprueba la existencia de origen de datos externo cuando crea el objeto de origen de datos externo. Si el origen de datos no existe durante la ejecución de la consulta, se producirá un error.  
  
## <a name="general-remarks"></a>Notas generales  
Polybase, el origen de datos externo es de ámbito de base de datos en SQL Server y almacenamiento de datos SQL. Queda centrada en el servidor de almacenamiento de datos paralelos.
  
Polybase, cuando se define RESOURCE_MANAGER_LOCATION o JOB_TRACKER_LOCATION, el optimizador de consultas considera que optimizar cada consulta mediante la realización de un mapa de reducir el trabajo en el origen externo de Hadoop y la inserción de cálculo. Esto es totalmente una decisión basada en costos.  

Para asegurarse de que las consultas de PolyBase con éxito en caso de conmutación por error de Hadoop NameNode, considere el uso de una dirección IP virtual para el NameNode del clúster de Hadoop. Si no usa una dirección IP virtual para el Hadoop NameNode, si se produce una conmutación por error de Hadoop NameNode tendrá al objeto ALTER EXTERNAL DATA SOURCE para que apunte a la nueva ubicación.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Todos los orígenes de datos definidos en la misma ubicación de clúster de Hadoop deben usar la misma configuración de RESOURCE_MANAGER_LOCATION o JOB_TRACKER_LOCATION. Si no hay incoherencias, se producirá un error en tiempo de ejecución.  
  
 Si el clúster de Hadoop se configura con un nombre y el origen de datos externo utiliza la dirección IP para la ubicación de clúster, PolyBase todavía debe ser capaz de resolver el nombre del clúster cuando se utiliza el origen de datos. Para resolver el nombre, debe habilitar un reenviador DNS.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto de origen de datos externo.  
  
##  <a name="examples"></a>Ejemplos: SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Crear origen de datos externo para referencia Hadoop  
Para crear un origen de datos externo para hacer referencia a su clúster Hortonworks o Cloudera Hadoop, especifique el nombre de equipo o dirección IP del puerto y Hadoop Namenode.  
  
```tsql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. Crear origen de datos externos en Hadoop de referencia con la aplicación habilitada  
Especifique la opción RESOURCE_MANAGER_LOCATION para habilitar el cálculo de inserción a Hadoop para las consultas de PolyBase. Una vez habilitada, PolyBase usa una decisión basada en costos para determinar si el cálculo de la consulta se debe aplicar en Hadoop o se deben mover todos los datos para procesar la consulta en SQL Server.
  
```tsql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. Crear origen de datos externo para hacer referencia a Hadoop protegido con Kerberos  
Para comprobar si el clúster de Hadoop protegido con Kerberos, compruebe el valor de propiedad hadoop.security.authentication en Hadoop core-site.xml. Para hacer referencia a un clúster de Hadoop protegido con Kerberos, debe especificar una credencial de ámbito de la base de datos que contiene el nombre de usuario de Kerberos y la contraseña. La clave maestra de base de datos se utiliza para cifrar el secreto de credencial con ámbito de base de datos. 
  
```tsql  
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

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Crear origen de datos externo para hacer referencia a almacenamiento de blobs de Azure
Para crear un origen de datos externo para hacer referencia a su contenedor de almacenamiento de blobs de Azure, especifique el URI de almacenamiento de blobs de Azure y una credencial de ámbito de la base de datos que contiene la clave de cuenta de almacenamiento de Azure.

En este ejemplo, el origen de datos externo es un contenedor de almacenamiento de blobs de Azure denominado dailylogs bajo la cuenta de almacenamiento de Azure denominada myaccount. El almacenamiento de Azure es el origen de datos externo para la transferencia de datos solo; y no admite la aplicación del predicado.

En este ejemplo se muestra cómo crear la credencial de ámbito de la base de datos para la autenticación al almacenamiento de Azure. Especifique la clave de cuenta de almacenamiento de Azure en el secreto de credencial de base de datos. Especifique cualquier cadena en base de datos con ámbito de nombre de la identidad, no se utiliza para la autenticación al almacenamiento de Azure. A continuación, se utiliza la credencial en la instrucción que crea un origen de datos externo.

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>Ejemplos: Base de datos SQL Azure

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. Crear un origen de datos externos del Administrador de mapa de particiones
Para crear un origen de datos externo para hacer referencia a un SHARD_MAP_MANAGER, especifique el nombre del servidor lógico que hospeda el Administrador de mapa de particiones de base de datos de SQL Azure o una base de datos de SQL Server en una máquina virtual de Azure.

```tsql
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

### <a name="f-create-an-rdbms-external-data-source"></a>F. Crear un origen de datos externo de RDBMS
Para crear un origen de datos externo para hacer referencia a un RDBMS, especifica el nombre del servidor lógico de la base de datos remoto en la base de datos de SQL Azure.

```tsql
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

## <a name="examples-azure-sql-data-warehouse"></a>Ejemplos: Almacenamiento de datos SQL Azure

### <a name="g-create-external-data-source-to-reference-azure-blob-storage"></a>G. Crear origen de datos externo para hacer referencia a almacenamiento de blobs de Azure
Para crear un origen de datos externo para hacer referencia a su contenedor de almacenamiento de blobs de Azure, especifique el URI de almacenamiento de blobs de Azure y una credencial de ámbito de la base de datos que contiene la clave de cuenta de almacenamiento de Azure.

En este ejemplo, el origen de datos externo es un contenedor de almacenamiento de blobs de Azure denominado dailylogs bajo la cuenta de almacenamiento de Azure denominada myaccount. El origen de datos externos de almacenamiento de Azure es para la transferencia de datos solo y no es compatible con la aplicación del predicado.

En este ejemplo se muestra cómo crear la credencial de ámbito de la base de datos para la autenticación al almacenamiento de Azure. Especifique la clave de cuenta de almacenamiento de Azure en el secreto de credencial de base de datos. Especifique cualquier cadena en base de datos con ámbito de nombre de la identidad, no se utiliza para la autenticación al almacenamiento de Azure. A continuación, se utiliza la credencial en la instrucción que crea un origen de datos externo.

```tsql
-- Create a database master key if one does not already exist. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage 
WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```
### <a name="h-create-external-data-source-to-reference-azure-data-lake-store"></a>H. Crear origen de datos externo para la referencia de almacén de Azure Data Lake
Conectividad de almacén de Data lake de Azure se basa en el URI de ADLS y entidad de seguridad de servicio de la aplicación Azure Active directory. Documentación para crear esta aplicación puede encontrarse en[autenticación de almacén de datos lake mediante Active Directory](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```tsql
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

### <a name="i-create-external-data-source-to-reference-hadoop"></a>I. Crear origen de datos externo para referencia Hadoop
Para crear un origen de datos externo para hacer referencia a su clúster Hortonworks o Cloudera Hadoop, especifique el nombre de equipo o dirección IP del puerto y Hadoop Namenode.

```tsql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);
```

### <a name="j-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>J. Crear origen de datos externos en Hadoop de referencia con la aplicación habilitada
Especifique la opción JOB_TRACKER_LOCATION para habilitar el cálculo de inserción a Hadoop para las consultas de PolyBase. Una vez habilitada, PolyBase usa una decisión basada en costos para determinar si el cálculo de la consulta se debe aplicar en Hadoop o se deben mover todos los datos para procesar la consulta en SQL Server. 

```tsql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="k-create-external-data-source-to-reference-azure-blob-storage"></a>K. Crear origen de datos externo para hacer referencia a almacenamiento de blobs de Azure
Para crear una referencia externa ubicación de origen de origen de datos para hacer referencia a su contenedor de almacenamiento de blobs de Azure, especifique el URI de almacenamiento de blobs de Azure como los datos externos. Agrega tu clave de cuenta de almacenamiento de Azure al archivo de core-site.xml PDW para la autenticación.

En este ejemplo, el origen de datos externo es un contenedor de almacenamiento de blobs de Azure denominado dailylogs bajo la cuenta de almacenamiento de Azure denominada myaccount. El origen de datos externos de almacenamiento de Azure es para la transferencia de datos solo y no es compatible con la aplicación del predicado.

```tsql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>Ejemplos: Las operaciones masivas   
### <a name="l-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>L. Crear un origen de datos externo para operaciones masivas recuperar datos desde almacenamiento de blobs de Azure.   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].   
Utilice el siguiente origen de datos para operaciones masivas utilizando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). La credencial usada, debe crearse con `SHARED ACCESS SIGNATURE` como la identidad. Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).   
```tsql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
Para ver este ejemplo en uso, consulte [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[MODIFICAR el origen de datos externo (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREAR AS de tabla externa SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[Crear tabla como SELECT &#40; Almacenamiento de datos SQL de Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[Sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  


