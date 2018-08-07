---
title: CREATE EXTERNAL TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 6/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 57c8288f9a19599f3047fddb030f05a1edfbb300
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454549"
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Crea una tabla externa para PolyBase, o bien consultas de Elastic Database. Según el escenario, la sintaxis difiere de forma considerable. No se puede usar una tabla externa creada para PolyBase para las consultas de Elastic Database.  Del mismo modo, no se puede usar una tabla externa creada para consultas de Elastic Database para PolyBase, etc. 
  
> [!NOTE]  
>  PolyBase solo se admite en SQL Server 2016 (o superior), Azure SQL Data Warehouse y Almacenamiento de datos paralelos. Las consultas de Elastic Database solo se admiten en Azure SQL Database v12 o posterior.  


- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tablas externas para acceder a los datos almacenados en un clúster de Hadoop o en Azure Blob Storage, una tabla externa de PolyBase que hace referencia a los datos almacenados en un clúster de Hadoop o en Azure Blob Storage. También se pueden usar para crear una tabla externa para [consultas de Elastic Database](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 Use una tabla externa para:  
  
-   Consultar datos de Hadoop o Azure Blob Storage con instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Importar datos de Hadoop o Azure Blob Storage y almacenarlos en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Crear una tabla externa para su uso con una consulta de Elastic Database  
     .  
     
- Importar y almacenar datos de Azure Data Lake Store en Azure SQL Data Warehouse.
  
 Vea también [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) y [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
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
    | REJECT_TYPE = value | percentage,  
    | REJECT_VALUE = reject_value,  
    | REJECT_SAMPLE_VALUE = reject_sample_value,
    | REJECTED_ROW_LOCATION = '\REJECT_Directory'
  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* . [ schema_name ] . | schema_name. ] *table_name*  
 Nombre de entre una y tres partes de la tabla que se va a crear. En una tabla externa, solo los metadatos de tabla se almacenan en SQL junto con estadísticas básicas sobre el archivo o carpeta a los que se hace referencia en Hadoop o Azure Blob Storage. Ningún dato real se mueve o se almacena en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 \<column_definition> [ ,...*n* ] CREATE EXTERNAL TABLE permite una o varias definiciones de columna. CREATE EXTERNAL TABLE y CREATE TABLE usan la misma sintaxis para definir una columna. La excepción es que no se puede usar DEFAULT CONSTRAINT en tablas externas. Para obtener los detalles completos sobre las definiciones de columna y sus tipos de datos, vea [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) y [CREATE TABLE en Azure SQL Database](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 Las definiciones de columna, incluidos los tipos de datos y el número de columnas, deben coincidir con los datos de los archivos externos. Si hay alguna no coincidencia, se rechazan las filas de archivo al consultar los datos reales.  
  
 En tablas externas que hacen referencia a archivos de orígenes de datos externos, las definiciones de columna y tipo deben asignarse al esquema exacto del archivo externo. Al definir tipos de datos que hacen referencia a datos almacenados en Hadoop/Hive, use las siguientes asignaciones entre tipos de datos SQL y Hive y convierta el tipo a un tipo de datos SQL cuando seleccione desde él. Los tipos incluyen todas las versiones de Hive, a menos que se indique lo contrario.

> [!NOTE]  
>  SQL Server no admite el valor de datos _infinity_ de Hive en ninguna conversión. En PolyBase se produce un error de conversión de tipo de datos.


|Tipo de datos de SQL|Tipo de datos de .NET|Tipo de datos de Hive|Hadoop/Java Data Type|Comentarios|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|TINYINT|Byte|TINYINT|ByteWritable|Solo para números sin signo.|  
|SMALLINT|Int16|SMALLINT|ShortWritable||  
|INT|Int32|INT|IntWritable||  
|BIGINT|Int64|BIGINT|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|FLOAT|Doble|double|DoubleWritable||  
|REAL|Único|FLOAT|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|SMALLMONEY|Decimal|double|DoubleWritable||  
|NCHAR|String<br /><br /> Char[]|string|texto||  
|NVARCHAR|String<br /><br /> Char[]|string|Texto||  
|char|String<br /><br /> Char[]|string|Texto||  
|varchar|String<br /><br /> Char[]|string|Texto||  
|binary|Byte[]|binary|BytesWritable|Se aplica a Hive 0.8 y posterior.|  
|varbinary|Byte[]|binary|BytesWritable|Se aplica a Hive 0.8 y posterior.|  
|Date|DateTime|TIMESTAMP|TimestampWritable||  
|smalldatetime|DateTime|TIMESTAMP|TimestampWritable||  
|datetime2|DateTime|TIMESTAMP|TimestampWritable||  
|DATETIME|DateTime|TIMESTAMP|TimestampWritable||  
|time|Timespan|TIMESTAMP|TimestampWritable||  
|Decimal|Decimal|Decimal|BigDecimalWritable|Se aplica a Hive 0.11 y posterior.|  
  
 LOCATION =  '*folder_or_filepath*'  
 Especifica la ruta de acceso y el nombre de la carpeta o el archivo de los datos reales en Hadoop o Azure Blob Storage. La ubicación se inicia desde la carpeta raíz; la carpeta raíz es la ubicación de datos especificada en el origen de datos externo.  


En SQL Server, la instrucción CREATE EXTERNAL TABLE crea la ruta de acceso y la carpeta si aún no existen. Luego puede usar INSERT INTO para exportar datos de una tabla de SQL Server local al origen de datos externo. Para más información, vea [Polybase Queries](/sql/relational-databases/polybase/polybase-queries) (Consultas de Polybase). 

En SQL Data Warehouse y Analytics Platform System, la instrucción [CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) crea la ruta de acceso y la carpeta si no existen. En estos dos productos, CREATE EXTERNAL TABLE no crea la ruta de acceso ni la carpeta.

  
 Si se especifica LOCATION para que sea una carpeta, una consulta de PolyBase que seleccione en la tabla externa recuperará los archivos de la carpeta y todas sus subcarpetas. Al igual que Hadoop, PolyBase no devuelve carpetas ocultas. Tampoco devuelve los archivos cuyo nombre comienza con un carácter de subrayado (_) o un punto (.).  
  
 En este ejemplo, si LOCATION='/webdata/', una consulta de PolyBase devolverá filas de mydata.txt y mydata2.txt.  No devolverá mydata3.txt porque es una subcarpeta de una carpeta oculta. No devolverá _hidden.txt porque es un archivo oculto.  
  
 ![Datos recursivos para tablas externas](../../t-sql/statements/media/aps-polybase-folder-traversal.png "Recursive data for external tables")  
  
 Para cambiar el valor predeterminado y leer únicamente de la carpeta raíz, establezca el atributo \<polybase.recursive.traversal> en False en el archivo de configuración core-site.xml. Este archivo se encuentra en `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Por ejemplo, `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica el nombre del origen de datos externo que contiene la ubicación de los datos externos. Esta ubicación es Hadoop o Azure Blob Storage. Para crear un origen de datos externo, use [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica el nombre del objeto de formato de archivo externo que almacena el tipo de archivo y el método de compresión de los datos externos. Para crear un formato de archivo externo, use [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Opciones de Reject  
 Puede especificar parámetros de Reject que determinen cómo va a administrar PolyBase los registros *desfasados* que recupera del origen de datos externo. Un registro de datos se considera "desfasado" si los tipos de datos reales o el número de columnas no coinciden con las definiciones de columna de la tabla externa.  
  
 Si no se especifican ni se cambian los valores Reject, PolyBase usa los valores predeterminados. Esta información sobre los parámetros de Reject se almacena como metadatos adicionales al crear una tabla externa con la instrucción CREATE EXTERNAL TABLE.   Cuando una futura instrucción SELECT o SELECT INTO SELECT selecciona datos de la tabla externa, PolyBase usa las opciones de Reject para determinar el número o porcentaje de filas que se pueden rechazar antes de que se produzca un error en la consulta real. . La consulta devuelve resultados (parciales) hasta que se supera el umbral de Reject; después se produce un error con el mensaje de error correspondiente.  
  
 REJECT_TYPE = **value** | percentage  
 Aclara si la opción REJECT_VALUE se especifica como un valor literal o como un porcentaje.  
  
 value  
 REJECT_VALUE es un valor literal, no un porcentaje. Si el número de filas rechazadas supera el valor *reject_value*, se produce un error en la consulta de PolyBase.  
  
 Por ejemplo, si REJECT_VALUE = 5 y REJECT_TYPE = value, se produce un error en la consulta SELECT de PolyBase después de que se hayan rechazado 5 filas.  
  
 percentage  
 REJECT_VALUE es un porcentaje, no un valor literal. Si el *porcentaje* de filas con errores supera el valor *reject_value*, se produce un error en la consulta de PolyBase. El porcentaje de filas con errores se calcula a intervalos.  
  
 REJECT_VALUE = *reject_value*  
 Especifica el valor o el porcentaje de filas que se pueden rechazar antes de que se produzca un error en la consulta.  
  
 Para REJECT_TYPE = value, *reject_value* debe ser un entero comprendido entre 0 y 2.147.483.647.  
  
 Para REJECT_TYPE = percentage, *reject_value* debe ser un valor float comprendido entre 0 y 100.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Este atributo es necesario cuando se especifica REJECT_TYPE = percentage. Determina el número de filas que se intentan recuperar antes de que PolyBase vuelva a calcular el porcentaje de filas rechazadas.  
  
 El parámetro *reject_sample_value* debe ser un entero comprendido entre 0 y 2.147.483.647.  
  
 Por ejemplo, si REJECT_SAMPLE_VALUE = 1000, PolyBase calcula el porcentaje de filas con errores después de haber intentado importar 1000 filas desde el archivo de datos externos. Si el porcentaje de filas con errores es inferior al valor de *reject_value*, PolyBase intenta recuperar otras 1000 filas. Sigue recalculando el porcentaje de filas con errores después de intentar importar cada 1000 filas más.  
  
> [!NOTE]  
>  Puesto que PolyBase calcula el porcentaje de filas con errores a intervalos, el porcentaje real de filas con errores puede superar el valor de *reject_value*.  
  

Ejemplo:  
  
 En este ejemplo se muestra cómo interactúan entre sí las tres opciones REJECT. Por ejemplo, si REJECT_TYPE = percentage, REJECT_VALUE = 30 y REJECT_SAMPLE_VALUE = 100, sucederá lo siguiente:  
  
-   PolyBase intenta recuperar las 100 primeras filas; 25 no se importan y 75 sí.  
  
-   El porcentaje de filas con errores se calcula en un 25 %, que es menor que el valor de rechazo de 30 %. Por lo tanto, PolyBase sigue recuperando datos del origen de datos externo.  
  
-   PolyBase intenta cargar las siguientes 100 filas; esta vez, 25 lo hacen y 75 no.  
  
-   El porcentaje de filas con errores se recalcula en un 50 %. El porcentaje de filas con errores ha superado el valor de rechazo de 30 %.  
  
-   Se produce un error en la consulta de PolyBase con un 50 % de filas rechazadas después de intentar devolver las 200 primeras filas. Tenga en cuenta que se han devuelto filas coincidentes antes de que la consulta de PolyBase detecte que se ha superado el umbral de rechazo.  
  
REJECTED_ROW_LOCATION = *Ubicación del directorio*
  
  Especifica el directorio del origen de datos externo en el que se deben escribir las filas rechazadas y el archivo de errores correspondiente.
Si la ruta de acceso especificada no existe, PolyBase creará una en su nombre. Se crea un directorio secundario con el nombre "_rejectedrows". El carácter "_" garantiza que el directorio tenga un escape para otro procesamiento de datos a menos que se mencione explícitamente en el parámetro de ubicación. En este directorio hay una carpeta que se crea según la hora de envío de la carga con el formato AñoMesDía-HoraMinutoSegundo (por ejemplo, 20180330-173205). En esta carpeta se escriben dos tipos de archivos: el archivo _reason y el archivo de datos. 

Los archivos reason y los archivos de datos tienen el identificador de consulta asociado a la instrucción CTAS. Dado que los datos y reason están en archivos independientes, los archivos correspondientes tienen un sufijo coincidente. 
  
 Sharded external table options  
 Especifica el origen de datos externo (un origen de datos no SQL Server) y un método de distribución para las [consultas de Elastic Database](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 DATA_SOURCE  
 Origen de datos externo, como los datos almacenados en un sistema de archivos de Hadoop, Azure Blob Storage o un [administrador de mapas de particiones](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/).  
  
 SCHEMA_NAME  
 La cláusula SCHEMA_NAME ofrece la posibilidad de asignar la definición de tabla externa a una tabla de otro esquema en la base de datos remota. Úsela para eliminar la ambigüedad entre los esquemas que hay en las bases de datos local y remota.  
  
 OBJECT_NAME  
 La cláusula OBJECT_NAME ofrece la posibilidad de asignar la definición de tabla externa a una tabla con otro nombre en la base de datos remota. Úsela para eliminar la ambigüedad entre los nombres de objetos que hay en las bases de datos local y remota.  
  
 DISTRIBUTION  
 Opcional. Solo se necesita para bases de datos de tipo SHARD_MAP_MANAGER. Controla si una tabla se trata como una tabla con particiones o una tabla replicada. Con las tablas **SHARDED** (*column name*), los datos de las distintas tablas no se superponen. **REPLICATED** especifica que las tablas tienen los mismos datos en cada partición. **ROUND_ROBIN** indica que se usa un método específico de la aplicación para distribuir los datos.  
  
## <a name="permissions"></a>Permisos  
 Requiere estos permisos de usuario:  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 Tenga en cuenta que el inicio de sesión que crea el origen de datos externo debe tener permiso para leer y escribir en el origen de datos externo, ubicado en Hadoop o Azure Blob Storage.  


 > [!IMPORTANT]  

>  El permiso ALTER ANY EXTERNAL DATA SOURCE concede a cualquier entidad de seguridad la capacidad de crear y modificar cualquier objeto de origen de datos externo y, por lo tanto, también permite acceder a todas las credenciales con ámbito de base de datos de la base de datos. Debe considerarse como un permiso con muchos privilegios, por lo que solo debe concederse a las entidades de seguridad de confianza del sistema.

## <a name="error-handling"></a>Tratamiento de errores  
 Al ejecutar la instrucción CREATE EXTERNAL TABLE, PolyBase intenta conectarse al origen de datos externo. Si se produce un error en el intento de conexión, se produce un error en la instrucción y no se crea la tabla externa. El error en el comando puede tardar un minuto o más en producirse, ya que PolyBase vuelve a intentar conectar hasta que al final da como errónea la consulta.  
  
## <a name="general-remarks"></a>Notas generales  
 En escenarios de consulta "ad-hoc", es decir, SELECT FROM EXTERNAL TABLE, PolyBase almacena las filas recuperadas del origen de datos externo en una tabla temporal. Una vez finalizada la consulta, PolyBase quita y elimina la tabla temporal. En las tablas SQL no se almacenan datos permanentes.  
  
 En cambio, en el escenario de importación, es decir, SELECT INTO FROM EXTERNAL TABLE, PolyBase almacena las filas recuperadas del origen de datos externo como datos permanentes en la tabla SQL. La nueva tabla se crea durante la ejecución de la consulta cuando Polybase recupera los datos externos.  
  
 PolyBase puede insertar algunos de los cálculos de la consulta en Hadoop para mejorar el rendimiento. Esto se denomina "aplicación de predicado". Para habilitarlo, especifique la opción de ubicación del administrador de recursos de Hadoop en [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 Puede crear varias tablas externas que hagan referencia a los mismos o a diferentes orígenes de datos externos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 En CTP2, la funcionalidad de exportación no es compatible, es decir, el almacenamiento permanente de datos SQL en el origen de datos externo. Esta funcionalidad estará disponible en CTP3.  
  
 Puesto que los datos de una tabla externa residen fuera del dispositivo, no están bajo el control de PolyBase y un proceso externo puede modificarlos o quitarlos en cualquier momento. Por este motivo, no se garantiza que los resultados de consulta en una tabla externa sean deterministas. La misma consulta puede devolver resultados diferentes cada vez que se ejecute en una tabla externa. Del mismo modo, se puede producir un error en una consulta si se quitan o se reubican los datos externos.  
  
 Puede crear varias tablas externas que hagan referencia a diferentes orígenes de datos externos. Pero si ejecuta consultas de forma simultánea en diferentes orígenes de datos de Hadoop, cada origen de Hadoop debe usar el mismo valor de configuración de servidor 'hadoop connectivity'. Por ejemplo, no se puede ejecutar simultáneamente una consulta en un clúster de Cloudera Hadoop y un clúster de Hortonworks Hadoop, ya que usan valores de configuración diferentes. Para obtener más información sobre los valores de configuración y las combinaciones admitidas, vea [Configuración de conectividad de PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 En tablas externas solo se admiten estas instrucciones de lenguaje de definición de datos (DDL):  
  
-   CREATE TABLE y DROP TABLE  
  
-   CREATE STATISTICS y DROP STATISTICS  
Nota: En Azure SQL Database no se admiten CREATE y DROP STATISTICS en tablas externas. 
  
-   CREATE VIEW y DROP VIEW  
  
 Construcciones y operaciones no admitidas:  
  
-   Restricción DEFAULT en columnas de tabla externa  
  
-   Operaciones de lenguaje de manipulación de datos (DML) delete, insert y update  
  
 Limitaciones de las consultas:  
  
 PolyBase puede usar un máximo de 33.000 archivos por carpeta cuando se ejecutan 32 consultas simultáneas de PolyBase. Esta cifra máxima engloba los archivos y las subcarpetas de cada carpeta de HDFS. Si el grado de simultaneidad es inferior a 32, se pueden ejecutar consultas de PolyBase en carpetas de HDFS que contengan más de 33.000 archivos. Se recomienda tener unas rutas de acceso de archivos externos cortas y no usar más de 30.000 archivos por carpeta de HDFS. Si hay referencias a demasiados archivos, podría producirse una excepción de memoria insuficiente de Máquina virtual Java (JVM).  

Limitaciones de ancho de tabla: PolyBase en SQL Server 2016 tiene un límite de ancho de fila de 32 KB, en función del tamaño máximo de una sola fila válida por definición de tabla. Si la suma del esquema de columnas es superior a 32 KB, PolyBase no puede consultar los datos. 

En SQL Data Warehouse, esta limitación se ha ampliado a 1 MB.


## <a name="locking"></a>Bloqueo  
 Bloqueo compartido en el objeto SCHEMARESOLUTION.  
  
## <a name="security"></a>Seguridad  
 Los archivos de datos de una tabla externa se almacenan en Hadoop o Azure Blob Storage. Son sus propios procesos los que crean y administran estos archivos de datos. Es responsabilidad suya administrar la seguridad de los datos externos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Crear una tabla externa con datos en formato delimitado por texto.  
 En este ejemplo se muestran todos los pasos necesarios para crear una tabla externa que tenga datos con formato de archivos delimitados por texto. Se define un origen de datos externo *mydatasource* y un formato de archivo externo *myfileformat*. Luego se hace referencia a estos objetos de nivel de base de datos en la instrucción CREATE EXTERNAL TABLE. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) y [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
 En este ejemplo se muestran todos los pasos necesarios para crear una tabla externa que tenga datos con formato de RCFiles. Se define un origen de datos externo *mydatasource_rc* y un formato de archivo externo *myfileformat_rc*. Luego se hace referencia a estos objetos de nivel de base de datos en la instrucción CREATE EXTERNAL TABLE. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) y [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
 En este ejemplo se muestran todos los pasos necesarios para crear una tabla externa que tenga datos con formato de archivos ORC. Se define un origen de datos externo mydatasource_orc y un formato de archivo externo myfileformat_orc. Luego se hace referencia a estos objetos de nivel de base de datos en la instrucción CREATE EXTERNAL TABLE. Para obtener más información, vea [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) y [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
 Clickstream es una tabla externa que se conecta con el archivo de texto delimitado employee.tbl en un clúster de Hadoop. La consulta siguiente parece una consulta en una tabla estándar, pero recupera datos de Hadoop y luego calcula los resultados.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Combinar datos de Hadoop con datos SQL  
 Esta consulta parece una operación JOIN estándar en dos tablas SQL. La diferencia es que PolyBase recupera los datos de Clickstream de Hadoop y luego los combina con la tabla UrlDescription. Una tabla es una tabla externa y la otra es una tabla SQL estándar.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importar datos de Hadoop en una tabla SQL  
 En este ejemplo se crea una nueva tabla SQL ms_user que almacena de forma permanente el resultado de una combinación entre la tabla SQL estándar *user* y la tabla externa *ClickStream*.  
  
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
 En este ejemplo se vuelve a asignar una DMV remota a una tabla externa mediante las cláusulas SCHEMA_NAME y OBJECT_NAME.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. Importar datos de ADLS en Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
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
WITH
(
    FORMAT_TYPE = DELIMITEDTEXT 
    , FORMAT_OPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
)


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH
(
    LOCATION='/DimProduct/' , 
    DATA_SOURCE = AzureDataLakeStore , 
    FILE_FORMAT = TextFileFormat , 
    REJECT_TYPE = VALUE ,
    REJECT_VALUE = 0
) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. Combinar tablas externas  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. Combinar datos de HDFS con datos de PDW  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. Importar datos de filas de HDFS en una tabla de PDW distribuida  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. Importar datos de filas de HDFS en una tabla de PDW replicada  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Ver también  
 [Ejemplos de consultas de metadatos comunes (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



