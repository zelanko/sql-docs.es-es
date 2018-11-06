---
title: CREATE EXTERNAL TABLE AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: design
ms.topic: conceptual
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
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9ff275d2aad6d9ccf24ed632a8515e7ce8ea3fc2
ms.sourcegitcommit: b29745051be2326268f165cf72f5eb95dc893564
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2018
ms.locfileid: "50254461"
---
# <a name="create-external-table-as-select-transact-sql"></a>CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Crea una tabla externa y, después, exporta en paralelo los resultados de una instrucción SELECT de [!INCLUDE[tsql](../../includes/tsql-md.md)] a Hadoop o a Azure Storage Blob.  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ [ *database_name*. [ *schema_name* ]. ] | *schema_name*. ] *table_name*  
 Nombre de una, dos o tres partes de la tabla que se va a crear en la base de datos. En el caso de una tabla externa, solo los metadatos de la tabla se almacenan en la base de datos relacional.  
  
 LOCATION =  '*hdfs_folder*'  
 Especifica dónde se deben escribir los resultados de la instrucción SELECT en el origen de datos externo. La ubicación es un nombre de carpeta y puede incluir opcionalmente una ruta de acceso es relativa a la carpeta raíz del clúster de Hadoop o Azure Storage Blob.  PolyBase creará la ruta de acceso y la carpeta si aún no existen.  
  
 Los archivos externos escriben en *hdfs_folder* y se denominan *QueryID_date_time_ID.format*, donde *ID* es un identificador incremental y *format*, el formato de los datos exportados. Por ejemplo, QID776_20160130_182739_0.orc.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica el nombre del objeto de origen de datos externo que contiene la ubicación en donde se almacenan (o se almacenarán) los datos externos. La ubicación es un clúster de Hadoop o un blob de Azure Storage Blob. Para crear un origen de datos externo, use [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica el nombre del objeto de formato de archivo externo que contiene el formato del archivo de datos externos. Para crear un formato de archivo de datos externos, use [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Rechazar opciones  
 Las opciones de rechazo no son aplicables en el momento en que se ejecuta esta instrucción CREATE EXTERNAL TABLE AS SELECT. En su lugar, se especifican aquí para que la base de datos pueda usarlas en un momento posterior, cuando importe datos de la tabla externa. Más adelante, cuando la instrucción CREATE TABLE AS SELECT seleccione datos de la tabla externa, la base de datos usará las opciones de rechazo para determinar el número o el porcentaje de filas que pueden no importarse antes de que la importación se detenga.  
  
 REJECT_VALUE = *reject_value*  
 Especifica el valor o el porcentaje de filas que pueden no importarse antes de que la base de datos detenga la importación.  
  
 REJECT_TYPE = **value** | percentage  
 Aclara si la opción REJECT_VALUE se especifica como un valor literal o como un porcentaje.  
  
 value  
 REJECT_VALUE es un valor literal, no un porcentaje.  La base de datos detendrá la importación de filas del archivo de datos externos cuando el número de filas con errores supere el valor de *reject_value*.  
  
 Por ejemplo, si REJECT_VALUE = 5 y REJECT_TYPE = value, la base de datos detendrá la importación de filas cuando 5 filas no se hayan podido importar.  
  
 percentage  
 REJECT_VALUE es un porcentaje, no un valor literal. La base de datos detendrá la importación de filas del archivo de datos externos cuando el valor de *percentage* de las filas con errores supere el valor de *reject_value*. El porcentaje de filas con errores se calcula a intervalos.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Necesario cuando REJECT_TYPE = percentage. Especifica el número de filas para intentar importarlas antes de que la base de datos recalcule el porcentaje de filas con error.  
  
 Por ejemplo, si REJECT_SAMPLE_VALUE = 1000, la base de datos calculará el porcentaje de filas con errores después de haber intentado importar 1000 filas desde el archivo de datos externos. Si el porcentaje de filas con errores es inferior al valor de *reject_value*, la base de datos intentará cargar otro 1000 filas. La base de datos seguirá recalculando el porcentaje de filas con errores después de intentar importar cada 1000 filas más.  
  
> [!NOTE]  
>  Puesto que la base de datos calcula el porcentaje de filas con errores a intervalos, el porcentaje real de filas con errores puede llegar a superar el valor de *reject_value*.  
  
 Ejemplo:  
  
 En este ejemplo se muestra cómo interactúan entre sí las tres opciones REJECT. Por ejemplo, si REJECT_TYPE = percentage, REJECT_VALUE = 30 y REJECT_SAMPLE_VALUE = 100, sucederá lo siguiente:  
  
-   La base de datos intenta cargar las 100 primeras filas; 25 no se importan y 75 sí.  
  
-   El porcentaje de las filas con errores se calcula en un 25 %, que es menor que el valor de rechazo de 30 %. Por lo tanto, no es necesario detener la carga.  
  
-   La base de datos intenta cargar las 100 primeras filas; esta vez, 25 se importan y 75 no.  
  
-   El porcentaje de filas con errores se recalcula en un 50%. El porcentaje de filas con errores supera pues el valor de rechazo de 30 %.  
  
-   La carga no se efectúa y refleja un 50 % de filas con errores después de intentar cargar 200 filas, lo cual es superior al límite de 30 % especificado.  
  
 WITH *common_table_expression*  
 Especifica un conjunto de resultados temporal con nombre, conocido como expresión de tabla común (CTE). Para más información, vea [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria> Rellena la nueva tabla con los resultados de una instrucción SELECT. *select_criteria* es el cuerpo de la instrucción SELECT que determina qué datos se copian en la nueva tabla. Para más información sobre las instrucciones SELECT, vea [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este comando, el **usuario de base de datos** necesita todos estos permisos o pertenencias a grupos:  
  
-   Permiso **ALTER SCHEMA** en el esquema local que va a contener la nueva tabla o pertenencia al rol fijo de base de datos **db_ddladmin**.  
  
-   Permiso **CREATE TABLE** o pertenencia al rol fijo de base de datos **db_ddladmin**.  
  
-   Permiso **SELECT** en cualquier objeto al que se haga referencia en *select_criteria*.  
  
 El inicio de sesión necesita todos estos permisos:  
  
-   Permiso **ADMINISTER BULK OPERATIONS**  
  
-   Permiso **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   Permiso **ALTER ANY EXTERNAL FILE FORMAT**  
  
-   El inicio de sesión debe tener permiso de escritura para leer y escribir en la carpeta externa en el clúster de Hadoop o Azure Storage Blob.  
 
 > [!IMPORTANT]  
 >  El permiso ALTER ANY EXTERNAL DATA SOURCE concede a cualquier entidad de seguridad la capacidad de crear y modificar cualquier objeto de origen de datos externo y, por lo tanto, también permite obtener acceso a todas las credenciales con ámbito de base de datos de la base de datos. Debe considerarse como un permiso con muchos privilegios, por lo que solo debe concederse a las entidades de seguridad de confianza del sistema.
  
## <a name="error-handling"></a>Tratamiento de errores  
 Cuando CREATE EXTERNAL TABLE AS SELECT exporta los datos a un archivo delimitado de texto, no hay ningún archivo de rechazo para las filas que no se pueden exportar.  
  
 Al crear la tabla externa, la base de datos intenta conectarse al clúster de Hadoop externo o a Azure Storage Blob. Si se produce un error en la conexión, el comando generará un error y no se creará la tabla externa. El comando puede tardar un minuto (o más) en producir un error, ya que la base de datos intenta conectar al menos en tres ocasiones.  
  
 Si CREATE EXTERNAL TABLE AS SELECT se cancela o produce un error, la base de datos realizará un único intento para quitar los nuevos archivos y carpetas que ya se hayan creado en el origen de datos externo.  
  
 La base de datos notificará los errores de Java que se producen en el origen de datos externo durante la exportación de datos.  
  
##  <a name="GeneralRemarks"></a> Notas generales  
 Una vez finalizada la instrucción CREATE EXTERNAL TABLE AS SELECT, se pueden ejecutar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en la tabla externa. Estas operaciones importarán datos a la base de datos el tiempo que dure la consulta, a menos que la importación se realice con la instrucción CREATE TABLE AS SELECT.  
  
 La definición y el nombre de tabla externa se almacenan en los metadatos de la base de datos. Los datos se almacenan en el origen de datos externo.  
  
 Los archivos externos se denominan *QueryID_date_time_ID.format*, donde *ID* es un identificador incremental y *format* es el formato de los datos exportados. Por ejemplo, QID776_20160130_182739_0.orc.  
  
 La instrucción CREATE EXTERNAL TABLE AS SELECT siempre crea una tabla sin particiones, incluso si la tabla de origen tiene particiones.  
  
 En cuanto a los planes de consulta, creados con EXPLAIN, la base de datos emplea estas operaciones de plan de consulta para las tablas externas:  
  
-   Movimiento aleatorio externo  
  
-   Movimiento de difusión externa  
  
-   Movimiento de partición externa  
  
 **SE APLICA A:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Como requisito previo para crear una tabla externa, el administrador del dispositivo debe configurar la conectividad de Hadoop. Para más información, vea la sección sobre cómo configurar la conectividad a datos externos (Analytics Platform System) en la documentación de APS, que puede descargar desde [aquí](http://www.microsoft.com/download/details.aspx?id=48241).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Dado que los datos de la tabla externa están fuera de la base de datos, las operaciones de copia de seguridad y restauración solo funcionarán con los datos almacenados en la base de datos. Esto significa que solo se hará una copia de seguridad y una restauración de los metadatos.  
  
 La base de datos no comprueba la conexión al origen de datos externo al restaurar una copia de seguridad de base de datos que contiene una tabla externa. Si el origen no está accesible, la restauración de metadatos de la tabla externa seguirá realizándose correctamente, pero no se podrán llevar a cabo operaciones SELECT en la tabla externa.  
  
 La base de datos no garantiza la coherencia de los datos entre la base de datos y los datos externos. Usted, como cliente, es el único responsable de mantener la coherencia entre los datos externos y la base de datos.  
  
 No se admiten operaciones de lenguaje de manipulación de datos (DML) en las tablas externas. Por ejemplo, no se pueden usar las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] actualización, inserción o eliminación de [!INCLUDE[tsql](../../includes/tsql-md.md)] para modificar los datos externos.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW y DROP VIEW son las únicas operaciones de lenguaje de manipulación de datos (DDL) que se permiten en las tablas externas.  
  
 PolyBase puede consumir un máximo de 33 000 archivos por carpeta cuando se ejecutan 32 consultas simultáneas de PolyBase. Esta cifra máxima engloba los archivos y las subcarpetas de cada carpeta de HDFS. Si el grado de simultaneidad es inferior a 32, se podrán ejecutar consultas de PolyBase en carpetas de HDFS que contengan más de 33 000 archivos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda a los usuarios de Hadoop y PolyBase tener unas rutas de acceso de archivo cortas y no usar más de 30 000 archivos por carpeta de HDFS. Si hay referencias a demasiados archivos, podría producirse una excepción de memoria insuficiente de JVM.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) no tiene ningún efecto en CREATE EXTERNAL TABLE AS SELECT. Para lograr un comportamiento similar, use [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 Cuando CREATE EXTERNAL TABLE AS SELECT realiza una selección desde un RCFile, los valores de columna del RCFile no deben contener el carácter "|".  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto SCHEMARESOLUTION.  
  
##  <a name="Examples"></a> Ejemplos  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. Crear una tabla de Hadoop con CREATE EXTERNAL TABLE AS SELECT  
 En el siguiente ejemplo se crea una tabla externa denominada `hdfsCustomer`, usando para ello los datos y las definiciones de columna de la tabla de origen `dimCustomer`.  
  
 La definición de tabla se almacena en la base de datos y los resultados de la instrucción SELECT se exportan al archivo "/pdwdata/customer.tbl" en el origen de datos externo de Hadoop *customer_ds*. El archivo tiene un formato acorde al formato de archivo externo *customer_ff*.  
  
 La base de datos genera el nombre de archivo, que contiene el identificador de la consulta para que sea más fácil establecer una correlación entre el archivo y la consulta que lo generó.  
  
 La ruta de acceso `hdfs://xxx.xxx.xxx.xxx:5000/files/` que precede al directorio Customer ya debe existir. Si no existe, la base de datos la creará.  
  
> [!NOTE]  
>  En este ejemplo se especifica el puerto 5000. Si el puerto no se especifica, la base de datos usará 8020 como puerto predeterminado.  
  
 El nombre de archivo y ubicación de Hadoop resultantes serán `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. Usar una sugerencia de consulta con CREATE EXTERNAL TABLE AS SELECT  
 Esta consulta muestra la sintaxis básica para usar una sugerencia de combinación de consulta con la instrucción CREATE EXTERNAL TABLE AS SELECT. Después de enviar la consulta, la base de datos usa la estrategia de combinación hash para generar el plan de consulta. Para más información sobre las sugerencias de combinación y cómo usar la cláusula OPTION, vea [OPTION &#40;cláusula de Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  En este ejemplo se especifica el puerto 5000. Si el puerto no se especifica, la base de datos usará 8020 como puerto predeterminado.  
  
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
  
## <a name="see-also"></a>Ver también  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE TABLE &#40;Azure SQL Data Warehouse, Parallel Data Warehouse&#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)  (CREATE TABLE [Azure SQL Data Warehouse, Almacenamiento de datos paralelo])  
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


