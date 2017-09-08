---
title: Crear externa tabla como SELECT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CREATE EXTERNAL TABLE AS SELECT
- CREATE_EXTERNAL_TABLE_AS_SELECT
- CREATE EXTERNAL TABLE AS SELECT_TSQL
helpviewer_keywords:
- External, table
- PolyBase, external table
- External, table create as select
- PolyBase, create table as select
ms.assetid: 32dfe254-6df7-4437-bfd6-ca7d37557b0a
caps.latest.revision: 16
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 716c0fdaa701865e8d35154cd19068051e0ab017
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-table-as-select-transact-sql"></a>Crear externa tabla como SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Crea una tabla externa y, a continuación, exporta, en paralelo, los resultados de una [!INCLUDE[tsql](../../includes/tsql-md.md)] una instrucción SELECT a Hadoop o blobs de almacenamiento de Azure.  
  
 Utilice la instrucción crear externo tabla AS seleccione (CETAS) para:  
  
-   Exportar una tabla de base de datos al almacenamiento de blobs de Azure o Hadoop.  
  
-   Importar datos desde almacenamiento de blobs de Azure o Hadoop y almacenarlo en la base de datos.  
  
-   Consultar datos desde almacenamiento de blobs de Azure o Hadoop, combinar con tablas de base de datos relacional y reescribir los resultados al almacenamiento de blobs de Azure o Hadoop.  
  
-   Consultar datos desde almacenamiento de blobs de Azure o Hadoop, transformar mediante las capacidades de procesamiento rápido de la base de datos y escribirla de nuevo al almacenamiento de blobs de Azure o Hadoop.  
  
 Para obtener más información, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name   
    WITH (   
        LOCATION = 'hdfs_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
    AS <select_statement>  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
}  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumentos  
 [[ *database_name* . [ *schema_name* ]. ] | *schema_name* . ] *table_name*  
 Uno a tres - parte nombre de la tabla para crear la base de datos. Para una tabla externa, solo los metadatos de la tabla se almacenan en la base de datos relacional.  
  
 UBICACIÓN = '*hdfs_folder*'  
 Especifica dónde se deben escribir los resultados de la instrucción SELECT en el origen de datos externo. La ubicación es un nombre de carpeta y, opcionalmente, puede incluir una ruta de acceso es relativa a la carpeta raíz del Hadoop clúster o blobs de almacenamiento de Azure.  PolyBase creará la ruta de acceso y la carpeta si aún no existe.  
  
 Los archivos externos se escriben en *hdfs_folder* y con nombre *QueryID_date_time_ID.format*, donde *identificador* es un identificador incremental y *formato* es el formato de los datos exportados. Por ejemplo, QID776_20160130_182739_0.orc.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica el nombre del objeto de origen de datos externo que contiene la ubicación donde los datos externos se almacenarán o se almacenarán. La ubicación es un clúster de Hadoop o un Blob de almacenamiento de Azure. Para crear un origen de datos externo, use [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica el nombre del objeto de formato de archivo externo que contiene el formato del archivo de datos externo. Para crear un formato de archivo externo, use [crear EXTERNAL FILE FORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Rechazar opciones  
 Las opciones de rechazo no se aplican en el momento en que se ejecuta esta instrucción CREATE externo TABLE AS SELECT. En su lugar, se especifican aquí para que la base de datos puede utilizar en un momento posterior cuando importa datos de la tabla externa. Posteriormente, cuando la instrucción CREATE TABLE AS SELECT selecciona datos de la tabla externa, la base de datos utilizará las opciones de rechazo para determinar el número o porcentaje de filas que pueden dar error al importar antes de que detenga la importación.  
  
 REJECT_VALUE = *reject_value*  
 Especifica el valor o el porcentaje de filas que pueden dar error al importar antes de base de datos detiene la importación.  
  
 REJECT_TYPE = **valor** | porcentaje  
 Aclara si se especifica la opción REJECT_VALUE como un valor literal o un porcentaje.  
  
 value  
 REJECT_VALUE es un valor literal, no un porcentaje.  La base de datos detendrá la importación de filas del archivo de datos externo cuando supera el número de filas con errores *reject_value*.  
  
 Por ejemplo, si REJECT_VALUE = 5 y REJECT_TYPE = value, la base de datos detendrá la importación de filas después de 5 filas no han podido importar.  
  
 Porcentaje  
 REJECT_VALUE es un porcentaje, no un valor literal. La base de datos detendrá la importación de filas de la externa del archivo de datos cuando el *porcentaje* de filas con errores supera *reject_value*. El porcentaje de filas con errores se calcula a intervalos.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Obligatorio cuando REJECT_TYPE = porcentaje, esta configuración especifica el número de filas que se intenta importar antes de la base de datos vuelve a calcular el porcentaje de filas con errores.  
  
 Por ejemplo, si REJECT_SAMPLE_VALUE = 1000, la base de datos calcula el porcentaje de filas con errores después de que ha intentado importar 1000 filas desde el archivo de datos externo. Si el porcentaje de filas con errores es menor que *reject_value*, la base de datos intentará cargar otro 1000 filas. La base de datos continúa para volver a calcular el porcentaje de filas con errores después de intentar importar cada 1000 filas adicionales.  
  
> [!NOTE]  
>  Puesto que la base de datos calcula el porcentaje de filas con errores a intervalos, puede superar el porcentaje real de filas con errores *reject_value*.  
  
 Ejemplo:  
  
 Este ejemplo muestra cómo interactúan entre sí las tres opciones de rechazo. Por ejemplo, si REJECT_TYPE = porcentaje, REJECT_VALUE = 30 y REJECT_SAMPLE_VALUE = 100, puede producirse el siguiente escenario:  
  
-   La base de datos intenta cargar las 100 primeras filas; 25 producirá un error y 75 se realizan correctamente.  
  
-   Porcentaje de filas con errores se calcula como 25%, que es menor que el valor de rechazo de 30%. Por lo tanto, no es necesario detener la carga.  
  
-   La base de datos intenta cargar las 100 filas; Esta vez correctamente 25 y 75 producirá un error.  
  
-   Se vuelve a calcular el porcentaje de filas con errores como 50%. El porcentaje de filas con errores ha superado el valor de rechazo de 30%.  
  
-   La carga sufre un error con 50% no se pudo filas después de intentar cargar 200 filas, que es mayor que el límite de 30% especificado.  
  
 CON *common_table_expression*  
 Especifica un conjunto de resultados temporal con nombre, conocido como expresión de tabla común (CTE). Para obtener más información, consulte [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Seleccione \<select_criteria > rellena la nueva tabla con los resultados de una instrucción SELECT. *select_criteria* es el cuerpo de la instrucción SELECT que determina qué datos se deben copiar en la nueva tabla. Para obtener información acerca de las instrucciones SELECT, vea [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este comando la **usuario de base de datos** necesita todos estos permisos o las pertenencias a grupos:  
  
-   **ALTER SCHEMA** permiso en el esquema local que contendrá la nueva tabla o la pertenencia a la **db_ddladmin** rol fijo de base de datos.  
  
-   **CREATE TABLE** permiso o la pertenencia a la **db_ddladmin** rol fijo de base de datos.  
  
-   **Seleccione** permiso en cualquier objeto al que hace referencia en el *select_criteria*.  
  
 El inicio de sesión necesita todos estos permisos:  
  
-   **ADMINISTER BULK OPERATIONS** permiso  
  
-   **ALTER ANY EXTERNAL DATA SOURCE** permiso  
  
-   **ALTER ANY EXTERNAL FILE FORMAT** permiso  
  
-   El inicio de sesión debe tener permiso de escritura para leer y escribir en la carpeta externa en el Hadoop clúster o blobs de almacenamiento de Azure.  
 
 > [!IMPORTANT]  
 >  El permiso ALTER ANY EXTERNAL DATA SOURCE concede a cualquier entidad de seguridad de la capacidad de crear y modificar cualquier objeto de origen de datos externo y, por lo tanto, también concede la capacidad de tener acceso a todas las credenciales de ámbito de la base de datos en la base de datos. Este permiso debe considerarse como con altos privilegios y, por tanto, se debe conceder únicamente a las entidades de confianza en el sistema.
  
## <a name="error-handling"></a>Tratamiento de errores  
 Cuando cree externo tabla AS SELECT exporta los datos a un archivo de texto delimitado, no hay ningún archivo de rechazo para las filas que no se pudo exportar.  
  
 Al crear la tabla externa, la base de datos intenta conectarse al clúster de Hadoop externo o Blob de almacenamiento de Azure. Si se produce un error en la conexión, el comando generará un error y no se creará la tabla externa. Puede tardar un minuto o más de un error de comando desde los reintentos de la base de datos la conexión al menos 3 veces.  
  
 Si CREATE externo TABLE AS SELECT se canceló o se produce un error, la base de datos hará que un intento de un solo uso para quitar los nuevos archivos y carpetas ya creadas en el origen de datos externo.  
  
 La base de datos va a notificar los errores de Java que se producen en el origen de datos externo durante la exportación de datos.  
  
##  <a name="GeneralRemarks"></a>Notas generales  
 Una vez finalizada la instrucción CETAS, puede ejecutar [!INCLUDE[tsql](../../includes/tsql-md.md)] las consultas en la tabla externa. Estas operaciones importarán datos en la base de datos para la duración de la consulta, a menos que se importa mediante la instrucción CREATE TABLE AS SELECT.  
  
 El nombre de la tabla externa y la definición se almacenan en los metadatos de la base de datos. Los datos se almacenan en el origen de datos externo.  
  
 Los archivos externos se denominan *QueryID_date_time_ID.format*, donde *ID* es un identificador incremental y *format* es el formato de los datos exportados. Por ejemplo, QID776_20160130_182739_0.orc.  
  
 La instrucción CETAS siempre crea una tabla sin particiones, incluso si la tabla de origen tiene particiones.  
  
 Para los planes de consulta, creado con explicación, el databaseuses estas operaciones del plan de consulta para las tablas externas:  
  
-   Movimiento de orden aleatorio externo  
  
-   Mover difusión externo  
  
-   Movimiento de partición externo  
  
 **Se aplica a:**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]como requisito previo para crear una tabla externa, el administrador del equipo necesario configurar la conectividad de hadoop.   Para obtener más información, vea Configurar la conectividad a datos externos (Analytics Platform System) en la documentación de puntos de acceso que puede descargar desde [aquí](http://www.microsoft.com/download/details.aspx?id=48241).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Puesto que los datos de la tabla externa que se encuentran fuera de la base de datos, copia de seguridad y las operaciones de restauración solo funcionará en datos almacenados en la base de datos. Esto significa que solo los metadatos se copia de seguridad y restaurar.  
  
 La base de datos no comprueba la conexión al origen de datos externo al restaurar una copia de seguridad de base de datos que contiene una tabla externa. Si el origen no está accesible, todavía se realizará correctamente la restauración de metadatos de la tabla externa, pero se producirá un error en las operaciones SELECT en la tabla externa.  
  
 La base de datos no garantiza la coherencia de los datos entre la base de datos y los datos externos. Usted, el cliente es el único responsable para mantener la coherencia entre los datos externos y la base de datos.  
  
 No se admiten operaciones de DML (lenguaje) de manipulación de datos en tablas externas. Por ejemplo, no puede usar el [!INCLUDE[tsql](../../includes/tsql-md.md)] actualizar, insertar o eliminar [!INCLUDE[tsql](../../includes/tsql-md.md)]instrucciones para modificar los datos externos.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW y DROP VIEW son las operaciones de language (DDL) de definición de datos solo permitidas en tablas externas.  
  
 PolyBase puede consumir un máximo de 33 k de archivos por carpeta cuando se ejecutan 32 consultas simultáneas de PolyBase. Este número incluye archivos y subcarpetas en cada carpeta HDFS. Si el grado de simultaneidad es menor que 32, un usuario puede ejecutar las consultas de PolyBase en carpetas en HDFS que contienen archivos de más de 33 k. [!INCLUDE[msCoName](../../includes/msconame-md.md)]recomienda a los usuarios de Hadoop y PolyBase mantener rutas de acceso de archivo cortos y usa archivos de no más de 30 k por carpeta HDFS. Cuando se hace referencia a demasiados archivos que se produce una excepción de memoria insuficiente JVM.  
  
 [SET ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) no tiene ningún efecto en esta CREATE externo TABLE AS SELECT. Para lograr un comportamiento similar, utilice [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 Cuando cree externo tabla AS SELECT selecciona desde un RCFile, los valores de columna en el RCFile no deben contener la canalización ' |' caracteres.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto SCHEMARESOLUTION.  
  
##  <a name="Examples"></a> Ejemplos  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. Crear una tabla de Hadoop mediante crear externo tabla AS seleccione (CETAS)  
 En el ejemplo siguiente se crea una nueva tabla externa denominada `hdfsCustomer`, con las definiciones de columna y los datos de la tabla de origen `dimCustomer`.  
  
 La definición de tabla se almacena en la base de datos y los resultados de la instrucción SELECT se exportan a la ' / pdwdata/customer.tbl' archivo en el origen de datos externo de Hadoop *customer_ds*. El archivo tiene un formato según el formato de archivo externo *customer_ff*.  
  
 El nombre del archivo generado por la base de datos y contiene el identificador de la consulta para facilitar la alineación del archivo con la consulta que lo generó.  
  
 La ruta de acceso `hdfs://xxx.xxx.xxx.xxx:5000/files/` precede el directorio de cliente ya debe existir. Sin embargo, si no existe el directorio de cliente, la base de datos creará el directorio.  
  
> [!NOTE]  
>  En este ejemplo se especifica para 5000. Si no se especifica el puerto, la base de datos utiliza 8020 como el puerto predeterminado.  
  
 El Hadoop resultante será la ubicación y nombre de archivo `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. Utilizar una sugerencia de consulta con CREATE EXTERNAL tabla AS SELECT (CETAS)  
 Esta consulta muestra la sintaxis básica para el uso de una sugerencia de combinación de la consulta con la instrucción CETAS. Después de la consulta se envía a que la base de datos utiliza la estrategia de combinación hash para generar el plan de consulta. Para obtener más información sobre las sugerencias de combinación y cómo usar la cláusula OPTION, consulte [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  En este ejemplo se especifica para 5000. Si no se especifica el puerto, la base de datos utiliza 8020 como el puerto predeterminado.  
  
```  
  
      -- Example is based on AdventureWorks  
CREATE EXTERNAL TABLE dbo.FactInternetSalesNew  
WITH   
    (   
        LOCATION = '/files/Customer',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
    )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [Crear tabla &#40; Almacenamiento de datos SQL Azure, almacenamiento de datos en paralelo &#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [Crear tabla como SELECT &#40; Almacenamiento de datos SQL de Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [Eliminar tabla &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  



