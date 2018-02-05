---
title: Crear tabla externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e9ee131e1c4bb09ae19c90d84b78a7d6fc662ae8
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="create-external-table-transact-sql"></a>Crear tabla externa (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Crea una tabla externa de PolyBase que hace referencia a los datos almacenados en un clúster de Hadoop o almacenamiento de blobs de Azure. También puede utilizarse para crear una tabla externa para [consulta de base de datos elástica](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 Utilice una tabla externa para:  
  
-   Consultar datos de almacenamiento de blob de Azure o Hadoop con [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones.  
  
-   Importar y almacenar los datos de almacenamiento de blobs de Azure o Hadoop en su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
-   Crear una tabla externa para su uso con una base de datos elástica  
     consulta.  
     
- Importar y almacenar los datos de almacén de Data Lake de Azure en almacenamiento de datos de SQL Azure
  
 Vea también [crear origen de datos externo &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) y [Eliminar tabla externa &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* . [nombre_esquema]. | schema_name. ] *table_name*  
 Uno a tres - parte nombre de la tabla que se va a crear. Para una tabla externa, solo los metadatos de tabla se almacenan en SQL junto con estadísticas básicas sobre el archivo y o carpeta que se hace referencia en el almacenamiento de blobs de Azure o Hadoop. Ningún dato real que se mueve o se almacenan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 \<definición_de_columna > [,... *n*  ] Crear tabla externa permite una o varias definiciones de columna. Crear tabla externa y CREATE TABLE utilizan la misma sintaxis para definir una columna. Una excepción a esto, no puede utilizar la restricción DEFAULT en las tablas externas. Para obtener los detalles completos acerca de las definiciones de columna y sus tipos de datos, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) y [crear una tabla de base de datos SQL Azure](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 Las definiciones de columna, incluidos los tipos de datos y el número de columnas deben coincidir con los datos de los archivos externos. Si se produce un error de coincidencia, se rechazarán las filas del archivo cuando se consultan los datos reales.  
  
 Para tablas externas que hacen referencia a archivos de orígenes de datos externos, deben asignar las definiciones de columna y escriba en el esquema exacto del archivo externo. Al definir los tipos de datos que hacen referencia a los datos almacenados en Hadoop/Hive, utilice las siguientes asignaciones entre tipos de datos SQL y Hive y convierte el tipo a un tipo de datos SQL cuando se selecciona de él. Los tipos incluyen todas las versiones de Hive a menos que se indique lo contrario.

> [!NOTE]  
>  SQL Server no admite el subárbol _infinito_ valor de datos en cualquier conversión. PolyBase se producirá un error de conversión de tipo de datos.


|Tipo de datos de SQL|Tipo de datos de .NET|Tipo de datos de Hive|Hadoop/Java Data Type|Comentarios|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|tinyint|Byte|tinyint|ByteWritable|Sólo números sin signo.|  
|smallint|Int16|smallint|ShortWritable||  
|int|Int32|int|IntWritable||  
|bigint|Int64|bigint|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|float|Doble|double|DoubleWritable||  
|real|Único|float|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|smallmoney|Decimal|double|DoubleWritable||  
|NCHAR|String<br /><br /> Char[]|string|texto||  
|nvarchar|String<br /><br /> Char[]|string|Texto||  
|char|String<br /><br /> Char[]|string|Texto||  
|varchar|String<br /><br /> Char[]|string|Texto||  
|binary|Byte[]|binary|BytesWritable|Se aplica al subárbol 0,8 y versiones posterior.|  
|varbinary|Byte[]|binary|BytesWritable|Se aplica al subárbol 0,8 y versiones posterior.|  
|date|DateTime|TIMESTAMP|TimestampWritable||  
|smalldatetime|DateTime|TIMESTAMP|TimestampWritable||  
|datetime2|DateTime|TIMESTAMP|TimestampWritable||  
|datetime|DateTime|TIMESTAMP|TimestampWritable||  
|time|Timespan|TIMESTAMP|TimestampWritable||  
|decimal|Decimal|decimal|BigDecimalWritable|Se aplica a Hive0.11 y versiones posteriores.|  
  
 UBICACIÓN = '*folder_or_filepath*'  
 Especifica la carpeta o la ruta de acceso y nombre de archivo para los datos reales en el almacenamiento de blobs de Azure o Hadoop. La ubicación que se inicia desde la carpeta raíz. la carpeta raíz es la ubicación de datos especificada en el origen de datos externo.  
  
 Si se especifica la ubicación para que sea una carpeta, una consulta de PolyBase que selecciona en la tabla externa recuperará los archivos de la carpeta y todas sus subcarpetas. Al igual que Hadoop, PolyBase no devuelve carpetas ocultas. No devuelve los archivos para los que el nombre de archivo comienza con un carácter de subrayado (_) o un punto (.).  
  
 En este ejemplo, si ubicación = '/ webdata /', una consulta de PolyBase devolverá filas de mydata.txt y mydata2.txt.  No devolverá mydata3.txt porque es una subcarpeta de una carpeta oculta. No devolverá _hidden.txt porque es un archivo oculto.  
  
 ![Datos recursivos para tablas externas](../../t-sql/statements/media/aps-polybase-folder-traversal.png "datos recursivos para tablas externas")  
  
 Para cambiar el valor predeterminado y solo lectura en la carpeta raíz, establezca el atributo \<polybase.recursive.traversal > en 'false' en el archivo de configuración de core-site.xml. Este archivo se encuentra en `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Por ejemplo, `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica el nombre del origen de datos externo que contiene la ubicación de los datos externos. Esta ubicación es el almacenamiento de blobs de Azure o Hadoop. Para crear un origen de datos externo, use [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica el nombre del objeto de formato de archivo externo que almacena el método de compresión y el tipo de archivo para los datos externos. Para crear un formato de archivo externo, use [crear EXTERNAL FILE FORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Rechazar opciones  
 Puede especificar parámetros de rechazo que determinan cómo controlará PolyBase *desfasadas* registra recupera del origen de datos externo. Un registro de datos se considera 'desfasadas' si se el número de columnas o tipos de datos real no coinciden con las definiciones de columna de la tabla externa.  
  
 Cuando no se especifica o cambiar los valores de rechazo, PolyBase usa valores predeterminados. Esta información acerca de los parámetros de rechazo se almacena como metadatos adicionales cuando se crea una tabla externa con la instrucción CREATE TABLE externo.   Cuando un futuro instrucciones SELECT o seleccione INTO SELECT selecciona datos de la tabla externa, PolyBase utilizará las opciones de rechazo para determinar el número o porcentaje de filas que se pueda rechazar antes de que se produce un error en la consulta real. . La consulta devolverá resultados (parciales) hasta que se supere el umbral de rechazo; a continuación, se produce un error con el mensaje de error adecuado.  
  
 REJECT_TYPE = **valor** | porcentaje  
 Aclara si se especifica la opción REJECT_VALUE como un valor literal o un porcentaje.  
  
 value  
 REJECT_VALUE es un valor literal, no un porcentaje. La consulta de PolyBase se producirá un error cuando se supera el número de filas rechazados *reject_value*.  
  
 Por ejemplo, si REJECT_VALUE = 5 y REJECT_TYPE = valor, la consulta SELECT se producirá un error después de que se han rechazado 5 filas de PolyBase.  
  
 Porcentaje  
 REJECT_VALUE es un porcentaje, no un valor literal. Una consulta de PolyBase se producirá un error cuando la *porcentaje* de filas con errores supera *reject_value*. El porcentaje de filas con errores se calcula a intervalos.  
  
 REJECT_VALUE = *reject_value*  
 Especifica el valor o el porcentaje de filas que se pueda rechazar antes de que se produce un error en la consulta.  
  
 Para REJECT_TYPE = valor, *reject_value* debe ser un entero comprendido entre 0 y 2.147.483.647.  
  
 Para REJECT_TYPE = porcentaje, *reject_value* debe ser un valor flotante comprendido entre 0 y 100.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Este atributo es necesario cuando se especifica REJECT_TYPE = porcentaje. Determina el número de filas que se intentan recuperar antes la PolyBase vuelve a calcular el porcentaje de filas rechazados.  
  
 El *reject_sample_value* parámetro debe ser un entero comprendido entre 0 y 2.147.483.647.  
  
 Por ejemplo, si REJECT_SAMPLE_VALUE = 1000, PolyBase calcula el porcentaje de filas con errores después de que ha intentado importar 1000 filas desde el archivo de datos externo. Si el porcentaje de filas con errores es menor que *reject_value*, PolyBase intentará recuperar otro 1000 filas. Continúa para volver a calcular el porcentaje de filas con errores después de intentar importar cada 1000 filas adicionales.  
  
> [!NOTE]  
>  Puesto que PolyBase calcula el porcentaje de filas con errores a intervalos, puede superar el porcentaje real de filas con errores *reject_value*.  
  
 Ejemplo:  
  
 Este ejemplo muestra cómo interactúan entre sí las tres opciones de rechazo. Por ejemplo, si REJECT_TYPE = porcentaje, REJECT_VALUE = 30 y REJECT_SAMPLE_VALUE = 100, puede producirse el siguiente escenario:  
  
-   PolyBase intenta recuperar las 100 primeras filas; 25 producirá un error y 75 se realizan correctamente.  
  
-   Porcentaje de filas con errores se calcula como 25%, que es menor que el valor de rechazo de 30%. Por lo tanto, PolyBase continuará la recuperación de datos desde el origen de datos externo.  
  
-   PolyBase intenta cargar las 100 filas; Esta vez correctamente 25 y 75 producirá un error.  
  
-   Se vuelve a calcular el porcentaje de filas con errores como 50%. El porcentaje de filas con errores ha superado el valor de rechazo de 30%.  
  
-   La consulta de PolyBase con filas de 50% rechazado se produce un error después de intentar devolver las 200 primeras filas. Tenga en cuenta que se han devuelto filas coincidentes antes de la consulta de PolyBase detecta que se ha superado el umbral de rechazo.  
  
 Opciones de tabla externa particionadas  
 Especifica el origen de datos externo (un origen de datos no es de SQL Server) y un método de distribución para el [consulta de base de datos elástica](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 DATA_SOURCE  
 Un origen de datos externo, como los datos almacenados en un sistema de archivos de Hadoop, almacenamiento de blobs de Azure, o un [manager de mapa de particiones](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/).  
  
 SCHEMA_NAME  
 La cláusula SCHEMA_NAME proporciona la capacidad de asignar la definición de tabla externa a una tabla en un esquema diferente en la base de datos remota. Utilice esto para eliminar la ambigüedad entre los esquemas que existen en las bases de datos locales y remotos.  
  
 OBJECT_NAME  
 La cláusula OBJECT_NAME proporciona la capacidad para asignar la definición de tabla externa a una tabla con un nombre diferente en la base de datos remota. Utilice esto para eliminar la ambigüedad entre los nombres de objeto que existen en las bases de datos locales y remotos.  
  
 DISTRIBUCIÓN  
 Opcional. Esto solo es necesario solo para las bases de datos de tipo SHARD_MAP_MANAGER. Esta propiedad controla si una tabla se trata como una tabla particionada o una tabla replicada. Con **SHARDED** (*nombre de la columna*) de las tablas, los datos de tablas diferentes no se superponen. **Replica** especifica que las tablas tienen los mismos datos en cada partición. **ROUND_ROBIN** indica que un método específico de la aplicación se utiliza para distribuir los datos.  
  
## <a name="permissions"></a>Permissions  
 Requiere estos permisos de usuario:  
  
-   **CREATE TABLE**  
  
-   **MODIFICAR CUALQUIER ESQUEMA**  
  
-   **MODIFICAR CUALQUIER ORIGEN DE DATOS EXTERNOS**  
  
-   **MODIFICAR CUALQUIER FORMATO DE ARCHIVO EXTERNO**  

-   **BASE DE DATOS DE CONTROL**
  
 Tenga en cuenta que el inicio de sesión que crea el origen de datos externo debe tener permiso para leer y escribir en el origen de datos externo, ubicado en el almacenamiento de blobs de Azure o Hadoop.  


 > [!IMPORTANT]  

>  El permiso ALTER ANY EXTERNAL DATA SOURCE concede a cualquier entidad de seguridad de la capacidad de crear y modificar cualquier objeto de origen de datos externo y, por lo tanto, también concede la capacidad de tener acceso a todas las credenciales de ámbito de la base de datos en la base de datos. Este permiso debe considerarse como con altos privilegios y, por tanto, se debe conceder únicamente a las entidades de confianza en el sistema.

## <a name="error-handling"></a>Tratamiento de errores  
 Al ejecutar la instrucción CREATE TABLE externo, PolyBase intenta conectarse al origen de datos externo. Si se produce un error en el intento de conexión, se producirá un error en la instrucción y no se creará la tabla externa. Puede tardar un minuto o más para que el comando producirá un error porque PolyBase vuelve a intentar la conexión antes de cancelar al final de la consulta.  
  
## <a name="general-remarks"></a>Notas generales  
 En escenarios de consulta "ad-hoc", es decir, seleccione desde tabla externa, PolyBase almacena las filas recuperadas con el origen de datos externos en una tabla temporal. Una vez finalizada la consulta, PolyBase quita y elimina la tabla temporal. No hay datos permanentes se almacenan en tablas SQL.  
  
 En cambio, en el escenario de importación, es decir, seleccione en desde tabla externa, PolyBase almacena las filas recuperadas con el origen de datos externo como datos permanentes en la tabla SQL. La nueva tabla se crea durante la ejecución de la consulta cuando Polybase recupera los datos externos.  
  
 PolyBase puede insertar algunos de los cálculos de consulta a Hadoop para mejorar el rendimiento de las consultas. Esto se denomina aplicación del predicado. Para habilitar esta opción, especifique la opción de ubicación del Administrador de recursos de Hadoop en [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 Puede crear varias tablas externas que hacen referencia a los orígenes de datos externos iguales o distintos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 En CTP2, la funcionalidad de exportación no se admite, es decir, de forma permanente al almacenar datos de SQL en el origen de datos externo. Esta funcionalidad estará disponible en CTP3.  
  
 Puesto que los datos de una tabla externa residen desactivar el dispositivo, lo no está bajo el control de PolyBase y se puede cambiar o quitar en cualquier momento por un proceso externo. Por este motivo, no se garantiza que los resultados de consulta en una tabla externa debe ser determinista. La misma consulta puede devolver resultados diferentes cada vez que se ejecute en una tabla externa. De forma similar, una consulta puede producir un error si se quita o se reubican los datos externos.  
  
 Puede crear varias tablas externas que cada uno de ellos hacen referencia a orígenes de datos externos distintos. Sin embargo, si ejecuta consultas simultáneamente en diferentes orígenes de datos de Hadoop, cada origen de Hadoop debe usar la misma configuración de configuración de servidor "conectividad de hadoop". Por ejemplo, no se puede ejecutar simultáneamente una consulta en un clúster de Cloudera Hadoop y un clúster de Hortonworks Hadoop desde estos valores de configuración diferente de uso. Para la configuración y las combinaciones admitidas, vea [configuración de PolyBase &#40; Transact-SQL &#41; ](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 Solo estas instrucciones de lenguaje de definición de datos (DDL) se admiten en tablas externas:  
  
-   CREATE TABLE y DROP TABLE  
  
-   CREATE STATISTICS y DROP STATISTICS  
Nota: Al crear y quitar las estadísticas en tablas externas no se admiten en la base de datos de SQL Azure. 
  
-   CREATE VIEW y DROP VIEW  
  
 Las construcciones y las operaciones no admitidas:  
  
-   La restricción predeterminada de las columnas de tabla externa  
  
-   Operaciones de lenguaje de manipulación (DML) de datos de delete, insert y update  
  
 Limitaciones de consulta:  
  
 PolyBase puede consumir un máximo de 33 k de archivos por carpeta cuando se ejecutan 32 consultas simultáneas de PolyBase. Este número incluye archivos y subcarpetas en cada carpeta HDFS. Si el grado de simultaneidad es menor que 32, un usuario puede ejecutar las consultas de PolyBase en carpetas en HDFS que contienen archivos de más de 33 k. Se recomienda que mantenga rutas de acceso de archivo externo cortos y use no más de 30 archivos k por carpeta HDFS. Cuando se hace referencia a demasiados archivos, podría producirse una excepción de memoria insuficiente de máquina Virtual Java (JVM).  

Limitaciones de ancho de tabla: PolyBase en SQL Server 2016 tiene un límite de ancho de fila de 32KB, en función del tamaño máximo de una sola fila válida por la definición de la tabla. Si la suma del esquema de columna es mayor que 32KB, PolyBase no podrá consultar los datos. 

En el almacén de datos de SQL, esta limitación se ha ampliado a 1MB.


## <a name="locking"></a>Bloqueo  
 Compartir el bloqueo en el objeto SCHEMARESOLUTION.  
  
## <a name="security"></a>Seguridad  
 Los archivos de datos para una tabla externa se almacena en almacenamiento de blobs de Azure o Hadoop. Estos archivos de datos se crea y administra sus propios procesos. Es su responsabilidad para administrar la seguridad de los datos externos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Crear una tabla externa con datos en formato delimitado por el texto.  
 Este ejemplo muestra todos los pasos necesarios para crear una tabla externa que tiene datos con formato en archivos de texto delimitado. Define un origen de datos externo *mydatasource* y un formato de archivo externo *myfileformat*. Estos objetos de base de datos, a continuación, se hace referencia en la instrucción CREATE TABLE externo. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) y [el formato de archivo externo de CREATE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. Crear una tabla externa con datos en formato RCFile.  
 Este ejemplo muestra todos los pasos necesarios para crear una tabla externa que tiene datos con formato RCFiles. Define un origen de datos externo *mydatasource_rc* y un formato de archivo externo *myfileformat_rc*. Estos objetos de base de datos, a continuación, se hace referencia en la instrucción CREATE TABLE externo. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) y [el formato de archivo externo de CREATE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. Crear una tabla externa con datos en formato ORC.  
 Este ejemplo muestra todos los pasos necesarios para crear una tabla externa que tiene el formato de datos como archivos ORC. Define un mydatasource_orc de origen de datos externo y un myfileformat_orc de formato de archivo externo. Estos objetos de base de datos, a continuación, se hace referencia en la instrucción CREATE TABLE externo. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) y [el formato de archivo externo de CREATE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>D. Consultar datos de Hadoop  
 Clickstream es una tabla externa que se conecta el archivo de texto delimitado employee.tbl en un clúster de Hadoop. La consulta siguiente es similar a una consulta en una tabla estándar. Sin embargo, esta consulta recupera datos de Hadoop y, a continuación, calcula el producirá.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Combinar datos de Hadoop con datos de SQL  
 Esta consulta es similar a una combinación estándar en dos tablas SQL. La diferencia es que PolyBase recupera la información de Hadoop y, a continuación, combina con la tabla UrlDescription. Una tabla es una tabla externa y el otro es una tabla SQL estándar.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importar datos desde Hadoop en una tabla SQL  
 Este ejemplo crea una nueva tabla ms_user SQL que almacena el resultado de una combinación entre la tabla SQL estándar de forma permanente *usuario* y la tabla externa *ClickStream*.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. Crear una tabla externa para un origen de datos con particiones  
 En este ejemplo se reasigna una DMV remota a una tabla externa mediante las cláusulas SCHEMA_NAME y OBJECT_NAME.  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. Importación de datos de ADLS en Azure[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH ( FORMATTYPE = DELIMITEDTEXT 
     , FORMATOPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
    )


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH ( LOCATION='/DimProduct/' , 
       DATA_SOURCE = AzureDataLakeStore , 
       FILE_FORMAT = TextFileFormat , 
       REJECT_TYPE = VALUE ,
       REJECT_VALUE = 0 ) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. JOIN tablas externas  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. Combinar datos HDFS con datos PDW  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. Importar datos de las filas de HDFS en una tabla de PDW distribuida  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. Importar datos de las filas de HDFS en una tabla replicada de PDW  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consulta de metadatos comunes (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREAR AS de tabla externa SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Crear tabla como SELECT &#40; Almacenamiento de datos SQL de Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



