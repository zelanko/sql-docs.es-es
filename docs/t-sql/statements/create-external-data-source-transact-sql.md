---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a927964a3f3cf8fe5119011a430393330402a7aa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76516646"
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)

Crea un origen de datos externo para realizar consultas mediante SQL Server, SQL Database, Azure Synapse Analytics o Analytics Platform System (almacenamiento de datos paralelos o PDW).

En este artículo se proporciona la sintaxis, argumentos, comentarios, permisos y ejemplos para cualquier producto SQL que elija.

Para obtener más información sobre las convenciones de sintaxis, vea [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="click-a-product"></a>Haga clic en un producto.

En la siguiente fila, haga clic en cualquier nombre de producto que le interese. Al hacer clic, en esta página web se muestra otro contenido, adecuado para el producto que seleccione.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

|                               |                                                              |                                                              |                                                              |      |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| **_\* SQL Server \*_** &nbsp; | [SQL Database](create-external-data-source-transact-sql.md?view=azuresqldb-current) | [Azure Synapse<br />Analytics](create-external-data-source-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System (PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7) |      |
|                               |                                                              |                                                              |                                                              |      |

&nbsp;

## <a name="overview-sql-server"></a>Introducción: SQL Server

Crea un origen de datos externo para consultas de PolyBase. Los orígenes de datos externos se usan para establecer la conectividad y admiten estos casos de uso principales:

- Virtualización y carga de datos mediante [PolyBase][intro_pb]
- Operaciones de carga masiva con `BULK INSERT` o `OPENROWSET`

**SE APLICA A**: SQL Server 2016 (o posterior)

## <a name="syntax"></a>Sintaxis

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CONNECTION_OPTIONS        = '<name_value_pairs>']
[,   CREDENTIAL                = <credential_name> ]
[,   PUSHDOWN                  = ON | OFF]
[,   TYPE                      = HADOOP | BLOB_STORAGE ]
[,   RESOURCE_MANAGER_LOCATION = '<resource_manager>[:<port>]'
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica el nombre definido por el usuario para el origen de datos. El nombre debe ser único en la base de datos en SQL Server.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Proporciona el protocolo de conectividad y la ruta de acceso al origen de datos externo.

| Origen de datos externo    | Prefijo de ubicación | Ruta de acceso de ubicación                                         | Ubicaciones admitidas por producto o servicio |
| ----------------------- | --------------- | ----------------------------------------------------- | ---------------------------------------- |
| Cloudera o Hortonworks | `hdfs`          | `<Namenode>[:port]`                                   | SQL Server (2016 y versiones posteriores)                       |
| Azure Blob Storage      | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` | SQL Server (2016 y versiones posteriores)                       |
| SQL Server              | `sqlserver`     | `<server_name>[\<instance_name>][:port]`              | SQL Server (2019+)                       |
| Oracle                  | `oracle`        | `<server_name>[:port]`                                | SQL Server (2019+)                       |
| Teradata                | `teradata`      | `<server_name>[:port]`                                | SQL Server (2019+)                       |
| MongoDB o CosmosDB     | `mongodb`       | `<server_name>[:port]`                                | SQL Server (2019+)                       |
| ODBC                    | `odbc`          | `<server_name>[:port]`                                | SQL Server (2019+): solo Windows        |
| Operaciones masivas         | `https`         | `<storage_account>.blob.core.windows.net/<container>` | SQL Server (2017 y versiones posteriores)                       |

Ruta de acceso de ubicación:

- `<`NameNode`>`: nombre de equipo, nombre de URI de servicio o dirección IP del `Namenode` en el clúster de Hadoop. PolyBase debe resolver los nombres DNS utilizados por el clúster de Hadoop. <!-- For highly available Hadoop configurations, provide the Nameservice ID as the `LOCATION`. -->
- `port` = el puerto en el cual escucha el origen de datos externo. En Hadoop, el puerto se puede encontrar mediante el parámetro de configuración `fs.defaultFS`. El valor predeterminado es 8020.
- `<container>` = el contenedor de la cuenta de almacenamiento que contiene los datos. Los contenedores raíz son de solo lectura, no se pueden volver a escribir datos en el contenedor.
- `<storage_account>` = el nombre de la cuenta de almacenamiento del recurso de Azure.
- `<server_name>` = el nombre de host.
- `<instance_name>` = el nombre de la instancia con nombre de SQL Server. Se usa si tiene el servicio de SQL Server Browser en ejecución en la instancia de destino.

Instrucciones y notas adicionales cuando se establece la ubicación:

- El motor de SQL no comprueba la existencia del origen de datos externo cuando se crea el objeto. Para la validación, crea una tabla externa utilizando el origen de datos externo.
- Para garantizar una semántica de consulta coherente, use el mismo origen de datos externo para todas las tablas cuando realice consultas a Hadoop.
- Puede usar el prefijo de ubicación `sqlserver` para conectar SQL Server 2019 a SQL Server, SQL Database o Azure Synapse Analytics.
- Especifique `Driver={<Name of Driver>}` al conectarse a través de `ODBC`.
- `wasb` es el protocolo predeterminado para Azure Blob Storage. `wasbs` es opcional pero recomendado, ya que se enviarán los datos mediante una conexión SSL segura.
- Para garantizar que las consultas de PolyBase son correctas durante una conmutación por error del `Namenode` de Hadoop, considere la posibilidad de usar una dirección IP virtual para el `Namenode` del clúster de Hadoop. Si no, ejecute un comando [ALTER EXTERNAL DATA SOURCE][alter_eds] para que apunte a la nueva ubicación.

### <a name="connection_options--key_value_pair"></a>CONNECTION_OPTIONS = *key_value_pair*

Especifica opciones adicionales al conectarse a través de `ODBC` a un origen de datos externo.

Se requiere como mínimo el nombre del controlador, pero existen otras opciones, como `APP='<your_application_name>'` o `ApplicationIntent= ReadOnly|ReadWrite`, que también resulta útil establecerlas y pueden ayudarle con la solución de problemas.

Consulte la documentación del producto `ODBC` para obtener una lista de [CONNECTION_OPTIONS][connection_options] permitidas.

### <a name="pushdown--on--off"></a>PUSHDOWN = *ON | OFF*

Indica si se puede insertar cálculo en el origen de datos externo. El valor predeterminado es ON.

`PUSHDOWN` se admite al conectarse a SQL Server, Oracle, Teradata, MongoDB u ODBC en el nivel de origen de datos externo.

Habilitar o deshabilitar la inserción en el nivel de consulta se logra a través de una [sugerencia][hint_pb].

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica una credencial de ámbito de base de datos para la autenticación en el origen de datos externo.

Instrucciones y notas adicionales cuando se crea una credencial:

- `CREDENTIAL` solo es necesario si se ha protegido el blob. `CREDENTIAL` no es necesario para los conjuntos de datos que permiten el acceso anónimo.
- Cuando `TYPE` = `BLOB_STORAGE`, la credencial debe crearse mediante el uso de `SHARED ACCESS SIGNATURE` como identidad. Además, el token de SAS debe configurarse del modo siguiente:
  - Excluir el `?` inicial cuando se configura como secreto
  - Disponer de al menos permiso de lectura en el archivo que se debe cargar (por ejemplo `srt=o&sp=r`)
  - Usar un período de caducidad válido (todas las fechas se encuentran en hora UTC).

Para obtener un ejemplo del uso de `CREDENTIAL` con `SHARED ACCESS SIGNATURE` y `TYPE` = `BLOB_STORAGE`, vea [Creación de un origen de datos externo para ejecutar operaciones masivas y recuperar datos desde Azure Blob Storage en SQL Database](#g-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage).

Para crear una credencial con ámbito de base de datos, vea [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc].

### <a name="type---hadoop--blob_storage-"></a>TYPE = *[ HADOOP | BLOB_STORAGE ]*

Especifica el tipo de origen de datos externo que se está configurando. Este parámetro no siempre es necesario.

- Use HADOOP cuando el origen de datos externo sea Cloudera, Hortonworks o Azure Blob Storage.
- Use BLOB_STORAGE al ejecutar operaciones masivas con [BULK INSERT][bulk_insert] o con [OPENROWSET][openrowset] con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].

> [!IMPORTANT]
> No establezca `TYPE` si usa cualquier otro origen de datos externo.

Para obtener un ejemplo del uso de `TYPE` = `HADOOP` para cargar datos desde Azure Blob Storage, vea [Creación de un origen de datos externo para hacer referencia a Azure Blob Storage](#e-create-external-data-source-to-reference-azure-blob-storage).

### <a name="resource_manager_location--resourcemanager_uriport"></a>RESOURCE_MANAGER_LOCATION = *'ResourceManager_URI[:port]'*

Configure este valor opcional al conectarse a Hortonworks o Cloudera.

Cuando `RESOURCE_MANAGER_LOCATION` está definido, el optimizador de consultas toma una decisión basada en el coste para mejorar el rendimiento. Se puede usar un trabajo de MapReduce para insertar el cálculo en Hadoop. La especificación de `RESOURCE_MANAGER_LOCATION` puede reducir significativamente el volumen de datos transferidos entre Hadoop y SQL, lo cual puede suponer una mejora en el rendimiento de las consultas.

Si no se especifica el administrador de recursos, se deshabilita la inserción de cálculo en Hadoop para las consultas de PolyBase.

Si no se especifica el puerto, el valor predeterminado se elige mediante el valor actual de la configuración "hadoop connectivity".

| Conectividad de Hadoop | Puerto predeterminado del administrador de recursos |
| ------------------- | ----------------------------- |
| 1                   | 50300                         |
| 2                   | 50300                         |
| 3                   | 8021                          |
| 4                   | 8032                          |
| 5                   | 8050                          |
| 6                   | 8032                          |
| 7                   | 8050                          |

Para obtener una lista completa de las versiones de Hadoop compatibles, vea [Configuración de conectividad de PolyBase (Transact-SQL)][connectivity_pb].

> [!IMPORTANT]  
> El valor RESOURCE_MANAGER_LOCATION no se valida cuando se crea el origen de datos externo. Escribir un valor incorrecto puede provocar un error de consulta en tiempo de ejecución cada vez que se intente la inserción, ya que el valor proporcionado no podrá realizar la resolución.

En [Creación de un origen de datos externo para hacer referencia a Hadoop con la inserción habilitada](#c-create-external-data-source-to-reference-hadoop-with-push-down-enabled) se proporciona un ejemplo concreto y más instrucciones.

## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL en la base de datos en SQL Server.

## <a name="locking"></a>Bloqueo

Toma un bloqueo compartido en el objeto EXTERNAL DATA SOURCE.

## <a name="security"></a>Seguridad

PolyBase es compatible con la autenticación basada en proxy para la mayoría de orígenes de datos externos. Cree una credencial con ámbito de base de datos para crear la cuenta de proxy.

Cuando se conecta al almacenamiento o el grupo de datos en un clúster de macrodatos de SQL Server, las credenciales del usuario se pasan a través del sistema back-end. Cree inicios de sesión en el propio grupo de datos para habilitar la autenticación de paso a través.

Actualmente no se admite un token de SAS con tipo `HADOOP`. Solo se admite con una clave de acceso de cuenta de almacenamiento. Si se intenta crear un origen de datos externo con el tipo `HADOOP` y una credencial SAS, aparece un error como el siguiente:

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples-sql-server-2016"></a>Ejemplos: SQL Server (2016 y versiones posteriores)

> [!IMPORTANT]
> Para obtener información sobre cómo instalar y habilitar PolyBase, vea [Instalación de PolyBase en Windows](../../relational-databases/polybase/polybase-installation.md)

### <a name="a-create-external-data-source-in-sql-2019-to-reference-oracle"></a>A. Creación de un origen de datos externo en SQL 2019 para hacer referencia a Oracle

Para crear un origen de datos externo que haga referencia a Oracle, asegúrese de que tiene una credencial con ámbito de base de datos. También, opcionalmente, puede habilitar o deshabilitar la inserción de cálculo en este origen de datos.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '!MyC0mpl3xP@ssw0rd!'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL OracleProxyAccount
WITH
     IDENTITY   = 'oracle_username'
,    SECRET     = 'oracle_password'
;

CREATE EXTERNAL DATA SOURCE MyOracleServer
WITH
(    LOCATION   = 'oracle://145.145.145.145:1521'
,    CREDENTIAL = OracleProxyAccount
,    PUSHDOWN   = ON
,    TYPE=BLOB_STORAGE
)
;
```

Para ver más ejemplos de otros orígenes de datos, como MongoDB, vea [Configurar PolyBase para acceder a datos externos en MongoDB][mongodb_pb].

### <a name="b-create-external-data-source-to-reference-hadoop"></a>B. Creación de un origen de datos externo para hacer referencia a Hadoop

Para crear un origen de datos externo para hacer referencia al clúster de Hortonworks o Cloudera Hadoop, especifique el nombre de equipo o la dirección IP de `Namenode` de Hadoop y el puerto. <!-- Provide the Nameservice ID as the `LOCATION` for highly available configurations. -->

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION = 'hdfs://10.10.10.10:8050'
,    TYPE     = HADOOP
)
;
```

### <a name="c-create-external-data-source-to-reference-hadoop-with-push-down-enabled"></a>C. Creación de un origen de datos externo para hacer referencia a Hadoop con la inserción habilitada

Especifique la opción `RESOURCE_MANAGER_LOCATION` para habilitar la inserción de cálculo en Hadoop para las consultas de PolyBase. Una vez habilitado, PolyBase toma una decisión basada en el coste para determinar si se debe aplicar el cálculo de la consulta en Hadoop.

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8020'
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="d-create-external-data-source-to-reference-kerberos-secured-hadoop"></a>D. Creación de un origen de datos externo para hacer referencia a Hadoop con protección de Kerberos

Para comprobar si el clúster de Hadoop está protegido con Kerberos, compruebe el valor de la propiedad hadoop.security.authentication en core-site.xml de Hadoop. Para hacer referencia a un clúster de Hadoop protegido con Kerberos, debe especificar una credencial con ámbito de base de datos que contenga el nombre de usuario y la contraseña de Kerberos. La clave maestra de base de datos se usa para cifrar el secreto de la credencial de ámbito de base de datos.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
WITH
     IDENTITY   = '<hadoop_user_name>'
,    SECRET     = '<hadoop_password>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8050'
,    CREDENTIAL                = HadoopUser1
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="e-create-external-data-source-to-reference-azure-blob-storage"></a>E. Creación de un origen de datos externo para hacer referencia a Azure Blob Storage

En este ejemplo, el origen de datos externo es un contenedor de Azure Blob Storage denominado `daily` bajo la cuenta de Azure Storage denominada `logs`. El origen de datos externo de Azure Storage es solo para la transferencia de datos. No admite la inserción de predicado.

En este ejemplo se muestra cómo crear la credencial de ámbito de base de datos para la autenticación en Azure Storage. Especifique la clave de la cuenta de Azure Storage en el secreto de la credencial de base de datos. Puede especificar cualquier cadena en la identidad de la credencial con ámbito de base de datos, ya que no se usará para la autenticación en Azure Storage.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
     IDENTITY   = '<my_account>'
,    SECRET     = '<azure_storage_account_key>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
(    LOCATION   = 'wasbs://daily@logs.blob.core.windows.net/'
,    CREDENTIAL = AzureStorageCredential
,    TYPE       = HADOOP
)
;
```

### <a name="f-create-external-data-source-to-reference-a-sql-server-named-instance-via-polybase-connectivity-sql-2019"></a>F. Creación de un origen de datos externo para hacer referencia a una instancia con nombre de SQL Server a través de la conectividad de PolyBase (SQL 2019)

Para crear un origen de datos externo que haga referencia a una instancia con nombre de SQL Server, puede usar CONNECTION_OPTIONS para especificar el nombre de la instancia. En el ejemplo siguiente, WINSQL2019 es el nombre de host y SQL2019 es el nombre de la instancia.

```sql
CREATE EXTERNAL DATA SOURCE SQLServerInstance2
WITH (
  LOCATION = 'sqlserver://WINSQL2019',
  CONNECTION_OPTIONS = 'Server=%s\SQL2019',
  CREDENTIAL = SQLServerCredentials
);

```

Como alternativa, puede usar un puerto para conectarse a una instancia de SQL Server.

```sql
CREATE EXTERNAL DATA SOURCE SQLServerInstance2
WITH (
  LOCATION = 'sqlserver://WINSQL2019:58137',
  CREDENTIAL = SQLServerCredentials
);

```

## <a name="examples-bulk-operations"></a>Ejemplos: Operaciones masivas

> [!NOTE]
> No coloque un **/** final, nombre de archivo o parámetros de firma de acceso compartido al final de la URL de `LOCATION` al configurar un origen de datos externo para las operaciones masivas.

### <a name="g-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>G. Creación de un origen de datos externo para operaciones masivas de recuperación de datos desde Azure Blob Storage

**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
Use el origen de datos siguiente para las operaciones masivas con [BULK INSERT][bulk_insert] o [OPENROWSET][openrowset]. La credencial debe establecer `SHARED ACCESS SIGNATURE` como identidad, no debe tener al inicio `?` en el token de SAS, debe tener al menos permiso de lectura en el archivo que se debe cargar (por ejemplo `srt=o&sp=r`), y el período de expiración debe ser válido (todas las fechas se expresan en hora UTC). Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)][sas_token].

```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices
WITH
     IDENTITY = 'SHARED ACCESS SIGNATURE'
--   REMOVE ? FROM THE BEGINNING OF THE SAS TOKEN
,    SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************'
;

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
WITH
(    LOCATION   = 'https://newinvoices.blob.core.windows.net/week3'
,    CREDENTIAL = AccessAzureInvoices
,    TYPE       = BLOB_STORAGE
)
;
```

Para ver este ejemplo en uso, vea [BULK INSERT][bulk_insert_example].

## <a name="see-also"></a>Consulte también

- [ALTER EXTERNAL DATA SOURCE (Transact-SQL)][alter_eds]
- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT (Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Uso de firmas de acceso compartido (SAS)][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql

[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_eff]: https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-transact-sql
[create_etb_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-as-select-transact-sql?view=azure-sqldw-latest
[create_tbl_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=azure-sqldw-latest

[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql

[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown

<!-- Azure Docs -->
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

|                                                              |                                 |                                                              |                                                              |      |
| ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-2017) | **_\* SQL Database \*_** &nbsp; | [Azure Synapse<br />Analytics](create-external-data-source-transact-sql.md?view=azure-sqldw-latest) | [Analytics Platform<br />System (PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7) |      |
|                                                              |                                 |                                                              |                                                              |      |

&nbsp;

## <a name="overview-azure-sql-database"></a>Introducción: Azure SQL Database

Crea un origen de datos externo para consultas elásticas. Los orígenes de datos externos se usan para establecer la conectividad y admiten estos casos de uso principales:

- Operaciones de carga masiva con `BULK INSERT` o `OPENROWSET`
- Consultar instancias remotas de SQL Database o Azure Synapse utilizando SQL Database con [consulta elástica][remote_eq]
- Consultar una instancia de Azure SQL Database con particiones utilizando la [consulta elástica][sharded_eq]

## <a name="syntax"></a>Sintaxis

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CREDENTIAL                = <credential_name> ]
[,   TYPE                      = BLOB_STORAGE | RDBMS | SHARD_MAP_MANAGER ]
[,   DATABASE_NAME             = '<database_name>' ]
[,   SHARD_MAP_NAME            = '<shard_map_manager>' ]
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica el nombre definido por el usuario para el origen de datos. El nombre debe ser único en la base de datos en SQL Database.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Proporciona el protocolo de conectividad y la ruta de acceso al origen de datos externo.

| Origen de datos externo   | Prefijo de ubicación | Ruta de acceso de ubicación                                         |
| ---------------------- | --------------- | ----------------------------------------------------- |
| Operaciones masivas        | `https`         | `<storage_account>.blob.core.windows.net/<container>` |
| Consulta elástica (partición)  | No se requiere    | `<shard_map_server_name>.database.windows.net`        |
| Consulta elástica (remota) | No se requiere    | `<remote_server_name>.database.windows.net`           |

Ruta de acceso de ubicación:

- `<shard_map_server_name>` = el nombre del servidor lógico de Azure que hospeda el administrador del mapa de particiones. El argumento `DATABASE_NAME` proporciona la base de datos que se utiliza para hospedar el mapa de particiones y `SHARD_MAP_NAME` se utiliza para el propio mapa de particiones.
- `<remote_server_name>` = el nombre de servidor lógico de destino para la consulta elástica. El nombre de la base de datos se especifica utilizando el argumento `DATABASE_NAME`.

Instrucciones y notas adicionales cuando se establece la ubicación:

- El motor de SQL Database no comprueba la existencia del origen de datos externo cuando se crea el objeto. Para la validación, crea una tabla externa utilizando el origen de datos externo.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica una credencial de ámbito de base de datos para la autenticación en el origen de datos externo.

Instrucciones y notas adicionales cuando se crea una credencial:

- Para cargar datos desde Azure Blob Storage a SQL Database, use una clave de Azure Storage.
- `CREDENTIAL` solo es necesario si se ha protegido el blob. `CREDENTIAL` no es necesario para los conjuntos de datos que permiten el acceso anónimo.
- Cuando `TYPE` = `BLOB_STORAGE`, la credencial debe crearse mediante el uso de `SHARED ACCESS SIGNATURE` como identidad. Además, el token de SAS debe configurarse del modo siguiente:
  - Excluir el `?` inicial cuando se configura como secreto
  - Disponer de al menos permiso de lectura en el archivo que se debe cargar (por ejemplo `srt=o&sp=r`)
  - Usar un período de caducidad válido (todas las fechas se encuentran en hora UTC).

Para obtener un ejemplo del uso de `CREDENTIAL` con `SHARED ACCESS SIGNATURE` y `TYPE` = `BLOB_STORAGE`, vea [Creación de un origen de datos externo para ejecutar operaciones masivas y recuperar datos desde Azure Blob Storage en SQL Database](#c-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage).

Para crear una credencial con ámbito de base de datos, vea [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc].

### <a name="type---blob_storage--rdbms--shard_map_manager"></a>TYPE = *[ BLOB_STORAGE | RDBMS | SHARD_MAP_MANAGER]*

Especifica el tipo de origen de datos externo que se está configurando. Este parámetro no siempre es necesario.

- Use RDBMS para consultas entre bases de datos mediante una consulta elástica de SQL Database.
- Use SHARD_MAP_MANAGER al crear un origen de datos externo al conectarse a una base de datos SQL Database particionada.
- Use BLOB_STORAGE al ejecutar operaciones masivas con [BULK INSERT][bulk_insert] o con [OPENROWSET][openrowset].

> [!IMPORTANT]
> No establezca `TYPE` si usa cualquier otro origen de datos externo.

### <a name="database_name--database_name"></a>DATABASE_NAME = *database_name*

Configure este argumento cuando `TYPE` se haya establecido en `RDBMS` o `SHARD_MAP_MANAGER`.

| TYPE              | Valor de DATABASE_NAME                                       |
| ----------------- | ------------------------------------------------------------ |
| RDBMS             | El nombre de la base de datos remota en el servidor que se proporciona mediante `LOCATION` |
| SHARD_MAP_MANAGER | Nombre de la base de datos que funciona como administrador del mapa de particiones      |

Para obtener un ejemplo en el que se muestra cómo crear un origen de datos externo donde `TYPE` = `RDBMS`, consulte [Creación de un origen de datos externo de RDBMS](#b-create-an-rdbms-external-data-source).

### <a name="shard_map_name--shard_map_name"></a>SHARD_MAP_NAME = *shard_map_name*

Se usa cuando el `TYPE` argumento está establecido en `SHARD_MAP_MANAGER` únicamente para establecer el nombre del mapa de particiones.

Para ver un ejemplo en el que se muestra cómo crear un origen de datos externo donde `TYPE` = `SHARD_MAP_MANAGER`, consulte [Creación de un origen de datos externo de administrador de mapas de partición](#a-create-a-shard-map-manager-external-data-source).

## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL en la base de datos en SQL Database.

## <a name="locking"></a>Bloqueo

Toma un bloqueo compartido en el objeto EXTERNAL DATA SOURCE.

## <a name="examples"></a>Ejemplos:

### <a name="a-create-a-shard-map-manager-external-data-source"></a>A. Creación de un origen de datos externo de administrador de mapa de particiones

Para crear un origen de datos externo para hacer referencia a un SHARD_MAP_MANAGER, especifique el nombre del servidor de SQL Database que hospeda el administrador de mapa de particiones en SQL Database o una base de datos de SQL Server en una máquina virtual.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
WITH
     IDENTITY   = '<username>'
,    SECRET     = '<password>'
;

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc
WITH
(    TYPE             = SHARD_MAP_MANAGER
,    LOCATION         = '<server_name>.database.windows.net'
,    DATABASE_NAME    = 'ElasticScaleStarterKit_ShardMapManagerDb'
,    CREDENTIAL       = ElasticDBQueryCred
,    SHARD_MAP_NAME   = 'CustomerIDShardMap'
)
;
```

Para obtener un tutorial paso a paso, vea [Getting started with elastic queries for sharding (horizontal partitioning)][sharded_eq_tutorial] [Introducción a las consultas elásticas para particionamiento (creación de particiones horizontales)].

### <a name="b-create-an-rdbms-external-data-source"></a>B. Creación de un origen de datos externo de RDBMS

Para crear un origen de datos externo para hacer referencia a RDBMS, especifique el nombre del servidor de SQL Database de la base de datos remota en SQL Database.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential
WITH
     IDENTITY  = '<username>'
,    SECRET    = '<password>'
;

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc
WITH
(    TYPE          = RDBMS
,    LOCATION      = '<server_name>.database.windows.net'
,    DATABASE_NAME = 'Customers'
,    CREDENTIAL    = SQL_Credential
)
;
```

Para obtener un tutorial paso a paso sobre RDBMS, vea [Introducción a las consultas entre bases de datos (particiones verticales)][remote_eq_tutorial].

## <a name="examples-bulk-operations"></a>Ejemplos: Operaciones masivas

> [!NOTE]
> No coloque un **/** final, nombre de archivo o parámetros de firma de acceso compartido al final de la URL de `LOCATION` al configurar un origen de datos externo para las operaciones masivas.

### <a name="c-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>C. Creación de un origen de datos externo para operaciones masivas de recuperación de datos desde Azure Blob Storage

Use el origen de datos siguiente para las operaciones masivas con [BULK INSERT][bulk_insert] o [OPENROWSET][openrowset]. La credencial debe establecer `SHARED ACCESS SIGNATURE` como identidad, no debe tener al inicio `?` en el token de SAS, debe tener al menos permiso de lectura en el archivo que se debe cargar (por ejemplo `srt=o&sp=r`), y el período de expiración debe ser válido (todas las fechas se expresan en hora UTC). Para más información sobre las firmas de acceso compartido, vea [Uso de Firmas de acceso compartido (SAS)][sas_token].

```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices
WITH
     IDENTITY = 'SHARED ACCESS SIGNATURE'
--   REMOVE ? FROM THE BEGINNING OF THE SAS TOKEN
,    SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************'
;

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
WITH
(    LOCATION   = 'https://newinvoices.blob.core.windows.net/week3'
,    CREDENTIAL = AccessAzureInvoices
,    TYPE       = BLOB_STORAGE
)
;
```

Para ver este ejemplo en uso, vea [BULK INSERT][bulk_insert_example].

## <a name="see-also"></a>Consulte también

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Uso de firmas de acceso compartido (SAS)][sas_token]
- [Introducción a la consulta elástica][intro_eq]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql
[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql
[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/
[remote_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[remote_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[sharded_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/
[sharded_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/

<!-- Azure Docs -->
[azure_ad]: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

|                                                              |                                                              |                                            |                                                              |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ | ------------------------------------------------------------ | ---- |
| [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-2017) | [SQL Database](create-external-data-source-transact-sql.md?view=azuresqldb-current) | **_\* Azure Synapse<br />Analytics \*_** &nbsp; | [Analytics Platform<br />System (PDW)](create-external-data-source-transact-sql.md?view=aps-pdw-2016-au7) |      |
|                                                              |                                                              |                                            |                                                              |      |

&nbsp;

## <a name="overview-azure-synapse-analytics"></a>Introducción: Azure Synapse Analytics

Crea un origen de datos externo para PolyBase. Los orígenes de datos externos se usan para establecer la conectividad y admiten el siguiente caso de uso principal: Virtualización y carga de datos mediante [PolyBase][intro_pb]

> [!IMPORTANT]  
> Para crear un origen de datos de externo y consultar una instancia de SQL Analytics mediante Azure SQL Database con [consulta elástica][remote_eq], vea [SQL Database](create-external-data-source-transact-sql.md?view=azuresqldb-current).

## <a name="syntax"></a>Sintaxis

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CREDENTIAL                = <credential_name> ]
[,   TYPE                      =  HADOOP
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica el nombre definido por el usuario para el origen de datos. El nombre debe ser único en la base de datos de SQL en Azure Synapse.

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Proporciona el protocolo de conectividad y la ruta de acceso al origen de datos externo.

| Origen de datos externo        | Prefijo de ubicación | Ruta de acceso de ubicación                                         |
| --------------------------- | --------------- | ----------------------------------------------------- |
| Azure Blob Storage          | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` |
| Azure Data Lake Store Gen1 | `adl`           | `<storage_account>.azuredatalake.net`                 |
| Azure Data Lake Store Gen2 | `abfs[s]`       | `<container>@<storage_account>.dfs.core.windows.net`  |

Ruta de acceso de ubicación:

- `<container>` = el contenedor de la cuenta de almacenamiento que contiene los datos. Los contenedores raíz son de solo lectura, no se pueden volver a escribir datos en el contenedor.
- `<storage_account>` = el nombre de la cuenta de almacenamiento del recurso de Azure.

Instrucciones y notas adicionales cuando se establece la ubicación:

- La opción predeterminada consiste en usar `enable secure SSL connections` al aprovisionar Azure Data Lake Storage Gen 2. Si está habilitada, debe usar `abfss` al seleccionar una conexión SSL segura. Tenga en cuenta que `abfss` funciona también con conexiones SSL no seguras.
- Azure Synapse no comprueba la existencia del origen de datos externo cuando se crea el objeto. . Para la validación, crea una tabla externa utilizando el origen de datos externo.
- Para garantizar una semántica de consulta coherente, use el mismo origen de datos externo para todas las tablas cuando realice consultas a Hadoop.
- `wasb` es el protocolo predeterminado para Azure Blob Storage. `wasbs` es opcional pero recomendado, ya que se enviarán los datos mediante una conexión SSL segura.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica una credencial de ámbito de base de datos para la autenticación en el origen de datos externo.

Instrucciones y notas adicionales cuando se crea una credencial:

- Para cargar datos desde Azure Blob Storage o Azure Data Lake Store (ADLS) Gen2 en SQL DW, use una clave de almacenamiento de Azure.
- `CREDENTIAL` solo es necesario si se ha protegido el blob. `CREDENTIAL` no es necesario para los conjuntos de datos que permiten el acceso anónimo.

Para crear una credencial con ámbito de base de datos, vea [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc].

### <a name="type--hadoop"></a>TYPE = *HADOOP*

Especifica el tipo de origen de datos externo que se está configurando. Este parámetro no siempre es necesario.

- Use HADOOP cuando el origen de datos externo sea Azure Blob Storage, ADLS Gen1 o ADLS Gen2.

> [!IMPORTANT]
> No establezca `TYPE` si usa cualquier otro origen de datos externo.

Para obtener un ejemplo del uso de `TYPE` = `HADOOP` para cargar datos desde Azure Blob Storage, vea [Creación de un origen de datos externo para hacer referencia a Azure Blob Storage](#a-create-external-data-source-to-reference-azure-blob-storage).

## <a name="permissions"></a>Permisos

Necesita el permiso CONTROL en la base de datos.

## <a name="locking"></a>Bloqueo

Toma un bloqueo compartido en el objeto EXTERNAL DATA SOURCE.

## <a name="security"></a>Seguridad

PolyBase es compatible con la autenticación basada en proxy para la mayoría de orígenes de datos externos. Cree una credencial con ámbito de base de datos para crear la cuenta de proxy.

Cuando se conecta al almacenamiento o el grupo de datos en un clúster de macrodatos de SQL Server, las credenciales del usuario se pasan a través del sistema back-end. Cree inicios de sesión en el propio grupo de datos para habilitar la autenticación de paso a través.

Actualmente no se admite un token de SAS con tipo `HADOOP`. Solo se admite con una clave de acceso de cuenta de almacenamiento. Si se intenta crear un origen de datos externo con el tipo `HADOOP` y una credencial SAS, aparece un error como el siguiente:

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples"></a>Ejemplos:

### <a name="a-create-external-data-source-to-reference-azure-blob-storage"></a>A. Creación de un origen de datos externo para hacer referencia a Azure Blob Storage

En este ejemplo, el origen de datos externo es un contenedor de Azure Blob Storage denominado `daily` bajo la cuenta de Azure Storage denominada `logs`. El origen de datos externo de Azure Storage es solo para la transferencia de datos. No admite la inserción de predicado.

En este ejemplo se muestra cómo crear la credencial de ámbito de base de datos para la autenticación en Azure Storage. Especifique la clave de la cuenta de Azure Storage en el secreto de la credencial de base de datos. Puede especificar cualquier cadena en la identidad de la credencial con ámbito de base de datos, ya que no se usará para la autenticación en Azure Storage.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
     IDENTITY   = '<my_account>'
,    SECRET     = '<azure_storage_account_key>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
(    LOCATION   = 'wasbs://daily@logs.blob.core.windows.net/'
,    CREDENTIAL = AzureStorageCredential
,    TYPE       = HADOOP
)
;
```

### <a name="b-create-external-data-source-to-reference-azure-data-lake-store-gen-1-or-2-using-a-service-principal"></a>B. Creación de un origen de datos externo para hacer referencia a Azure Data Lake Store Gen 1 o 2 mediante una entidad de servicio

La conectividad de Azure Data Lake Store puede basarse en el URI de ADLS y en la entidad de servicio de la aplicación de Azure Active Directory. La documentación para crear esta aplicación se puede encontrar en [Autenticación entre servicios: Data Lake Store con Azure Active Directory][azure_ad[].

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLS_credential
WITH
--   IDENTITY   = '<clientID>@<OAuth2.0TokenEndPoint>'
     IDENTITY   = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token'
--,  SECRET     = '<KEY>'
,    SECRET     = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;

-- For Gen 1 - Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Storage.
-- LOCATION: Provide Data Lake Storage Gen 1 account name and URI
-- CREDENTIAL: Provide the credential created in the previous step
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH
(    LOCATION       = 'adl://newyorktaxidataset.azuredatalakestore.net'
,    CREDENTIAL     = ADLS_credential
,    TYPE           = HADOOP
)
;

-- For Gen 2 - Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Storage.
-- LOCATION: Provide Data Lake Storage Gen 2 account name and URI
-- CREDENTIAL: Provide the credential created in the previous step
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH
(    LOCATION       = 'abfss://newyorktaxidataset.azuredatalakestore.net' -- Please note the abfss endpoint when your account has secure transfer enabled
,    CREDENTIAL     = ADLS_credential
,    TYPE           = HADOOP
)
;
```

### <a name="c-create-external-data-source-to-reference-azure-data-lake-store-gen-2-using-the-storage-account-key"></a>C. Creación de un origen de datos externo para hacer referencia a Azure Data Lake Store Gen 2 con la clave de cuenta de almacenamiento

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'
;

CREATE DATABASE SCOPED CREDENTIAL ADLS_credential
WITH
--   IDENTITY   = '<storage_account_name>'
     IDENTITY   = 'newyorktaxidata'
--,  SECRET     = '<storage_account_key>'
,    SECRET     = 'yz5N4+bxSb89McdiysJAzo+9hgEHcJRJuXbF/uC3mhbezES/oe00vXnZEl14U0lN3vxrFKsphKov16C0w6aiTQ=='
;

-- Note this example uses a Gen 2 secured endpoint (abfss)
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
(    LOCATION   = 'abfss://2013@newyorktaxidataset.dfs.core.windows.net'
,    CREDENTIAL = ADLS_credential
,    TYPE       = HADOOP
)
[;]
```

### <a name="d-create-external-data-source-to-reference-polybase-connectivity-to-azure-data-lake-store-gen-2"></a>D. Creación de un origen de datos externo para hacer referencia a conectividad de Polybase para Azure Data Lake Store Gen 2

No es necesario especificar SECRET al conectarse a la cuenta de Azure Data Lake Store Gen2 con el mecanismo de [identidad administrada](/azure/active-directory/managed-identities-azure-resources/overview
).

```sql
-- If you do not have a Master Key on your DW you will need to create one
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'

--Create database scoped credential with **IDENTITY = 'Managed Service Identity'**

CREATE DATABASE SCOPED CREDENTIAL msi_cred WITH IDENTITY = 'Managed Service Identity';

--Create external data source with abfss:// scheme for connecting to your Azure Data Lake Store Gen2 account

CREATE EXTERNAL DATA SOURCE ext_datasource_with_abfss WITH (TYPE = hadoop, LOCATION = 'abfss://myfile@mystorageaccount.dfs.core.windows.net', CREDENTIAL = msi_cred);
```

## <a name="see-also"></a>Consulte también

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT (Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [CREATE EXTERNAL TABLE AS SELECT (Azure Synapse Analytics)][create_etb_as_sel]
- [CREATE TABLE AS SELECT (Azure Synapse Analytics)][create_tbl_as_sel]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Uso de firmas de acceso compartido (SAS)][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql

[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_eff]: https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[create_etb_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-as-select-transact-sql?view=azure-sqldw-latest
[create_tbl_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=azure-sqldw-latest

[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql

[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/
[remote_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[remote_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[sharded_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/
[sharded_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/

<!-- Azure Docs -->
[azure_ad]: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

|                                                              |                                                              |                                                              |                                                         |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------- | ---- |
| [SQL Server](create-external-data-source-transact-sql.md?view=sql-server-2017) | [SQL Database](create-external-data-source-transact-sql.md?view=azuresqldb-current) | [Azure Synapse<br />Analytics](create-external-data-source-transact-sql.md?view=azure-sqldw-latest) | **_\* Analytics<br />Platform System (PDW) \*_** &nbsp; |      |
|                                                              |                                                              |                                                              |                                                         |      |

&nbsp;

## <a name="overview-analytics-platform-system"></a>Introducción: Sistema de la plataforma de análisis

Crea un origen de datos externo para consultas de PolyBase. Los orígenes de datos externos se usan para establecer la conectividad y admiten el siguiente caso de uso: Virtualización y carga de datos mediante [PolyBase][intro_pb]

## <a name="syntax"></a>Sintaxis

```sql
CREATE EXTERNAL DATA SOURCE <data_source_name>
WITH
(    LOCATION                  = '<prefix>://<path>[:<port>]'
[,   CREDENTIAL                = <credential_name> ]
[,   TYPE                      = HADOOP ]
[,   RESOURCE_MANAGER_LOCATION = '<resource_manager>[:<port>]'
)
[;]
```

## <a name="arguments"></a>Argumentos

### <a name="data_source_name"></a>data_source_name

Especifica el nombre definido por el usuario para el origen de datos. El nombre debe ser único dentro del servidor en Analytics Platform System (Almacenamiento de datos paralelos o PDW).

### <a name="location--prefixpathport"></a>LOCATION = *`'<prefix>://<path[:port]>'`*

Proporciona el protocolo de conectividad y la ruta de acceso al origen de datos externo.

| Origen de datos externo    | Prefijo de ubicación | Ruta de acceso de ubicación                                         |
| ----------------------- | --------------- | ----------------------------------------------------- |
| Cloudera o Hortonworks | `hdfs`          | `<Namenode>[:port]`                                   |
| Azure Blob Storage      | `wasb[s]`       | `<container>@<storage_account>.blob.core.windows.net` |

Ruta de acceso de ubicación:

- `<`NameNode`>`: nombre de equipo, nombre de URI de servicio o dirección IP del `Namenode` en el clúster de Hadoop. PolyBase debe resolver los nombres DNS utilizados por el clúster de Hadoop. <!-- For highly available Hadoop configurations, provide the Nameservice ID as the `LOCATION`. -->
- `port` = el puerto en el cual escucha el origen de datos externo. En Hadoop, el puerto se puede encontrar mediante el parámetro de configuración `fs.defaultFS`. El valor predeterminado es 8020.
- `<container>` = el contenedor de la cuenta de almacenamiento que contiene los datos. Los contenedores raíz son de solo lectura, no se pueden volver a escribir datos en el contenedor.
- `<storage_account>` = el nombre de la cuenta de almacenamiento del recurso de Azure.

Instrucciones y notas adicionales cuando se establece la ubicación:

- El motor de PDW no comprueba la existencia del origen de datos externo cuando se crea el objeto. Para la validación, crea una tabla externa utilizando el origen de datos externo.
- Para garantizar una semántica de consulta coherente, use el mismo origen de datos externo para todas las tablas cuando realice consultas a Hadoop.
- `wasb` es el protocolo predeterminado para Azure Blob Storage. `wasbs` es opcional pero recomendado, ya que se enviarán los datos mediante una conexión SSL segura.
- Para garantizar que las consultas de PolyBase son correctas durante una conmutación por error del `Namenode` de Hadoop, considere la posibilidad de usar una dirección IP virtual para el `Namenode` del clúster de Hadoop. Si no, ejecute un comando [ALTER EXTERNAL DATA SOURCE][alter_eds] para que apunte a la nueva ubicación.

### <a name="credential--credential_name"></a>CREDENTIAL = *credential_name*

Especifica una credencial de ámbito de base de datos para la autenticación en el origen de datos externo.

Instrucciones y notas adicionales cuando se crea una credencial:

- Para cargar datos desde Azure Blob Storage o Azure Data Lake Store (ADLS) Gen2 en SQL Data Warehouse o PDW, use una clave de almacenamiento de Azure.
- `CREDENTIAL` solo es necesario si se ha protegido el blob. `CREDENTIAL` no es necesario para los conjuntos de datos que permiten el acceso anónimo.

### <a name="type---hadoop-"></a>TYPE = *[ HADOOP ]*

Especifica el tipo de origen de datos externo que se está configurando. Este parámetro no siempre es necesario.

- Use HADOOP cuando el origen de datos externo sea Cloudera, Hortonworks o Azure Blob Storage.

> [!IMPORTANT]
> No establezca `TYPE` si usa cualquier otro origen de datos externo.

Para obtener un ejemplo del uso de `TYPE` = `HADOOP` para cargar datos desde Azure Blob Storage, vea [Creación de un origen de datos externo para hacer referencia a Azure Blob Storage](#d-create-external-data-source-to-reference-azure-blob-storage).

### <a name="resource_manager_location--resourcemanager_uriport"></a>RESOURCE_MANAGER_LOCATION = *'ResourceManager_URI[:port]'*

Configure este valor opcional al conectarse a Hortonworks o Cloudera.

Cuando `RESOURCE_MANAGER_LOCATION` está definido, el optimizador de consultas toma una decisión basada en el coste para mejorar el rendimiento. Se puede usar un trabajo de MapReduce para insertar el cálculo en Hadoop. La especificación de `RESOURCE_MANAGER_LOCATION` puede reducir significativamente el volumen de datos transferidos entre Hadoop y SQL, lo cual puede suponer una mejora en el rendimiento de las consultas.

Si no se especifica el administrador de recursos, se deshabilita la inserción de cálculo en Hadoop para las consultas de PolyBase.

Si no se especifica el puerto, el valor predeterminado se elige mediante el valor actual de la configuración "hadoop connectivity".

| Conectividad de Hadoop | Puerto predeterminado del administrador de recursos |
| ------------------- | ----------------------------- |
| 1                   | 50300                         |
| 2                   | 50300                         |
| 3                   | 8021                          |
| 4                   | 8032                          |
| 5                   | 8050                          |
| 6                   | 8032                          |
| 7                   | 8050                          |

Para obtener una lista completa de las versiones de Hadoop compatibles, vea [Configuración de conectividad de PolyBase (Transact-SQL)][connectivity_pb].

> [!IMPORTANT]
> El valor RESOURCE_MANAGER_LOCATION no se valida cuando se crea el origen de datos externo. Escribir un valor incorrecto puede provocar un error de consulta en tiempo de ejecución cada vez que se intente la inserción, ya que el valor proporcionado no podrá realizar la resolución.

En [Creación de un origen de datos externo para hacer referencia a Hadoop con la inserción habilitada](#b-create-external-data-source-to-reference-hadoop-with-push-down-enabled) se proporciona un ejemplo concreto y más instrucciones.

## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL en la base de datos en Analytics Platform System (Almacenamiento de datos paralelos o PDW).

> [!NOTE]
> En versiones anteriores de PDW, la creación del origen de datos externo requería los permisos ALTER ANY EXTERNAL DATA SOURCE.

## <a name="locking"></a>Bloqueo

Toma un bloqueo compartido en el objeto EXTERNAL DATA SOURCE.

## <a name="security"></a>Seguridad

PolyBase es compatible con la autenticación basada en proxy para la mayoría de orígenes de datos externos. Cree una credencial con ámbito de base de datos para crear la cuenta de proxy.

Actualmente no se admite un token de SAS con tipo `HADOOP`. Solo se admite con una clave de acceso de cuenta de almacenamiento. Si se intenta crear un origen de datos externo con el tipo `HADOOP` y una credencial SAS, aparece un error como el siguiente:

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`

## <a name="examples"></a>Ejemplos:

### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. Creación de un origen de datos externo para hacer referencia a Hadoop

Para crear un origen de datos externo para hacer referencia al clúster de Hortonworks o Cloudera Hadoop, especifique el nombre de equipo o la dirección IP de `Namenode` de Hadoop y el puerto. <!-- Provide the Nameservice ID as the `LOCATION` for highly available configurations. -->

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION = 'hdfs://10.10.10.10:8050'
,    TYPE     = HADOOP
)
;
```

### <a name="b-create-external-data-source-to-reference-hadoop-with-push-down-enabled"></a>B. Creación de un origen de datos externo para hacer referencia a Hadoop con la inserción habilitada

Especifique la opción `RESOURCE_MANAGER_LOCATION` para habilitar la inserción de cálculo en Hadoop para las consultas de PolyBase. Una vez habilitado, PolyBase toma una decisión basada en el coste para determinar si se debe aplicar el cálculo de la consulta en Hadoop.

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8020'
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="c-create-external-data-source-to-reference-kerberos-secured-hadoop"></a>C. Creación de un origen de datos externo para hacer referencia a Hadoop con protección de Kerberos

Para comprobar si el clúster de Hadoop está protegido con Kerberos, compruebe el valor de la propiedad hadoop.security.authentication en core-site.xml de Hadoop. Para hacer referencia a un clúster de Hadoop protegido con Kerberos, debe especificar una credencial con ámbito de base de datos que contenga el nombre de usuario y la contraseña de Kerberos. La clave maestra de base de datos se usa para cifrar el secreto de la credencial de ámbito de base de datos.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
WITH
     IDENTITY   = '<hadoop_user_name>'
,    SECRET     = '<hadoop_password>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH
(    LOCATION                  = 'hdfs://10.10.10.10:8050'
,    CREDENTIAL                = HadoopUser1
,    TYPE                      = HADOOP
,    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
)
;
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. Creación de un origen de datos externo para hacer referencia a Azure Blob Storage

En este ejemplo, el origen de datos externo es un contenedor de Azure Blob Storage denominado `daily` bajo la cuenta de Azure Storage denominada `logs`. El origen de datos externo de Azure Storage es solo para la transferencia de datos. No admite la inserción de predicado.

En este ejemplo se muestra cómo crear la credencial de ámbito de base de datos para la autenticación en Azure Storage. Especifique la clave de la cuenta de Azure Storage en el secreto de la credencial de base de datos. Puede especificar cualquier cadena en la identidad de la credencial con ámbito de base de datos, ya que no se usará para la autenticación en Azure Storage.

```sql
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo'
;

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
     IDENTITY   = '<my_account>'
,    SECRET     = '<azure_storage_account_key>'
;

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage
WITH
(    LOCATION   = 'wasbs://daily@logs.blob.core.windows.net/'
,    CREDENTIAL = AzureStorageCredential
,    TYPE       = HADOOP
)
;
```

## <a name="see-also"></a>Consulte también

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)][create_dsc]
- [CREATE EXTERNAL FILE FORMAT (Transact-SQL)][create_eff]
- [CREATE EXTERNAL TABLE (Transact-SQL)][create_etb]
- [sys.external_data_sources (Transact-SQL)][cat_eds]
- [Uso de firmas de acceso compartido (SAS)][sas_token]

<!-- links to external pages -->
<!-- SQL Docs -->
[bulk_insert]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql
[bulk_insert_example]: https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage
[openrowset]: https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql

[create_dsc]: https://docs.microsoft.com/sql/t-sql/statements/create-database-scoped-credential-transact-sql
[create_eff]: https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql
[create_etb]: https://docs.microsoft.com/sql/t-sql/statements/create-external-data-source
[create_etb_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-external-table-as-select-transact-sql?view=azure-sqldw-latest
[create_tbl_as_sel]: https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?view=azure-sqldw-latest

[alter_eds]: https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql

[cat_eds]: https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-external-data-sources-transact-sql
<!-- PolyBase docs -->
[intro_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide
[mongodb_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-configure-mongodb
[connectivity_pb]:https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql
[connection_options]: https://docs.microsoft.com/sql/relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client
[hint_pb]: https://docs.microsoft.com/sql/relational-databases/polybase/polybase-pushdown-computation#force-pushdown
<!-- Elastic Query Docs -->
[intro_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/
[remote_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[remote_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/
[sharded_eq]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/
[sharded_eq_tutorial]: https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/

<!-- Azure Docs -->
[azure_ad]: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory
[sas_token]: https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1

::: moniker-end
