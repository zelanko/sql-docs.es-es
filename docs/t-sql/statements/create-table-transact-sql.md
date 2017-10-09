---
title: Crear tabla (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILESTREAM_TSQL
- TABLE
- CREATE_TABLE_TSQL
- CREATE TABLE
- FILESTREAM
- TABLE_TSQL
- FILESTREAM_ON
- FILESTREAM_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK constraints
- global temporary tables [SQL Server]
- local temporary tables [SQL Server]
- size [SQL Server], tables
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], columns
- maximum number of indexes per table
- number of tables per database
- number of indexes per table
- table creation [SQL Server], CREATE TABLE
- temporary tables [SQL Server], creating
- table size [SQL Server]
- nullability [SQL Server]
- partitioned tables [SQL Server], creating
- DEFAULT definition
- null values [SQL Server], columns
- number of rows per table
- maximum number of columns per table
- FOREIGN KEY constraints, creating
- PRIMARY KEY constraints
- number of bytes per row
- CREATE TABLE statement
- number of columns per table
- maximum number of bytes per row
ms.assetid: 1e068443-b9ea-486a-804f-ce7b6e048e8b
caps.latest.revision: 256
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0978041b1c2683f6af3f6c531ddc10edc6b9bcbf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql"></a>CREATE TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una nueva tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
> [!NOTE]   
>  Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] sintaxis, vea [CREATE TABLE (almacenamiento de datos de SQL Azure)](../../t-sql/statements/create-table-azure-sql-data-warehouse.md).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
--Simple CREATE TABLE Syntax (common if not using options)  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
[ ; ]  
```  
  
## <a name="syntax"></a>Sintaxis  
  
```  
--Disk-Based CREATE TABLE Syntax  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ AS FileTable ]  
    ( {   <column_definition>   
        | <computed_column_definition>    
        | <column_set_definition>   
        | [ <table_constraint> ]   
        | [ <table_index> ] }  
          [ ,...n ]    
          [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name   
             , system_end_time_column_name ) ]  
      )  
    [ ON { partition_scheme_name ( partition_column_name )   
           | filegroup   
           | "default" } ]   
    [ TEXTIMAGE_ON { filegroup | "default" } ]   
    [ FILESTREAM_ON { partition_scheme_name   
           | filegroup   
           | "default" } ]  
    [ WITH ( <table_option> [ ,...n ] ) ]  
[ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ FILESTREAM ]  
    [ COLLATE collation_name ]   
    [ SPARSE ]  
    [ MASKED WITH ( FUNCTION = ' mask_function ') ]  
    [ CONSTRAINT constraint_name [ DEFAULT constant_expression ] ]   
    [ IDENTITY [ ( seed,increment ) ]  
    [ NOT FOR REPLICATION ]   
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]   
    [ NULL | NOT NULL ]  
    [ ROWGUIDCOL ]  
    [ ENCRYPTED WITH   
        ( COLUMN_ENCRYPTION_KEY = key_name ,  
          ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
          ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
        ) ]  
    [ <column_constraint> [ ...n ] ]   
    [ <column_index> ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}   
  
<column_index> ::=   
 INDEX index_name [ CLUSTERED | NONCLUSTERED ]  
    [ WITH ( <index_option> [ ,... n ] ) ]  
    [ ON { partition_scheme_name (column_name )   
         | filegroup_name  
         | default   
         }  
    ]   
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
<computed_column_definition> ::=  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH FILLFACTOR = fillfactor   
          | WITH ( <index_option> [ , ...n ] )  
        ]  
        [ ON { partition_scheme_name ( partition_column_name )   
        | filegroup | "default" } ]  
  
    | [ FOREIGN KEY ]   
        REFERENCES referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
  
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
]   
  
<column_set_definition> ::=  
column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
< table_constraint > ::=  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )   
        [   
            WITH FILLFACTOR = fillfactor   
           |WITH ( <index_option> [ , ...n ] )   
        ]  
        [ ON { partition_scheme_name (partition_column_name)  
            | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )   
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
 

  
< table_index > ::=   
{  
    {  
      INDEX index_name [ CLUSTERED | NONCLUSTERED ]   
         (column_name [ ASC | DESC ] [ ,... n ] )   
    | INDEX index_name CLUSTERED COLUMNSTORE  
    | INDEX index_name [ NONCLUSTERED ] COLUMNSTORE (column_name [ ,... n ] )  
    }  
    [ WITH ( <index_option> [ ,... n ] ) ]   
    [ ON { partition_scheme_name (column_name )   
         | filegroup_name  
         | default   
         }  
    ]   
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
}   


<table_option> ::=  
{  
    [DATA_COMPRESSION = { NONE | ROW | PAGE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]]  
    [ FILETABLE_DIRECTORY = <directory_name> ]   
    [ FILETABLE_COLLATE_FILENAME = { <collation_name> | database_default } ]  
    [ FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = <constraint_name> ]  
    [ FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]  
    [ FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]  
    [ SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name  
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ] ]  
    [ REMOTE_DATA_ARCHIVE =   
      {   
          ON [ ( <table_stretch_options> [,...n] ) ]  
        | OFF ( MIGRATION_STATE = PAUSED )   
      }   
    ]  
}  
  
<table_stretch_options> ::=  
{  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
 }  
  
<index_option> ::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }   
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF}   
  | ALLOW_PAGE_LOCKS ={ ON | OFF}   
  | COMPRESSION_DELAY= {0 | delay [Minutes]}  
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
       [ , ...n ] ) ]  
}  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
```  
  
```  
  
      --Memory optimized CREATE TABLE Syntax  
CREATE TABLE  
    [database_name . [schema_name ] . | schema_name . ] table_name  
    ( { <column_definition>  
    | [ <table_constraint> ] [ ,... n ]  
    | [ <table_index> ]  
      [ ,... n ] }   
      [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name   
        , system_end_time_column_name ) ]  
)  
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]  
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]   
    [ NULL | NOT NULL ]  
[  
    [ CONSTRAINT constraint_name ] DEFAULT memory_optimized_constant_expression ]  
    | [ IDENTITY [ ( 1, 1 ) ]  
]  
    [ <column_constraint> ]  
    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
 [ CONSTRAINT constraint_name ]  
{   
  { PRIMARY KEY | UNIQUE }    
      {   NONCLUSTERED   
        | NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count)   
      }   
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
  | CHECK ( logical_expression )   
}  
  
< table_constraint > ::=  
 [ CONSTRAINT constraint_name ]  
{    
   { PRIMARY KEY | UNIQUE }  
     {   
       NONCLUSTERED (column [ ASC | DESC ] [ ,... n ])  
       | NONCLUSTERED HASH (column [ ,... n ] ) WITH ( BUCKET_COUNT = bucket_count )   
                    }   
    | FOREIGN KEY   
        ( column [ ,...n ] )   
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
    | CHECK ( logical_expression )   
}  
  
<column_index> ::=  
  INDEX index_name  
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)  }  
  
<table_index> ::=  
  INDEX index_name  
{   [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)   
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )   
      [ ON filegroup_name | default ]  
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]  
      [ ON filegroup_name | default ]  
  
}  
  
<table_option> ::=  
{  
    MEMORY_OPTIMIZED = ON   
  | DURABILITY = {SCHEMA_ONLY | SCHEMA_AND_DATA}  
  | SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name  
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ]   
  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos en la que se crea la tabla. *database_name* debe especificar el nombre de una base de datos existente. Si no se especifica, *database_name* el valor predeterminado es la base de datos actual. El inicio de sesión para la conexión actual debe estar asociado con un identificador de usuario existente en la base de datos especificada por *database_name*, y el Id. de usuario debe tener permisos CREATE TABLE.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la nueva tabla.  
  
 *table_name*  
 Es el nombre de la nueva tabla. Los nombres de tabla deben seguir las reglas para [identificadores](../../relational-databases/databases/database-identifiers.md). *table_name* puede tener un máximo de 128 caracteres, excepto para los nombres de tablas temporales locales (nombres precedidos de un solo signo de número (#)) que no puede superar los 116 caracteres.  
  
 AS FileTable 
 
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
 
 Crea la nueva tabla como un objeto FileTable. No es necesario especificar columnas porque un objeto FileTable tiene un esquema fijo. Para obtener más información acerca de las FileTables, consulte [FileTables &#40; SQL Server &#41; ](../../relational-databases/blob/filetables-sql-server.md).  
  
 *column_name*  
 *computed_column_expression*  
 Es una expresión que define el valor de una columna calculada. Una columna calculada es una columna virtual que no está almacenada físicamente en la tabla, a menos que la columna esté marcada con PERSISTED. La columna se calcula a partir de una expresión que utiliza otras columnas de la misma tabla. Por ejemplo, una columna calculada puede tener la definición: **costo** AS **precio** \* **qty**. La expresión puede ser un nombre de columna no calculada, una constante, una función, una variable o cualquier combinación de estos elementos conectados mediante uno o más operadores. La expresión no puede ser una subconsulta ni contener tipos de datos de alias.  
  
 Las columnas calculadas se pueden usar en listas de selección, cláusulas WHERE, cláusulas ORDER BY u otras ubicaciones en que se puedan emplear expresiones regulares, con las siguientes excepciones:  
  
-   Las columnas calculadas deben marcarse como PERSISTED para que puedan participar en restricciones FOREIGN KEY o CHECK.  
  
-   Es posible usar una columna calculada como columna de clave en un índice o como parte de una restricción PRIMARY KEY o UNIQUE, si el valor de la columna calculada se define mediante una expresión determinista y el tipo de datos del resultado está permitido en columnas de índice.  
  
     Por ejemplo, si la tabla tiene las columnas de enteros **una** y **b**, la columna calculada **a + b** puede estar indizada, pero la columna calculada **a + DATEPART (dd, GETDATE()**  no se puede indizar porque el valor puede variar en invocaciones posteriores.  
  
-   Una columna calculada no puede ser el destino de una instrucción INSERT o UPDATE.  
  
> [!NOTE]  
>  Debido a que cada fila de una tabla puede tener distintos valores para las columnas implicadas en una columna calculada, la columna calculada puede no tener el mismo valor para cada fila.  
  
 En función de las expresiones utilizadas, la nulabilidad de las columnas calculadas la determina automáticamente el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Se considera que el resultado de la mayoría de las expresiones admite valores NULL incluso si únicamente están presentes columnas que no admiten valores NULL, ya que los posibles subdesbordamientos o desbordamientos también dan como resultado valores NULL. Utilice la función COLUMNPROPERTY con la **AllowsNull** propiedad para determinar la nulabilidad de las columnas calculadas en una tabla. Una expresión que acepta valores NULL se puede convertir en uno que no los admite si se especifica ISNULL con la *check_expression* constante, donde la constante es un valor no NULL sustituido por cualquier resultado NULL. Requiere el permiso REFERENCES sobre el tipo para las columnas calculadas basadas en expresiones de tipo definido por el usuario de Common Language Runtime (CLR).  
  
 PERSISTED  
 Especifica que [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] almacena físicamente los valores calculados en la tabla y actualiza los valores cuando se actualizan las columnas de las que depende la columna calculada. El hecho de marcar la columna calculada como PERSISTED le permite crear un índice en una columna calculada que es determinista, pero no precisa. Para obtener más información, vea [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md). Las columnas calculadas que se usan como columnas de partición de una tabla con particiones deben marcarse explícitamente como PERSISTED. *computed_column_expression* debe ser determinista cuando se especifica PERSISTED.  
  
 ON { *partition_scheme* | *archivos* | **"**predeterminado**"** }  

 Especifica el esquema de partición o el grupo de archivos en que se almacena la tabla. Si *partition_scheme* se especifica, la tabla es como una tabla con particiones cuyas particiones se almacenan en un conjunto de uno o más grupos de archivos especificado en *partition_scheme*. Si *archivos* se especifica, la tabla se almacena en el grupo de archivos con nombre. El grupo de archivos debe existir en la base de datos. Si **"**predeterminado**"** se especifica, o si no se especifica ON en absoluto, la tabla se almacena en el grupo de archivos predeterminado. El mecanismo de almacenamiento de una tabla según se especifica en CREATE TABLE no se puede modificar posteriormente.  
  
 ON {*partition_scheme* | *archivos* | **"**predeterminado**"**} también puede especificarse en una clave principal o una restricción UNIQUE. Estas restricciones crean índices. Si *archivos* se especifica, el índice se almacena en el grupo de archivos con nombre. Si **"**predeterminado**"** se especifica, o si no se especifica ON en absoluto, el índice se almacena en el mismo grupo de archivos que la tabla. Si la restricción PRIMARY KEY o UNIQUE crea un índice clúster, las páginas de datos de la tabla se almacenan en el mismo grupo de archivos que el índice. Si se especifica CLUSTERED o la restricción crea un índice agrupado y un *partition_scheme* se especifica que difiere de la *partition_scheme* o *delgrupodearchivos* de la definición de la tabla, o viceversa, se respetará la definición de la restricción y la otra se omitirá.  
  
> [!NOTE]  
>  En este contexto, el valor predeterminado no es una palabra clave. Es un identificador para el grupo de archivos predeterminado y debe delimitarse, como en ON **"**predeterminado**"** u ON **[**predeterminado**]**. Si **"**predeterminado**"** se especifica, la opción QUOTED_IDENTIFIER debe ser ON para la sesión actual. Esta es la configuración predeterminada. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
> [!NOTE]  
>  Después de crear una tabla con particiones, considere la posibilidad de establecer la opción LOCK_ESCALATION para la tabla en AUTO. Esto puede mejorar la simultaneidad al permitir que los bloqueos se extiendan al nivel de partición (HoBT) en lugar de la tabla. Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
 TEXTIMAGE_ON { *archivos*| **"**predeterminado**"** }  
 Indica que la **texto**, **ntext**, **imagen**, **xml**, **varchar (max)**,  **nvarchar (max)**, **varbinary (max)**, y las columnas de tipo definido por el usuario CLR (incluyendo geometría y geografía) se almacenan en el grupo de archivos especificado.  
  
 No se permite TEXTIMAGE_ON si no hay columnas de valores grandes en la tabla. No se puede especificar TEXTIMAGE_ON si *partition_scheme* se especifica. Si **"**predeterminado**"** se especifica, o si TEXTIMAGE_ON no se especifica en absoluto, las columnas de valores grandes se almacenan en el grupo de archivos predeterminado. El almacenamiento de los datos de columna de valores grandes especificados en CREATE TABLE no se puede modificar posteriormente.  

> [!NOTE]  
> Varchar (max), nvarchar (max), varbinary (max), xml y valores UDT grandes se almacenan directamente en la fila de datos, hasta un límite de 8.000 bytes y siempre que el valor puede ajustar el registro. Si el valor no cabe en el registro, un puntero se ordena de forma consecutiva y el resto se almacena de manera no consecutiva en el espacio de almacenamiento LOB. 0 es el valor predeterminado.
TEXTIMAGE_ON solo cambia la ubicación de la "espacio de almacenamiento LOB", no afecta a cuando los datos se almacenan de forma consecutiva. Use large value types out row, opción de sp_tableoption para almacenar todo el valor LOB fuera de la fila. 


> [!NOTE]  
>  En este contexto, el valor predeterminado no es una palabra clave. Es un identificador para el grupo de archivos predeterminado y debe delimitarse, como en TEXTIMAGE_ON **"**predeterminado**"** o TEXTIMAGE_ON **[**predeterminado**]**. Si **"**predeterminado**"** se especifica, la opción QUOTED_IDENTIFIER debe ser ON para la sesión actual. Esta es la configuración predeterminada. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 FILESTREAM_ON { *partition_scheme_name* | filegroup | **"**predeterminado**"** } **se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
 
 Especifica el grupo de archivos para los datos FILESTREAM.  
  
 Si la tabla contiene datos FILESTREAM y se crean particiones de la tabla, debe incluirse la cláusula FILESTREAM_ON y debe especificarse un esquema de partición de grupos de archivos FILESTREAM. Este esquema de partición debe utilizar la misma función de partición y las mismas columnas de partición que el esquema de partición para la tabla; de lo contrario, se produce un error.  
  
 Si la tabla no tiene particiones, no se pueden crear particiones en la columna FILESTREAM. Los datos FILESTREAM para la tabla deben almacenarse en un grupo de archivos único. Este grupo de archivos se especifica en la cláusula FILESTREAM_ON.  
  
 Si la tabla no tiene particiones y no se especifica la cláusula FILESTREAM_ON, se utiliza el grupo de archivos FILESTREAM que tenga la propiedad DEFAULT establecida. Si no hay ningún grupo de archivos FILESTREAM, se produce un error.  
  
-   Al igual que con ON y TEXTIMAGE_ON, el valor establecido utilizando CREATE TABLE para FILESTREAM_ON no se puede cambiar, excepto en los casos siguientes:  
  
-   A [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) instrucción convierte un montón en un índice agrupado. En este caso, se puede especificar un grupo de archivos FILESTREAM diferente, un esquema de partición o NULL.  
  
-   A [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) instrucción convierte un índice clúster en un montón. En este caso, un grupo de archivos FILESTREAM diferente, el esquema de partición, o **"**predeterminado**"** puede especificarse.  
  
 El grupo de archivos en el `FILESTREAM_ON <filegroup>` cláusula o cada grupo de archivos FILESTREAM que se menciona en el esquema de partición, debe tener un archivo definido para el grupo de archivos. Este archivo debe definirse mediante un [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) o [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrucción; en caso contrario, se produce un error.  
  
 Para temas relacionados con FILESTREAM, vea [objeto binario grande &#40; BLOB &#41; Datos &#40; SQL Server &#41; ](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 [ *type_schema_name***.** ] *type_name*  
 Especifica el tipo de datos de la columna y el esquema al que pertenece. Para las tablas basadas en disco, el tipo de datos puede ser uno de los siguientes:  
  
-   Tipo de datos del sistema.  
  
-   Un tipo de alias basado en un tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los tipos de datos de alias se crean con la instrucción CREATE TYPE antes de que puedan utilizarse en una definición de tabla. La asignación NULL o NOT NULL de un tipo de datos de alias puede invalidarse durante la instrucción CREATE TABLE. No obstante, la especificación de longitud no se puede cambiar; la longitud del tipo de datos de alias no se puede especificar en una instrucción CREATE TABLE.  
  
-   Un tipo definido por el usuario CLR. Los tipos definidos por el usuario CLR se crean con la instrucción CREATE TYPE para poder utilizarlos en una definición de tabla. Para crear una columna en un tipo definido por el usuario CLR, se necesita el permiso REFERENCES para el tipo.  
  
 Si *type_schema_name* no se especifica, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] referencias *type_name* en el siguiente orden:  
  
-   El tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El esquema predeterminado del usuario actual en la base de datos actual.  
  
-   El esquema **dbo** de la base de datos actual.  
  
 Para las tablas optimizadas en memoria, vea [tipos de datos admitidos para OLTP en memoria](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) para obtener una lista de tipos de sistemas.  
  
 *precisión*  
 Es la precisión del tipo de datos especificado. Para obtener más información acerca de los valores de precisión válidos, consulte [precisión, escala y longitud](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 *escala*  
 Es la escala del tipo de datos especificado. Para obtener más información acerca de los valores de escala válidos, consulte [precisión, escala y longitud](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 **max**  
 Solo se aplica a la **varchar**, **nvarchar**, y **varbinary** tipos de datos para almacenar 2 ^ 31 bytes de caracteres y datos binarios y 2 ^ 30 bytes de datos Unicode.  
  
 CONTENT  
 Especifica que cada instancia de la **xml** tipo de datos en *column_name* puede contener varios elementos de nivel superior. El contenido se aplica solo a la **xml** datos escriba y se puede especificar únicamente si *xml_schema_collection* también se especifica. Si no se especifica, CONTENT es el comportamiento predeterminado.  
  
 DOCUMENT  
 Especifica que cada instancia de la **xml** tipo de datos en *column_name* puede contener un único elemento de nivel superior. DOCUMENTO solo se aplica a la **xml** datos escriba y se puede especificar únicamente si *xml_schema_collection* también se especifica.  
  
 *xml_schema_collection*  
 Solo se aplica a la **xml** tipo de datos para asociar una colección de esquemas XML con el tipo. Antes de escribir un **xml** columna a un esquema, el esquema debe crearse en la base de datos mediante el uso de [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
 DEFAULT  
 Especifica el valor suministrado para la columna cuando no se ha especificado explícitamente un valor durante una inserción. Las definiciones DEFAULT se pueden aplicar a cualquier columna excepto los definidos como **marca de tiempo**, o los que tienen la propiedad IDENTITY. Si se especifica un valor predeterminado para una columna de tipo definido por el usuario, el tipo debe admitir una conversión implícita de *expresiónConstante* para el tipo definido por el usuario. Las definiciones DEFAULT desaparecen cuando se quita la tabla. Como valor predeterminado solo se puede utilizar un valor constante, por ejemplo una cadena de caracteres, una función escalar (función del sistema, definida por el usuario o CLR) o NULL. Para mantener la compatibilidad con las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se puede asignar un nombre de restricción a DEFAULT.  
  
 *expresiónConstante*  
 Es una constante, NULL o una función del sistema que se utiliza como valor predeterminado de una columna.  
  
 *memory_optimized_constant_expression*  
 Es una constante, NULL o una función del sistema que se admite como valor predeterminado de una columna. Debe admitirse en los procedimientos almacenados compilados de forma nativa. Para obtener más información sobre las funciones integradas en procedimientos almacenados compilados de forma nativa, vea [características admitidas para módulos T-SQL compilados forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 IDENTITY  
 Indica que la nueva columna es una columna de identidad. Cuando se agrega una fila nueva a la tabla, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] proporciona un valor incremental único para la columna. Las columnas de identidad se utilizan normalmente con las restricciones PRIMARY KEY como identificadores de fila únicos de la tabla. La propiedad IDENTITY se puede asignar a **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, o **numeric(p,0)** columnas. Solo se puede crear una columna de identidad para cada tabla. Las restricciones DEFAULT y los valores predeterminados enlazados no se pueden utilizar en las columnas de identidad. En este caso, deben especificarse el valor de inicialización y el incremento, o ninguno de esto valores. Si no se especifica ninguno, el valor predeterminado es (1,1).  
  
 En una tabla optimizada en memoria, el único valor permitido tanto para *inicialización* y *incremento* es 1; (1,1) es el valor predeterminado de *inicialización* y *incremento*.  
  
 *valor de inicialización*  
 Es el valor que se utiliza para la primera fila cargada en la tabla.  
  
 *incremento*  
 Es el valor incremental que se agrega al valor de identidad de la fila cargada anterior.  
  
 NOT FOR REPLICATION  
 En la instrucción CREATE TABLE, la cláusula NOT FOR REPLICATION se puede especificar para la propiedad IDENTITY, las restricciones FOREIGN KEY y las restricciones CHECK. Si se especifica esta cláusula para la propiedad IDENTITY, los valores no se incrementan en las columnas de identidad cuando los agentes de replicación realizan inserciones. Si se especifica esta cláusula para una restricción, la restricción no se aplica cuando los agentes de replicación realizan operaciones de inserción, actualización o eliminación.  
  
 SIEMPRE GENERA AS FILA {INICIO | FINALIZAR} [OCULTOS] [NOT NULL]  
 **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica que se utilizará una columna de datetime2 especificado por el sistema para registrar la hora de inicio para el que un registro es válido o la hora de finalización para el que un registro es válido. La columna debe definirse como NOT NULL. Si se intentan volver a especificarlas como NULL, el sistema producirá un error. Si no especifica explícitamente NOT NULL para una columna de período, el sistema definirá la columna como NOT NULL de forma predeterminada. Utilice este argumento junto con el período FOR SYSTEM_TIME y con SYSTEM_VERSIONING = ON argumentos para habilitar el control de versiones de sistema en una tabla. Para obtener más información, consulte [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 Puede marcar una o ambas columnas de periodo con **HIDDEN** marca implícitamente ocultar estas columnas que **seleccione \* FROM**  *`<table>`*  no Devuelve un valor de las columnas. De forma predeterminada, no se ocultan las columnas de periodo. Para poder usarlo, las columnas ocultas deben incluirse explícitamente en todas las consultas que hacen referencia directa a la tabla temporal. Para cambiar la **HIDDEN** atributo para una columna de período existente, **período** debe quitar y volver a crear con una marca oculta diferentes.  
  
 `INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] )`  
     
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Especifica que debe crear un índice en la tabla. Puede tratarse de un índice agrupado o un índice no agrupado. El índice va a contener las columnas enumeradas y ordenará los datos en orden ascendente o descendente.  
  
 ÍNDICE *index_name* CLUSTERED COLUMNSTORE  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Si se especifica para almacenar toda la tabla en formato de columnas con un índice de almacén de columnas agrupado. Esto siempre incluye todas las columnas de la tabla. Los datos no está ordenados en orden alfabético o numérico, ya que las filas se organizan obtener beneficios de compresión de almacén de columnas.  
  
 ÍNDICE *index_name* almacén de columnas [NONCLUSTERED] (*column_name* [,...*n* ] )  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Especifica que debe crear un índice no clúster de almacén de columnas en la tabla. La tabla subyacente puede ser un índice agrupado o montón de almacén de filas, o puede ser un índice de almacén de columnas agrupado. En todos los casos, crear un índice de almacén de columnas no agrupado en una tabla, almacena una segunda copia de los datos de las columnas en el índice.  
  
 El índice de almacén de columnas se almacenan y administran como un índice de almacén de columnas agrupado. Se denomina un índice de almacén de columnas porque las columnas pueden ser limitadas y está presente como un índice secundario en una tabla.  
  
 ON *partition_scheme_name***(***column_name***)**  
 Especifica el esquema de partición que define los grupos de archivos a los que se asignarán las particiones de un índice con particiones. El esquema de partición debe existir en la base de datos mediante la ejecución [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) o [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *column_name* especifica la columna en la que se crearán con particiones un índice con particiones. Esta columna debe coincidir con el tipo de datos, la longitud y la precisión del argumento de la partición de la función que *partition_scheme_name* está usando. *column_name* no está restringida a las columnas de la definición del índice. Puede especificar cualquier columna de la tabla base, excepto cuando un índice único, de creación de particiones *column_name* se debe elegir entre las que se usan como clave única. Esta restricción permite que [!INCLUDE[ssDE](../../includes/ssde-md.md)] compruebe la unicidad de los valores de clave en una única partición solamente.  
  
> [!NOTE]  
>  Cuando se crean particiones en un índice clúster no único, [!INCLUDE[ssDE](../../includes/ssde-md.md)] agrega de forma predeterminada la columna de partición a la lista de claves del índice clúster, en caso de que aún no se hubiera especificado. Cuando se crean particiones en un índice no clúster que tampoco es único, [!INCLUDE[ssDE](../../includes/ssde-md.md)] agrega la columna de partición como una columna sin clave (incluida) del índice, si aún no se especificó.  
  
 Si *partition_scheme_name* o *archivos* no se ha especificado y la tabla tiene particiones, el índice se sitúa en el mismo esquema de partición, con la misma columna de partición que la tabla subyacente.  
  
> [!NOTE]  
>  No se puede especificar un esquema de partición en un índice XML. Si se crean particiones en la tabla base, el índice XML usa el mismo esquema de partición que la tabla.  
  
 Para obtener más información acerca de las particiones de índices, [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 ON *filegroup_name*  
 Crea el índice especificado en el grupo de archivos especificado. Si no se ha especificado una ubicación y la tabla o vista no tiene particiones, el índice utiliza el mismo grupo de archivos que la tabla o vista subyacente. El grupo de archivos debe existir previamente.  
  
 ON **"**predeterminado**"**  
 Crea el índice especificado en el grupo de archivos predeterminado.  
  
 El término predeterminado (default), en este contexto, no es una palabra clave. Es un identificador para el grupo de archivos predeterminado y debe delimitarse, como en ON **"**predeterminado**"** u ON **[**predeterminado**]**. Si se especifica "default", la opción QUOTED_IDENTIFIER debe tener el valor ON para la sesión actual. Esta es la configuración predeterminada. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL"}]  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)].

 Especifica la posición de datos FILESTREAM para la tabla cuando se crea un índice clúster. La cláusula FILESTREAM_ON permite mover los datos FILESTREAM a otro esquema de partición o a otro grupo de archivos FILESTREAM.  
  
 *filestream_filegroup_name* es el nombre de un grupo de archivos FILESTREAM. El grupo de archivos debe tener un archivo que se definen para el grupo de archivos mediante un [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) o [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrucción; en caso contrario, se produce un error.  
  
 Si se crean particiones de la tabla, la cláusula FILESTREAM_ON deberá incluirse y especificar un esquema de partición de grupos de archivos FILESTREAM que utilice la misma función de partición y columnas de partición que el esquema de partición para la tabla. En caso contrario, se produce un error.  
  
 Si la tabla no tiene particiones, no se pueden crear particiones en la columna FILESTREAM. Los datos FILESTREAM para la tabla deben estar almacenados en un grupo de archivos único que se especifica en la cláusula FILESTREAM_ON.  
  
 NULL de FILESTREAM_ON se puede especificar en una instrucción CREATE INDEX si se va a crear un índice clúster y la tabla no contiene una columna FILESTREAM.  
  
 Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 ROWGUIDCOL  
 Indica que la nueva columna es una columna de GUID de filas. Solo un **uniqueidentifier** se puede designar la columna por tabla como columna ROWGUIDCOL. Si se aplica la propiedad ROWGUIDCOL, se puede hacer referencia a la columna mediante $ROWGUID. La propiedad ROWGUIDCOL se puede asignar solo a un **uniqueidentifier** columna. Las columnas de tipos de datos definidos por el usuario no se pueden designar con ROWGUIDCOL.  
  
 La propiedad ROWGUIDCOL no exige que los valores almacenados en la columna sean únicos. ROWGUIDCOL tampoco genera automáticamente valores para nuevas filas insertadas en la tabla. Para generar valores únicos para cada columna, use la [NEWID](../../t-sql/functions/newid-transact-sql.md) o [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) funcionen en [insertar](../../t-sql/statements/insert-transact-sql.md) instrucciones o usar estas funciones como el valor predeterminado para el columna.  
  
 CIFRADO CON  
 Especifica el cifrado de columnas mediante la [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) característica.  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 Especifica la clave de cifrado de columna. Para obtener más información, vea [CREATE COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
 ENCRYPTION_TYPE = {DETERMINISTA | ALEATORIO}  
 El**cifrado determinista** usa un método que genera siempre el mismo valor cifrado para cualquier valor de texto no cifrado concreto. Uso del cifrado determinista permite búsquedas mediante la comparación de igualdad, agrupación y la unión de tablas con combinaciones de igualdad en función de los valores cifrados, pero también puede permitir que los usuarios no autorizados averigüen la información acerca de los valores cifrados examinando los patrones en la columna cifrada. Combina dos tablas en columnas cifradas de manera determinista sólo es posible si ambas columnas se cifran con la misma clave de cifrado de columna. El cifrado determinista debe usar una intercalación de columna con un criterio de ordenación binario 2 para columnas de caracteres.  
  
 El**cifrado aleatorio** utiliza un método que cifra los datos de una manera menos predecible. El cifrado aleatorio es más seguro, pero impide las búsquedas de igualdad, agrupación y la unión en columnas cifradas. No se pueden indizar las columnas que se usa el cifrado aleatorio.  
  
 Utilice el cifrado determinista para las columnas que va a ser parámetros de búsqueda o parámetros de agrupación, por ejemplo un número de identificación de gobierno. Utilice el cifrado aleatorio, para los datos como un número de tarjeta de crédito, que no es agrupado con otros registros, ni se usa para combinar tablas y no que se busca como utilizar otras columnas (por ejemplo, un número de transacciones) para buscar la fila que contiene el cifrado columna de interés.  
  
 Columnas deben ser aplicables al tipo de datos.  
  
 ALGORITMO  
 Debe ser **'AEAD_AES_256_CBC_HMAC_SHA_256'**.  
  
 Para obtener más información, incluidas las restricciones de característica, vea [Always Encrypted &#40; motor de base de datos &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 SPARSE  
 Indica que la columna es una columna dispersa. El almacenamiento de columnas dispersas está optimizado para los valores NULL. Las columnas dispersas no se pueden designar como NOT NULL. Para obtener más información sobre las columnas dispersas y restricciones adicionales, consulte [usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).  
  
 ENMASCARADA con (función = ' *mask_function* ')  
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica una máscara dinámica de datos. *mask_function* es el nombre de la función de enmascaramiento con los parámetros adecuados. Existen tres funciones:  
  
-   es default()  
  
-   Email()  
  
-   Partial()  
  
-   Random()  
  
 Para los parámetros de función, vea [Dynamic Data Masking](../../relational-databases/security/dynamic-data-masking.md).  
  
 FILESTREAM  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)].

 Válido únicamente para **varbinary (max)** columnas. Especifica el almacenamiento FILESTREAM para el **varbinary (max)** datos BLOB.  
  
 La tabla también debe tener una columna de la **uniqueidentifier** tipo de datos que tiene el atributo ROWGUIDCOL. Esta columna no debe permitir valores nulos y debe tener una restricción de columna única UNIQUE o PRIMARY KEY. El valor de GUID de la columna lo debe proporcionar una aplicación cuando se inserten datos o una restricción DEFAULT que use la función NEWID ().  
  
 No se puede quitar la columna ROWGUIDCOL ni se pueden cambiar las restricciones relacionadas si hay definida una columna FILESTREAM para la tabla. Solamente se puede quitar la columna ROWGUIDCOL después de quitarse la última columna FILESTREAM.  
  
 Si se especifica el atributo de almacenamiento FILESTREAM para una columna, todos los valores para dicha columna se almacenan en un contenedor de datos de FILESTREAM del sistema de archivos.  
  
 COLLATE *collation_name*  
 Especifica la intercalación de la columna. Nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. *collation_name* sólo es aplicable para las columnas de la **char**, **varchar**, **texto**, **nchar**, **nvarchar**, y **ntext** tipos de datos. Si no se especifica, se asignará a la columna la intercalación del tipo de datos definido por el usuario, si la columna es de uno de estos tipos, o la intercalación predeterminada de la base de datos.  
  
 Para obtener más información acerca de los nombres de intercalación de Windows y SQL, consulte [nombre de intercalación de Windows](../../t-sql/statements/windows-collation-name-transact-sql.md) y [nombre de intercalación de SQL](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Para obtener más información acerca de la cláusula COLLATE, consulte [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 CONSTRAINT  
 Es una palabra clave opcional que indica el principio de la definición de una restricción PRIMARY KEY, NOT NULL, UNIQUE, FOREIGN KEY o CHECK.  
  
 *constraint_name*  
 Es el nombre de una restricción. Los nombres de restricción deben ser únicos en el esquema al que pertenece la tabla.  
  
 NULL | NOT NULL  
 Determinar si se permiten valores null en la columna. NULL no es estrictamente una restricción, pero se puede especificar, al igual que NOT NULL. NOT NULL solo puede especificarse para las columnas si también se especifica PERSISTED.  
  
 PRIMARY KEY  
 Es una restricción que exige la integridad de entidad para una o varias columnas especificadas a través de un índice único. Solo se puede crear una restricción PRIMARY KEY para cada tabla.  
  
 UNIQUE  
 Es una restricción que proporciona la integridad de entidad para una o varias columnas especificadas a través de un índice único. Las tablas pueden tener varias restricciones UNIQUE.  
  
 CLUSTERED | NONCLUSTERED  
 Indica que se ha creado un índice clúster o no clúster para la restricción PRIMARY KEY o UNIQUE. De forma predeterminada, el valor de las restricciones PRIMARY KEY es CLUSTERED, y el de las restricciones UNIQUE es NONCLUSTERED.  
  
 En una instrucción CREATE TABLE, se puede especificar CLUSTERED tan solo para una restricción. Si se especifica CLUSTERED para una restricción UNIQUE y se especifica también una restricción PRIMARY KEY, el valor predeterminado de PRIMARY KEY es NONCLUSTERED.  
  
 A continuación se muestra cómo utilizar NONCLUSTERED en una tabla basada en disco:  
  
```  
CREATE TABLE t1 ( c1 int, INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t2( c1 int INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t3( c1 int, c2 int INDEX ix_1 NONCLUSTERED)   
CREATE TABLE t4( c1 int, c2 int, INDEX ix_1 NONCLUSTERED (c1,c2))  
```  
  
 FOREIGN KEY REFERENCES  
 Es una restricción que proporciona integridad referencial para los datos de la columna o columnas. Las restricciones FOREIGN KEY requieren que cada valor de la columna exista en la columna o columnas de referencia correspondientes de la tabla a la que se hace referencia. Las restricciones FOREIGN KEY pueden hacer referencia solo a columnas que sean restricciones PRIMARY KEY o UNIQUE en la tabla de referencia o a columnas a las que se haga referencia en UNIQUE INDEX en la tabla de referencia. Las claves externas en las columnas calculadas deben marcarse también como PERSISTED.  
  
 [ *schema_name***.**] *referenced_table_name*]  
 Es el nombre de la tabla a la que hace referencia la restricción FOREIGN KEY y el esquema al que pertenece.  
  
 **(** *ref_column* [ **,**... *n* ] **)**  
 Es una columna o lista de columnas de la tabla a la que hace referencia la restricción FOREIGN KEY.  
  
 AL ELIMINAR { **NINGUNA ACCIÓN** | CASCADE | ESTABLECER COMO NULL | ESTABLECER UN VALOR PREDETERMINADO}  
 Especifica la acción que tiene lugar en las filas de la tabla creada si dichas filas tienen una relación referencial y la fila a la que se hace referencia se elimina de la tabla primaria. El valor predeterminado es NO ACTION.  
  
 NO ACTION  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y se revierte la acción de eliminación de la fila de la tabla primaria.  
  
 CASCADE  
 Si esa fila se elimina de la tabla primaria, las filas correspondientes se eliminan de la tabla de referencia.  
  
 SET NULL  
 Todos los valores que forman la clave externa se establecen en NULL si se elimina la fila correspondiente de la tabla primaria. Para que esta restricción se ejecute, las columnas de clave externa deben aceptar valores NULL.  
  
 SET DEFAULT  
 Todos los valores que forman la clave externa se establecen en los valores predeterminados si se elimina la fila correspondiente de la tabla primaria. Para que esta restricción se ejecute, todas las columnas de clave externa deben tener definiciones predeterminadas. Si una columna acepta valores NULL y no se ha establecido un valor predeterminado explícito, NULL se convierte en el valor predeterminado explícito de dicha columna.  
  
 No especifique CASCADE si la tabla se va a incluir en una publicación de combinación que utiliza registros lógicos. Para obtener más información sobre los registros lógicos, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 No se puede definir ON DELETE CASCADE si ya existe un desencadenador INSTEAD OF en ON DELETE en la tabla en cuestión.  
  
 Por ejemplo, en la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos, el **ProductVendor** tabla tiene una relación referencial con la **proveedor** tabla. El **ProductVendor.BusinessEntityID** referencias de clave externa del **Vendor.BusinessEntityID** clave principal.  
  
 Si se ejecuta una instrucción DELETE en una fila de la **proveedor** tabla y una acción ON DELETE CASCADE se especifica para **ProductVendor.BusinessEntityID**, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] busca dependiente de uno o más las filas de la **ProductVendor** tabla. Si las hay, las filas dependientes de la **ProductVendor** se elimina la tabla, y también hacer referencia la fila en la **proveedor** tabla.  
  
 Por el contrario, si se especifica NO ACTION, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y revierte la acción de eliminación de la **proveedor** fila si hay al menos una fila en la **ProductVendor** tabla que hace referencia a él.  
  
 EN ACTUALIZACIÓN { **NINGUNA ACCIÓN** | CASCADE | ESTABLECER COMO NULL | ESTABLECER UN VALOR PREDETERMINADO}  
 Especifica la acción que se produce en las filas de la tabla modificada cuando esas filas tienen una relación referencial y la fila a la que se hace referencia se actualiza en la tabla primaria. El valor predeterminado es NO ACTION.  
  
 NO ACTION  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y se revierte la acción de actualización de la fila de la tabla primaria.  
  
 CASCADE  
 Si esa fila se actualiza en la tabla primaria, las filas correspondientes se actualizan en la tabla de referencia.  
  
 SET NULL  
 Cuando se actualiza la fila correspondiente en la tabla primaria, todos los valores que componen la clave externa se establecen en NULL. Para que esta restricción se ejecute, las columnas de clave externa deben aceptar valores NULL.  
  
 SET DEFAULT  
 Cuando se actualiza la fila correspondiente en la tabla primaria, todos los valores que componen la clave externa se establecen en sus valores predeterminados. Para que esta restricción se ejecute, todas las columnas de clave externa deben tener definiciones predeterminadas. Si una columna acepta valores NULL y no se ha establecido un valor predeterminado explícito, NULL se convierte en el valor predeterminado explícito de dicha columna.  
  
 No especifique CASCADE si la tabla se va a incluir en una publicación de combinación que utiliza registros lógicos. Para obtener más información sobre los registros lógicos, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 No se puede definir ON UPDATE CASCADE, SET NULL o SET DEFAULT si ya existe un desencadenador INSTEAD OF en ON UPDATE en la tabla que se va a modificar.  
  
 Por ejemplo, en la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos, el **ProductVendor** tabla tiene una relación referencial con la **proveedor** tabla: **ProductVendor.BusinessEntity** referencias de clave externa del **Vendor.BusinessEntityID** clave principal.  
  
 Si se ejecuta una instrucción UPDATE en una fila en la **proveedor** tabla y una acción ON UPDATE CASCADE se especifica para **ProductVendor.BusinessEntityID**, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] busca dependiente de uno o más las filas de la **ProductVendor** tabla. Si las hay, las filas dependientes de la **ProductVendor** se actualiza la tabla, y también hacer referencia la fila en la **proveedor** tabla.  
  
 Por el contrario, si se especifica NO ACTION, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y revierte la acción de actualización de la **proveedor** fila si hay al menos una fila en la **ProductVendor** tabla que hace referencia a él.  
  
 CHECK  
 Es una restricción que exige la integridad del dominio al limitar los valores posibles que se pueden escribir en una o varias columnas. Las restricciones CHECK en las columnas calculadas deben marcarse también como PERSISTED.  
  
 *Filter*  
 Es una expresión lógica que devuelve TRUE o FALSE. Los tipos de datos de alias no pueden formar parte de la expresión.  
  
 *columna*  
 Es una columna o lista de columnas, entre paréntesis, que se utiliza en las restricciones de tabla para indicar las columnas que se están utilizando en la definición de la restricción.  
  
 [ **ASC** | DESC]  
 Especifica cómo se ordenan la columna o las columnas que participan en las restricciones de la tabla. El valor predeterminado es ASC.  
  
 *partition_scheme_name*  
 Es el nombre del esquema de partición que define los grupos de archivos a los que se van a asignar las particiones de una tabla con particiones. El esquema de partición debe existir en la base de datos.  
  
 [ *partition_column_name***.** ]  
 Especifica la columna en la que se van a crear las particiones de la tabla con particiones. La columna debe coincidir con el especificado en la partición de función que *partition_scheme_name* está utilizando en términos de tipo de datos, longitud y precisión. Una columna calculada que participa en una función de partición se debe marcar como PERSISTED de forma explícita.  
  
> [!IMPORTANT]  
>  Se recomienda especificar NOT NULL en la columna de partición de las tablas con particiones y también de las tablas sin particiones que sean orígenes o destinos de operaciones ALTER TABLE...SWITCH. De esta forma se garantiza que las restricciones CHECK en columnas de partición no tengan que comprobar si hay valores NULL.  
  
 CON valor de FILLFACTOR  **=**  *fillfactor*  
 Especifica en qué medida el [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe llenar cada página de índice que se va a utilizar para almacenar los datos de índice. Especificado por el usuario *fillfactor* los valores pueden ser entre 1 y 100. Si no se especifica un valor, el valor predeterminado es 0. Los valores de fill factor 0 y 100 son idénticos.  
  
> [!IMPORTANT]  
>  Documentación de WITH FILLFACTOR = *fillfactor* como la única opción de índice que se aplica a las restricciones PRIMARY KEY o UNIQUE se mantiene por compatibilidad con versiones anteriores, pero no se documentará de esta manera en futuras versiones.  
  
 *nombredeconjuntodecolumnas* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
 Es el nombre del conjunto de columnas. Un conjunto de columnas es una representación XML sin tipo que combina todas las columnas dispersas de una tabla en una salida estructurada. Para obtener más información sobre los conjuntos de columnas, vea [Usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md).  
  
 PERIOD FOR SYSTEM_TIME (*system_start_time_column_name* , *system_end_time_column_name* )  
   
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Especifica los nombres de las columnas que el sistema usará para registrar el período durante el que un registro es válido. Utilice este argumento junto con los GENERADOS siempre AS fila {inicio | FINAL} y con SYSTEM_VERSIONING = ON argumentos para habilitar el control de versiones de sistema en una tabla. Para obtener más información, consulte [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 COMPRESSION_DELAY  
   
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Para una optimización en memoria, retraso especifica el número mínimo de minutos que debe permanecer una fila en la tabla, sin cambios, antes de que sea apto para la compresión en el índice de almacén de columnas. SQL Server selecciona filas específicas a comprimir según su hora de última actualización. Por ejemplo, si va a cambiar filas con frecuencia durante un período de dos horas de tiempo, puede establecer COMPRESSION_DELAY = 120 minutos para asegurarse de que las actualizaciones se completan antes de que SQL Server comprime la fila.  
  
 Para una tabla basada en disco, retraso especifica el número mínimo de minutos que debe permanecer un grupo de filas delta en estado cerrado en el grupo de filas delta antes de que SQL Server puede comprimir en el grupo de filas comprimido. Puesto que las tablas basadas en disco no realizar el seguimiento de insertar y actualizar horas en filas individuales, SQL Server aplica el retraso a grupos de filas delta en estado cerrado.  
  
 El valor predeterminado es 0 minutos.  
  
 Para obtener recomendaciones sobre cuándo usar COMPRESSION_DELAY, consulte [Introducción al almacén de columnas para análisis operativos en tiempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
 \<table_option >:: = especifica una o varias opciones de tabla.  
  
 DATA_COMPRESSION  
 Especifica la opción de compresión de datos para la tabla, el número de partición o el intervalo de particiones especificados. Las opciones son las siguientes:  
  
 NONE  
 No se comprimen la tabla ni las particiones especificadas.  
  
 ROW  
 La tabla o las particiones especificadas se comprimen utilizando la compresión de fila.  
  
 PAGE  
 La tabla o las particiones especificadas se comprimen utilizando la compresión de página.  
  
 COLUMNSTORE  
   
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Solo se aplica a los índices de almacén de columnas, incluidos los clúster y no clúster. Almacén de columnas se especifica para comprimir con la mayor compresión de almacén de columnas de rendimiento. Esta es la opción típica.  
  
 COLUMNSTORE_ARCHIVE  
   
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Solo se aplica a los índices de almacén de columnas, incluidos los clúster y no clúster. COLUMNSTORE_ARCHIVE comprimirá aún más la tabla o partición para reducir su tamaño. Esto se puede usar para el archivado o para otras situaciones que requieran un tamaño de almacenamiento mínimo y pueda permitirse más tiempo para el almacenamiento y recuperación.  
  
 Para obtener más información acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
 EN LAS PARTICIONES **(** { `<partition_number_expression>` | [ **,**... *n* ] **)**  
 Especifica las particiones a las que se aplica el valor DATA_COMPRESSION. Si la tabla no tiene particiones, el argumento ON PARTITIONS generará un error. Si no se proporciona la cláusula ON PARTITIONS, la opción DATA_COMPRESSION se aplicará a todas las particiones de una tabla con particiones.  
  
 *partition_number_expression* se puede especificar de las maneras siguientes:  
  
-   Proporcione el número de una partición, por ejemplo: ON PARTITIONS (2).  
  
-   Proporcionar los números de partición de varias particiones separados por comas, por ejemplo: ON PARTITIONS (1, 5).  
  
-   Proporcione intervalos y particiones individuales, por ejemplo: ON PARTITIONS (2, 4, 6 TO 8).  
  
 `<range>`se puede especificar como números de partición separados por la palabra TO, por ejemplo: ON PARTITIONS (6 a 8).  
  
 Para establecer diferentes tipos de compresión de datos para distintas particiones, especifique la opción DATA_COMPRESSION más de una vez, por ejemplo:  
  
```  
WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
```  
  
 \<index_option >:: =  
 Especifica una o varias opciones de índice. Para obtener una descripción completa de estas opciones, consulte [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON | **OFF** }  
 Cuando es ON, el porcentaje de espacio disponible especificado por FILLFACTOR se aplica a las páginas de nivel intermedio del índice. Cuando es OFF o no se especifica ningún valor de FILLFACTOR, las páginas de nivel intermedio se rellenan casi al máximo de su capacidad dejando espacio suficiente para al menos una fila del tamaño máximo que el índice puede contener teniendo en cuenta el conjunto de claves de las páginas intermedias. El valor predeterminado es OFF.  
  
 Valor de FILLFACTOR  **=**  *fillfactor*  
 Especifica un porcentaje que indica cuánto debe llenar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] el nivel hoja de cada página de índice durante la creación o modificación de los índices. *valor de FILLFACTOR* debe ser un valor entero entre 1 y 100. El valor predeterminado es 0. Los valores de fill factor 0 y 100 son idénticos.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Especifica la respuesta de error cuando una operación de inserción intenta insertar valores de clave duplicados en un índice único. La opción IGNORE_DUP_KEY se aplica solamente a operaciones de inserción realizadas tras crear o volver a generar el índice. La opción no tiene ningún efecto cuando se ejecuta [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), o [actualización](../../t-sql/queries/update-transact-sql.md). El valor predeterminado es OFF.  
  
 ON  
 Se producirá un mensaje de advertencia cuando se inserten valores de clave duplicados en un índice único. Solo las filas que infrinjan la restricción de unicidad darán error.  
  
 OFF  
 Se producirá un mensaje de error cuando se inserten valores de clave duplicados en un índice único. Toda la operación INSERT se revertirá.  
  
 IGNORE_DUP_KEY no se puede establecer en ON para los índices creados en una vista, los índices que no sean únicos, los índices XML, los índices espaciales y los índices filtrados.  
  
 Para ver IGNORE_DUP_KEY, utilice [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 En la sintaxis compatible con versiones anteriores, WITH IGNORE_DUP_KEY es equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | **OFF** }  
 Si es ON, las estadísticas de índices no actualizadas no se vuelven a calcular automáticamente. Si es OFF, se habilita la actualización automática de estadísticas. El valor predeterminado es OFF.  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | {OFF}  
 Si es ON, los bloqueos de fila se permiten al tener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila. Si es OFF, no se utilizan bloqueos de fila. El valor predeterminado es ON.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | {OFF}  
 Si es ON, los bloqueos de página se permiten al tener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página. Si es OFF, no se utilizan bloqueos de página. El valor predeterminado es ON.  
  
 FILETABLE_DIRECTORY = *directory_name*  
   
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica el nombre de directorio de FileTable compatible con windows. Este nombre debe ser único entre todos los nombres de directorio de FileTable en la base de datos. La comparación de unicidad no distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación. Si no se especifica este valor, se usa el nombre de la tabla de archivos.  
  
 FILETABLE_COLLATE_FILENAME = { *collation_name* | database_default}  
   
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica el nombre de la intercalación que se va a aplicar a la columna **Name** en la FileTable. La intercalación no debe distinguir mayúsculas de minúsculas para cumplir con la semántica de nomenclatura de archivos de Windows. Si no se especifica este valor, se usa la intercalación predeterminada de la base de datos. Si la intercalación predeterminada de la base de datos distingue mayúsculas de minúsculas, se genera un error en la operación CREATE TABLE.  
  
 *collation_name*  
 El nombre de una intercalación sin distinción entre mayúsculas y minúsculas.  
  
 database_default  
 Especifica que se debe usar la intercalación predeterminada de la base de datos. Esta intercalación no debe distinguir mayúsculas de minúsculas.  
  
 FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *constraint_name*  
   
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica el nombre que se debe usar para la restricción de clave primaria creada automáticamente en el objeto FileTable. Si no se especifica este valor, el sistema genera un nombre para la restricción.  
  
 FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *constraint_name*  
   
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica el nombre que se usará para la restricción única se crea automáticamente en el **stream_id** columna de FileTable. Si no se especifica este valor, el sistema genera un nombre para la restricción.  
  
 FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *constraint_name*  
   
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica el nombre que se usará para la restricción única se crea automáticamente en el **parent_path_locator** y **nombre** columnas en la tabla FileTable. Si no se especifica este valor, el sistema genera un nombre para la restricción.  
  
 SYSTEM_VERSIONING  **=**  ON [(HISTORY_TABLE  **=**  *schema_name* .  *nombre_de_tabla_de_historial* [, DATA_CONSISTENCY_CHECK  **=**  { **ON** | {OFF}])]  
   
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
  
 Permite el control de versiones de sistema de la tabla si se cumplen el tipo de datos, restricciones de nulabilidad y requisitos de la restricción de clave principal. Si el **HISTORY_TABLE** no se utiliza el argumento, el sistema genera una nueva tabla de historial que coinciden con el esquema de la tabla actual en el mismo grupo de archivos como la tabla actual, crear un vínculo entre las dos tablas y permite al sistema registrar el historial de cada registro de la tabla actual en la tabla de historial. El nombre de esta tabla de historial será `MSSQL_TemporalHistoryFor<primary_table_object_id>`. De forma predeterminada, es la tabla de historial es **PAGE** comprimida. Si el argumento HISTORY_TABLE se utiliza para crear un vínculo a y usar una tabla de historial existente, se crea el vínculo entre la tabla actual y la tabla especificada. Si la tabla actual tiene particiones, la tabla de historial se crea en el grupo de archivos predeterminado, ya que la configuración de particiones no se replica automáticamente desde la tabla actual a la de historial. Si el nombre de una tabla de historial se especifica durante su creación, debe determinar el nombre del esquema y la tabla. Al crear un vínculo a una tabla de historial existente, puede realizar una comprobación de coherencia de datos. Esta comprobación de coherencia de datos garantiza que los registros existentes no se superponen. La comprobación de coherencia de datos se realiza de manera predeterminada. Utilice este argumento junto con el período FOR SYSTEM_TIME y genera siempre AS fila {inicio | Argumentos de finalización} para habilitar el control de versiones de sistema en una tabla. Para obtener más información, consulte [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 REMOTE_DATA_ARCHIVE = {ON [( *table_stretch_options* [,... n])] | DESACTIVAR (MIGRATION_STATE = EN PAUSA)}  
   
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Crea la nueva tabla con Stretch Database habilitado o deshabilitado. Para obtener más información, vea [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 **Para habilitar Stretch Database para una tabla**  
  
 Al habilitar Stretch para una tabla especificando `ON`, también se puede especificar `MIGRATION_STATE = OUTBOUND` para empezar a migrar los datos inmediatamente, o `MIGRATION_STATE = PAUSED` para posponer la migración de datos. El valor predeterminado es `MIGRATION_STATE = OUTBOUND`. Para obtener más información sobre la habilitación de Stretch para una tabla, vea [Enable Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
 **Requisitos previos**. Antes de habilitar Stretch para una tabla, tendrá que habilitar Stretch en el servidor y en la base de datos. Para obtener más información, vea [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 **Permisos**. Habilitación de Stretch para una base de datos o una tabla, requiere permisos db_owner. Habilitación de Stretch para una tabla, también requiere permisos ALTER en la tabla.  
  
 [FILTER_PREDICATE = {null | *predicado* }]  
   
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Opcionalmente, especifica un predicado de filtro para seleccionar las filas para migrar de una tabla que contiene datos históricos y actuales. El predicado debe llamar a una función con valores de tabla de determinista en línea. Para obtener más información, consulte [Enable Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) y [seleccionar filas para migrar mediante una función de filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). 
   
> [!IMPORTANT]  
>  Si se indica un predicado de filtro que tiene un rendimiento bajo, la migración de datos también tendrá un rendimiento bajo. Stretch Database aplica el predicado de filtro a la tabla mediante el operador CROSS APPLY.  
  
 Si no se especifica un predicado de filtro, se migrará toda la tabla.  
  
 Cuando se especifica un predicado de filtro, también tiene que especificar *MIGRATION_STATE*.  
  
 MIGRATION_STATE = {SALIENTE |  ENTRADA | EN PAUSA}  
   
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]y SQL Azure. 
  
-   Especificar `OUTBOUND` para migrar datos de SQL Server en Azure.  
  
-   Especificar `INBOUND` para copiar el control remoto copia los datos de la tabla de Azure para SQL Server y deshabilitar Stretch para la tabla. Para obtener más información, vea [Deshabilitar Stretch Database y recuperar datos remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
     Esta operación conlleva gastos de transferencia de datos y no se puede cancelar.  
  
-   Especificar `PAUSED` para pausar o posponer la migración de datos. Para obtener más información, consulte [pausar y reanudar la migración de datos &#40; Ajuste de la base de datos &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
 MEMORY_OPTIMIZED  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 El valor ON indica que la tabla está optimizado en memoria. Tablas optimizadas en memoria forman parte de la característica de OLTP en memoria, que se usa para un mejor el rendimiento del procesamiento de transacciones. Para empezar a trabajar con OLTP en memoria vea [inicio rápido 1: tecnologías de OLTP en memoria para el rendimiento de Transact-SQL con mayor rapidez](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md). Para obtener información más detallada acerca de las tablas optimizadas en memoria vea [tablas con optimización para memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 El valor predeterminado OFF indica que la tabla está basado en disco.  
  
 DURABILITY  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
  
 El valor de SCHEMA_AND_DATA indica que la tabla es duradera, lo que significa que los cambios se conservan en disco y sobreviven a reiniciar o conmutar por error.  SCHEMA_AND_DATA es el valor predeterminado.  
  
 El valor de SCHEMA_ONLY indica que la tabla no es perdurable. El esquema de tabla se conserva, pero ninguna actualización de datos no es persistentes tras un reinicio o conmutación por error de la base de datos. DURABILITY = SCHEMA_ONLY solo se permite con MEMORY_OPTIMIZED = ON.  
  
> [!WARNING]  
>  Cuando se crea una tabla con **DURABILITY = SCHEMA_ONLY**, y **READ_COMMITTED_SNAPSHOT** se cambia posteriormente mediante **ALTER DATABASE**, se perderán los datos de la tabla.  
  
 BUCKET_COUNT  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. 
  
 Indica el número de cubos que se deben crear en el índice hash. El valor máximo para BUCKET_COUNT en índices hash es 1 073 741 824. Para obtener más información acerca de números de depósitos, consulte [índices para tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  
  
 Bucket_count es un argumento requerido.  
  
 INDEX  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. 
  
Índices de columna y tabla pueden especificarse como parte de la instrucción CREATE TABLE. Para obtener más información sobre cómo agregar y quitar índices en tablas optimizadas en memoria, consulte: [modificar tablas](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)
  
 HASH  
   
  
**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. 
  
 Indica que se ha creado un índice HASH.  
  
 Los índices hash solo se admiten en las tablas con optimización para memoria.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener información sobre el número de tablas permitidas, columnas, restricciones e índices, vea [especificaciones de capacidad máxima para SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
 Normalmente, el espacio se asigna a las tablas e índices en incrementos de una extensión cada vez. Cuando la opción SET MIXED_PAGE_ALLOCATION de ALTER DATABASE se establece en TRUE, o siempre anteriores a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], cuando se crea una tabla o índice, se le asignan páginas de extensiones mixtas hasta que tiene suficientes páginas para llenar una extensión uniforme. Una vez que haya suficientes páginas para llenar una extensión uniforme, se asigna otra extensión cada vez que se llenan las extensiones asignadas actualmente. Para obtener un informe sobre la cantidad de espacio asignado y utilizado por una tabla, ejecute **sp_spaceused**.  
  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no exige el orden en que DEFAULT, IDENTITY, ROWGUIDCOL o las restricciones de columna se especifican en una definición de columna.  
  
 Al crear una tabla, la opción QUOTED IDENTIFIER siempre se almacena como ON en los metadatos de la tabla incluso si la opción está establecida en OFF al crear la tabla.  
  
## <a name="temporary-tables"></a>Tablas temporales  
 Se pueden crear tablas temporales locales y globales. Las tablas temporales locales son visibles solo en la sesión actual y las tablas temporales globales son visibles para todas las sesiones. No se pueden crear particiones en las tablas temporales.  
  
 Prefijo de nombres de tabla temporal local con solo signo de número (#*table_name*), el prefijo de nombres de tabla temporal global con un signo de número doble (##*table_name*).  
  
 Las instrucciones SQL hacen referencia a la tabla temporal mediante el valor especificado para *table_name* en la instrucción CREATE TABLE, por ejemplo ###:  
  
```  
CREATE TABLE #MyTempTable (cola INT PRIMARY KEY);  
  
INSERT INTO #MyTempTable VALUES (1);  
```  
  
 Si se ha creado más de una tabla temporal en un único procedimiento almacenado o lote, deben tener nombres distintos.  
  
 Si se crea una tabla temporal local en un procedimiento almacenado o una aplicación que varios usuarios pueden ejecutar al mismo tiempo, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] tiene que ser capaz de distinguir las tablas creadas por los distintos usuarios. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] realiza esto anexando internamente un sufijo numérico a cada nombre de tabla temporal local. El nombre completo de una tabla temporal tal como se almacena en la **sysobjects** tabla **tempdb** está formada por el nombre de tabla especificado en la instrucción CREATE TABLE y el sufijo numérico generado por el sistema. Para permitir el sufijo, *table_name* especificado para un nombre temporal local no puede superar los 116 caracteres.  
  
 Las tablas temporales se quitan automáticamente cuando están fuera de ámbito, a menos que ya se hayan quitado explícitamente mediante el uso de DROP TABLE:  
  
-   Una tabla temporal local creada en un procedimiento almacenado se quita automáticamente cuando se completa el procedimiento almacenado. Cualquiera de los procedimientos almacenados anidados ejecutados por el procedimiento almacenado que creó la tabla puede hacer referencia a la tabla. El proceso que llamó al procedimiento almacenado que creó la tabla no puede hacer referencia a la tabla.  
  
-   Las demás tablas temporales se quitan automáticamente al final de la sesión actual.  
  
-   Las tablas temporales globales se quitan automáticamente cuando la sesión que creó la tabla finaliza y las tareas restantes han dejado de hacer referencia a ellas. La asociación entre una tarea y una tabla se mantiene solo durante la vida de una única instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esto significa que la tabla temporal global se quita al finalizar la última instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que estuviera haciendo referencia activa a la tabla cuando finalizó la sesión que la creó.  
  
 Una tabla temporal local creada en un procedimiento almacenado o un desencadenador puede tener el mismo nombre que una tabla temporal creada antes de que se llame al procedimiento almacenado o al desencadenador. No obstante, si una consulta hace referencia a una tabla temporal y hay dos tablas temporales con el mismo nombre en ese momento, no está definido en cuál de las dos tablas debe resolverse la consulta. Los procedimientos almacenados anidados pueden crear también tablas temporales con el mismo nombre que la tabla temporal creada por el procedimiento almacenado que la llamó. Sin embargo, en el caso de las modificaciones que se van a resolver en la tabla creada en el procedimiento anidado, la tabla debe tener la misma estructura, con los mismos nombres de columna, que la tabla creada en el procedimiento que realiza la llamada. Esto se muestra en el ejemplo siguiente.  
  
```  
CREATE PROCEDURE dbo.Test2  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (2);  
    SELECT Test2Col = x FROM #t;  
GO  
  
CREATE PROCEDURE dbo.Test1  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (1);  
    SELECT Test1Col = x FROM #t;  
EXEC Test2;  
GO  
  
CREATE TABLE #t(x INT PRIMARY KEY);  
INSERT INTO #t VALUES (99);  
GO  
  
EXEC Test1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 (1 row(s) affected) 
 Test1Col 
 ----------- 
 1 

 (1 row(s) affected) 
 Test2Col 
 ----------- 
 2 
 ```
  
 Cuando se crean tablas temporales globales o locales, la sintaxis de CREATE TABLE admite la definición de restricciones, excepto restricciones FOREIGN KEY. Si se especifica una restricción FOREIGN KEY en una tabla temporal, la instrucción devuelve un mensaje de advertencia que indica que la restricción se ha omitido. La tabla se sigue creando sin las restricciones FOREIGN KEY. En las restricciones FOREIGN KEY no se puede hacer referencia a tablas temporales.  
  
 Si una tabla temporal se crea con una restricción con nombre y la tabla temporal se crea dentro del ámbito de una transacción definida por el usuario, solo un usuario a la vez puede ejecutar la instrucción que crea la tabla temporal. Por ejemplo, si un procedimiento almacenado crea una tabla temporal con una restricción de clave principal con nombre, el procedimiento almacenado no puede ser ejecutado a la vez por varios usuarios.  


## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>Ámbito de base de datos de las tablas temporales globales (base de datos de SQL Azure)

Las tablas temporales globales para SQL Server (iniciar con ## nombre de tabla) se almacenan en tempdb y se comparten entre las sesiones de todos los usuarios en toda la instancia de SQL Server. Para obtener información sobre los tipos de tablas SQL, vea la sección anterior sobre crear tablas.  

La base de datos de SQL Azure es compatible con las tablas temporales globales que también se almacenan en tempdb y el ámbito de nivel de base de datos.  Esto significa que las tablas temporales globales se comparten en las sesiones de todos los usuarios dentro de la misma base de datos de SQL Azure. Las sesiones de usuario de otras bases de datos de SQL Azure no pueden tener acceso a las tablas temporales globales.

Las tablas temporales globales para la base de datos de SQL Azure siguen la misma sintaxis y semántica de SQL Server se utiliza para las tablas temporales.  De forma similar, los procedimientos almacenados temporales globales también se centran en el nivel de base de datos en la base de datos de SQL Azure. Las tablas temporales locales (que se inicia con el nombre de la tabla de #) también se admiten para la base de datos de SQL Azure y siguen la misma sintaxis y semántica que usa SQL Server.  Vea la sección anterior sobre [tablas temporales](#temporary-tables).  

> [!IMPORTANT]
> Esta característica está en versión preliminar pública y está disponible para la base de datos de SQL Azure.
>

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-db"></a>Solución de problemas de las tablas temporales globales para la base de datos de SQL Azure 

Para la solución de problemas de tempdb, vea [solución de problemas de suficiente espacio en disco en tempdb](https://technet.microsoft.com/library/ms176029%28v=sql.105%29.aspx?f=255&MSPPError=-2147217396). Para obtener acceso a las DMV para solucionar problemas en la base de datos de SQL Azure, debe ser un administrador del servidor.
  
### <a name="permissions"></a>Permissions  

 Cualquier usuario puede crear objetos temporales globales. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. .  
  
### <a name="examples"></a>Ejemplos 

- Sesión A crea una tabla temporal global ##test en testdb1 de base de datos de SQL Azure y agrega 1 fila

```tsql
CREATE TABLE ##test ( a int, b int);
INSERT INTO ##test values (1,1);

--Obtain object ID for temp table ##test 
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID'; 

---Result
1253579504

---Obtain global temp table name for a given object ID 1253579504 in tempdb (2)
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504

---Result
##test
```
- Sesión B se conecta a la base de datos de SQL Azure testdb1 y puede tener acceso a la tabla ##test creados por la sesión A

```tsql
SELECT * FROM ##test
---Results
1,1
```

- Sesión C se conecta a otra base de datos testdb2 de base de datos de SQL Azure y desea obtener acceso a ##test creado en testdb1. Esta instrucción select falla debido a que el ámbito de la base de datos de las tablas temporales globales 

```tsql
SELECT * FROM ##test
---Results
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

- Objeto de sistema de direccionamiento en tempdb de la base de datos de SQL Azure de testdb1 de base de datos de usuario actual

```tsql
SELECT * FROM tempdb.sys.objects
SELECT * FROM tempdb.sys.columns
SELECT * FROM tempdb.sys.database_files
```



## <a name="partitioned-tables"></a>Tablas con particiones  
 Antes de crear una tabla con particiones mediante CREATE TABLE, debe crear una función de partición para especificar cómo se van a crear las particiones en la tabla. Se crea una función de partición mediante [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md). A continuación, debe crear un esquema de partición para especificar los grupos de archivos que van a contener las particiones indicadas mediante la función de partición. Se crea un esquema de partición mediante [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). La colocación de restricciones PRIMARY KEY o UNIQUE para separar grupos de archivos no se puede especificar para las tablas con particiones. Para obtener más información, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
## <a name="primary-key-constraints"></a>Restricciones PRIMARY KEY  
  
-   Una tabla solo puede incluir una restricción PRIMARY KEY.  
  
-   El índice generado por una restricción PRIMARY KEY no puede hacer que el número de índices de la tabla supere 999 índices no clúster y 1 índice clúster.  
  
-   Si no se especifica CLUSTERED o NONCLUSTERED para una restricción PRIMARY KEY, se utiliza CLUSTERED si no hay índices clúster especificados para las restricciones UNIQUE.  
  
-   Todas las columnas definidas en una restricción PRIMARY KEY se deben definir como NOT NULL. Si no se especifica nulabilidad, la nulabilidad de todas las columnas que participan en una restricción PRIMARY KEY se establece en NOT NULL.  
  
    > [!NOTE]  
    >  Para las tablas optimizadas en memoria, se permite la columna de clave que aceptan valores NULL.  
  
-   Si la clave principal se define en una columna de tipo definido por el usuario CLR, la implementación del tipo debe admitir el orden binario. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="unique-constraints"></a>Restricciones UNIQUE  
  
-   Si no se especifica CLUSTERED o NONCLUSTERED para una restricción UNIQUE, de forma predeterminada se utiliza NONCLUSTERED.  
  
-   Cada restricción UNIQUE genera un índice. El número de restricciones UNIQUE no puede hacer que el número de índices de la tabla supere los 999 índices no clúster y 1 índice clúster.  
  
-   Si se define una restricción única en una columna de tipo definido por el usuario CLR, la implementación del tipo debe admitir el orden binario o el orden basado en el operador. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="foreign-key-constraints"></a>Restricciones FOREIGN KEY  
  
-   Si se especifica un valor distinto de NULL en la columna de una restricción FOREIGN KEY, el valor debe existir en la columna a que se hace referencia; de lo contrario, se devolverá un error de infracción de clave externa.  
  
-   Las restricciones FOREIGN KEY se aplican a la columna anterior, a menos que se especifiquen columnas de origen.  
  
-   Las restricciones FOREIGN KEY solo pueden hacer referencia a las tablas de la misma base de datos en el mismo servidor. La integridad referencial entre bases de datos debe implementarse a través de desencadenadores. Para obtener más información, vea [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
-   Las restricciones FOREIGN KEY pueden hacer referencia a otras columnas de la misma tabla. Esto recibe el nombre de autorreferencia.  
  
-   La cláusula REFERENCES de una restricción FOREIGN KEY de nivel de columna solo puede incluir una columna de referencia. Esta columna debe tener el mismo tipo de datos que la columna en la que se define la restricción.  
  
-   La cláusula REFERENCES de una restricción FOREIGN KEY de nivel de tabla debe tener el mismo número de columnas de referencia que la lista de columnas de la restricción. El tipo de datos de cada columna de referencia debe ser también el mismo que el de la columna correspondiente de la lista de columnas.  
  
-   No se puede especificar CASCADE, SET NULL o SET DEFAULT si una columna de tipo **timestamp** forma parte de la clave externa o la clave que se hace referencia.  
  
-   CASCADE, SET NULL, SET DEFAULT y NO ACTION se pueden combinar en las tablas con relaciones referenciales entre sí. Si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] detecta NO ACTION, detiene y revierte las acciones CASCADE, SET NULL y SET DEFAULT relacionadas. Cuando una instrucción DELETE hace que se combinen las acciones CASCADE, SET NULL, SET DEFAULT y NO ACTION, todas las acciones CASCADE, SET NULL y SET DEFAULT se aplican antes de que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] compruebe la existencia de NO ACTION.  
  
-   El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no tiene un límite predefinido para el número de restricciones FOREIGN KEY que una tabla que hace referencia a otras tablas puede contener, o para el número de restricciones FOREIGN KEY pertenecientes a otras tablas que hacen referencia a una tabla específica.  
  
     No obstante, el número real de restricciones FOREIGN KEY que se puede utilizar está limitado por la configuración del hardware y por el diseño de la base de datos y de la aplicación. Se recomienda que la tabla no contenga más de 253 restricciones FOREIGN KEY y que no más de 253 restricciones FOREIGN KEY hagan referencia a ella. El límite real en cada caso puede variar en función de la aplicación y el hardware. Debe tener en cuenta el costo que supone la exigencia de restricciones FOREIGN KEY al diseñar la base de datos y las aplicaciones.  
  
-   Las restricciones FOREIGN KEY no se exigen en tablas temporales.  
  
-   Las restricciones FOREIGN KEY solo pueden hacer referencia a columnas de restricciones PRIMARY KEY o UNIQUE de la tabla a la que se hace referencia o a columnas en UNIQUE INDEX de dicha tabla.  
  
-   Si la clave externa se define en una columna de tipo definido por el usuario CLR, la implementación del tipo debe admitir el orden binario. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
-   Las columnas que participan en una relación de claves externas deben estar definidas con la misma longitud y escala.  
  
## <a name="default-definitions"></a>Definiciones DEFAULT  
  
-   Una tabla solo puede incluir una definición DEFAULT.  
  
-   Una definición DEFAULT puede contener valores constantes, funciones, funciones niládicas estándar de SQL o NULL. En la siguiente tabla se muestran las funciones niládicas y los valores que devuelven para el valor predeterminado durante la ejecución de una instrucción INSERT.  
  
    |Función niládica SQL-92|Valor devuelto|  
    |------------------------------|--------------------|  
    |CURRENT_TIMESTAMP|Fecha y hora actuales.|  
    |CURRENT_USER|Nombre del usuario que realiza la inserción.|  
    |SESSION_USER|Nombre del usuario que realiza la inserción.|  
    |SYSTEM_USER|Nombre del usuario que realiza la inserción.|  
    |User|Nombre del usuario que realiza la inserción.|  
  
-   *expresiónConstante* en el valor predeterminado es definición no puede hacer referencia a otra columna de la tabla o a otras tablas, vistas o procedimientos almacenados.  
  
-   Las definiciones DEFAULT no se puede crear en columnas con un **timestamp** tipo de datos o las columnas con una propiedad IDENTITY.  
  
-   Las definiciones DEFAULT no se pueden crear para columnas con tipos de datos de alias si estos están enlazados a un objeto predeterminado.  
  
## <a name="check-constraints"></a>Restricciones CHECK  
  
-   Una columna puede tener cualquier número de restricciones CHECK y la condición puede incluir varias expresiones lógicas combinadas con AND y OR. Varias restricciones CHECK para una columna se validan en el orden en que se crean.  
  
-   La condición de búsqueda debe evaluarse como una expresión booleana y no puede hacer referencia a otra tabla.  
  
-   Una restricción CHECK en el nivel de columna solo puede hacer referencia a la columna restringida y una restricción CHECK en el nivel de tabla solo puede hacer referencia a columnas de la misma tabla.  
  
     Las restricciones CHECK y las reglas sirven para la misma función de validación de los datos durante las instrucciones INSERT y UPDATE.  
  
-   Cuando hay una regla y una o más restricciones CHECK para una o varias columnas, se evalúan todas las restricciones.  
  
-   Las restricciones CHECK no pueden definirse en **texto**, **ntext**, o **imagen** columnas.  
  
## <a name="additional-constraint-information"></a>Información adicional sobre las restricciones  
  
-   Un índice creado para una restricción no se puede quitar usando DROP INDEX; la restricción debe quitarse con ALTER TABLE. Un índice creado para una restricción y usado por ella se puede volver a generar mediante ALTER INDEX...REBUILD. Para obtener más información, vea [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Nombres de restricción deben seguir las reglas para [identificadores](../../relational-databases/databases/database-identifiers.md), excepto en que el nombre no puede comenzar con un signo de número (#). Si *constraint_name* no es se proporciona, se asigna un nombre generado por el sistema a la restricción. El nombre de la restricción aparece en todos los mensajes de error relativos a infracciones de la restricción.  
  
-   Cuando se infringe una restricción en una instrucción INSERT, UPDATE o DELETE, la instrucción finaliza. Sin embargo, si SET XACT_ABORT se establece en OFF y la instrucción forma parte de una transacción explícita, continúa el procesamiento de la transacción. Si SET XACT_ABORT se establece en ON, se revierte toda la transacción. También puede usar la instrucción ROLLBACK TRANSACTION con la definición de transacción activando el @@ERROR función del sistema.  
  
-   Si ALLOW_ROW_LOCKS = ON y ALLOW_PAGE_LOCK = ON, los bloqueos de nivel de fila, página y tabla se permiten al tener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] elige el bloqueo apropiado y puede cambiar de escala el bloqueo: de un bloqueo de fila o página a un bloqueo de tabla. Si ALLOW_ROW_LOCKS = OFF y ALLOW_PAGE_LOCK = OFF, solo se permiten los bloqueos de nivel de tabla cuando se tiene acceso al índice.  
  
-   Si una tabla tiene restricciones FOREIGN KEY o CHECK, y desencadenadores, las condiciones de restricción se evalúan antes de que se ejecute el desencadenador.  
  
 Para obtener un informe en una tabla y sus columnas, utilice **sp_help** o **sp_helpconstraint**. Para cambiar el nombre de una tabla, use **sp_rename**. Para obtener un informe en las vistas y procedimientos almacenados que dependen de una tabla, utilice [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) y [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
## <a name="nullability-rules-within-a-table-definition"></a>Reglas de nulabilidad en una definición de tabla  
 La nulabilidad de una columna determina si esa columna puede permitir un valor nulo (NULL) para sus datos. NULL no es lo mismo que cero o en blanco: NULL significa que no se ha especificado ninguna entrada o que se ha proporcionado un valor NULL explícito, y suele implicar que se desconoce el valor o que no es aplicable.  
  
 Cuando cree o modifique una tabla con las instrucciones CREATE TABLE o ALTER TABLE, la configuración de la sesión y de la base de datos influirá en la nulabilidad para el tipo de datos utilizado en la definición de columna y, posiblemente, la invalidará. Se recomienda que defina siempre explícitamente una columna como NULL o NOT NULL en el caso de columnas no calculadas o, si utiliza un tipo de datos definido por el usuario, que permita que la columna utilice la nulabilidad predeterminada del tipo de datos. Las columnas dispersas siempre deben permitir valores NULL.  
  
 Si la nulabilidad de la columna no se especifica explícitamente, seguirá las reglas que se muestran en la tabla siguiente.  
  
|Tipo de datos de columna|Regla|  
|----------------------|----------|  
|Tipo de datos de alias|[!INCLUDE[ssDE](../../includes/ssde-md.md)] utiliza la nulabilidad especificada al crear el tipo de datos. Para determinar la nulabilidad predeterminada del tipo de datos, utilice **sp_help**.|  
|tipo definido por el usuario CLR|La nulabilidad se determina de acuerdo con la definición de columna.|  
|Tipo de datos suministrado por el sistema|Si el tipo de datos suministrado por el sistema solo tiene una opción, esta tiene prioridad. **marca de tiempo** datos tipos deben ser NOT NULL. Si la configuración de sesión se establece en ON con SET:<br />**ANSI_NULL_DFLT_ON** = ON, se asigna NULL.  <br />**ANSI_NULL_DFLT_OFF** = ON, no se asigna NULL.<br /><br /> Si la base de datos se configura con ALTER DATABASE:<br />**Si ANSI_NULL_DEFAULT_ON** = ON, se asigna NULL.  <br />**Si ANSI_NULL_DEFAULT_OFF** = ON, no se asigna NULL.<br /><br /> Para ver la configuración de base de datos para ANSI_NULL_DEFAULT, utilice la **sys.databases** vista de catálogo|  
  
 Cuando ninguna de las opciones ANSI_NULL_DFLT está establecida para la sesión y la base de datos tiene la configuración predeterminada (ANSI_NULL_DEFAULT es OFF), se asigna el valor predeterminado NOT NULL.  
  
 En el caso de una columna calculada, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] determinará automáticamente su nulabilidad. Para averiguar la nulabilidad de este tipo de columna, utilice la función COLUMNPROPERTY con la **AllowsNull** propiedad.  
  
> [!NOTE]  
>  El controlador ODBC de SQL Server y el proveedor Microsoft OLE DB para SQL Server tienen un valor predeterminado de ANSI_NULL_DFLT_ON establecido en ON. Los usuarios de ODBC y OLE DB pueden configurar esto en los orígenes de datos ODBC o con las propiedades o atributos de la conexión establecidos por la aplicación.  
  
## <a name="data-compression"></a>Data Compression  
 En las tablas del sistema no se puede habilitar la compresión. Cuando se crea una tabla, la compresión de datos se establece en NONE, a menos que se especifique otra cosa. Si se especifica una lista de particiones o una partición que están fuera del intervalo, se generará un error. Para obtener más información sobre la compresión de datos, vea [Compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
 Para evaluar cómo afecta el cambio del estado de compresión a una tabla, índice o partición, use el procedimiento almacenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) .  
  
## <a name="permissions"></a>Permissions  
 Se necesita el permiso CREATE TABLE en la base de datos y el permiso ALTER en el esquema en que se crea la tabla.  
  
 Si las columnas de la instrucción CREATE TABLE se definen como un tipo definido por el usuario CLR, se necesita la propiedad del tipo o el permiso REFERENCES.  
  
 Si las columnas de la instrucción CREATE TABLE tienen asociada una colección de esquemas XML, se necesita la propiedad de la colección de esquemas XML o el permiso REFERENCES.  
  
 Cualquier usuario puede crear tablas temporales en tempdb.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-a-primary-key-constraint-on-a-column"></a>A. Crear una restricción PRIMARY KEY en una columna  
 En el ejemplo siguiente se muestra la definición de columna para una restricción PRIMARY KEY con un índice clúster en la columna `EmployeeID` de la tabla `Employee`. Como no se especifica un nombre de restricción, el sistema proporciona el nombre de la restricción.  
  
```  
CREATE TABLE dbo.Employee (EmployeeID int  
PRIMARY KEY CLUSTERED);  
```  
  
### <a name="b-using-foreign-key-constraints"></a>B. Usar restricciones FOREIGN KEY  
 Una restricción FOREIGN KEY se utiliza para hacer referencia a otra tabla. Las claves externas pueden ser claves de una sola columna o de varias columnas. En el siguiente ejemplo se muestra una restricción FOREIGN KEY de una única columna en la tabla `SalesOrderHeader` que hace referencia a la tabla `SalesPerson`. Solo se requiere la cláusula REFERENCES para una restricción FOREIGN KEY de una única columna.  
  
```  
SalesPersonID int NULL  
REFERENCES SalesPerson(SalesPersonID)  
```  
  
 También puede utilizar la cláusula FOREIGN KEY de forma explícita y volver a formular el atributo de columna. Observe que no es necesario que el nombre de la columna sea el mismo en ambas tablas.  
  
```  
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)  
```  
  
 Las restricciones de claves de varias columnas se crean como restricciones de tabla. En la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], la tabla `SpecialOfferProduct` incluye una restricción PRIMARY KEY de varias columnas. En el siguiente ejemplo se muestra cómo hacer referencia a esta clave desde otra tabla; el nombre explícito de restricción es opcional.  
  
```  
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail FOREIGN KEY  
 (ProductID, SpecialOfferID)  
REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)  
```  
  
### <a name="c-using-unique-constraints"></a>C. Usar restricciones UNIQUE  
 Las restricciones UNIQUE se utilizan para exigir la unicidad en las columnas de clave no principal. En el siguiente ejemplo se exige la restricción de que la columna `Name` de la tabla `Product` debe ser única.  
  
```  
Name nvarchar(100) NOT NULL  
UNIQUE NONCLUSTERED  
```  
  
### <a name="d-using-default-definitions"></a>D. Usar definiciones DEFAULT  
 Los valores predeterminados suministran un valor (con las instrucciones INSERT y UPDATE) cuando no se especifica ninguno. Por ejemplo, la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] puede incluir una tabla de búsqueda con los distintos trabajos que los empleados pueden realizar en la compañía. En la columna que describe cada trabajo, el valor predeterminado de cadena de caracteres puede suministrar una descripción si no se ha escrito una descripción de forma explícita.  
  
```  
DEFAULT 'New Position - title not formalized yet'  
```  
  
 Además de constantes, las definiciones de DEFAULT pueden incluir funciones. Utilice el siguiente ejemplo para obtener la fecha actual de una entrada.  
  
```  
DEFAULT (getdate())  
```  
  
 Un recorrido de las funciones niládicas puede mejorar también la integridad de los datos. Para realizar un seguimiento del usuario que ha insertado una fila, utilice la función niládica para USER. No escriba las funciones niládicas entre paréntesis.  
  
```  
DEFAULT USER  
```  
  
### <a name="e-using-check-constraints"></a>E. Usar restricciones CHECK  
 En el siguiente ejemplo se muestra una restricción para los valores escritos en la columna `CreditRating` de la tabla `Vendor`. La restricción no tiene nombre.  
  
```  
CHECK (CreditRating >= 1 and CreditRating <= 5)  
```  
  
 En este ejemplo se muestra una restricción con nombre con una restricción de patrón en los datos de caracteres escritos en la columna de la tabla.  
  
```  
CONSTRAINT CK_emp_id CHECK (emp_id LIKE   
'[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'   
OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]')  
```  
  
 En este ejemplo se especifica que los valores se deben incluir en una lista específica o seguir un patrón dado.  
  
```  
CHECK (emp_id IN ('1389', '0736', '0877', '1622', '1756')  
OR emp_id LIKE '99[0-9][0-9]')  
```  
  
### <a name="f-showing-the-complete-table-definition"></a>F. Mostrar la definición de tabla completa  
 En el siguiente ejemplo se muestran las definiciones de tablas completas con todas las definiciones de restricciones para la tabla `PurchaseOrderDetail` creada en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Tenga en cuenta que, para ejecutar el ejemplo, el esquema de tabla se cambia a `dbo`.  
  
```  
CREATE TABLE dbo.PurchaseOrderDetail  
(  
    PurchaseOrderID int NOT NULL  
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),  
    LineNumber smallint NOT NULL,  
    ProductID int NULL   
        REFERENCES Production.Product(ProductID),  
    UnitPrice money NULL,  
    OrderQty smallint NULL,  
    ReceivedQty float NULL,  
    RejectedQty float NULL,  
    DueDate datetime NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL  
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (newid()),  
    ModifiedDate datetime NOT NULL   
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (getdate()),  
    LineTotal  AS ((UnitPrice*OrderQty)),  
    StockedQty  AS ((ReceivedQty-RejectedQty)),  
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber  
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)  
               WITH (IGNORE_DUP_KEY = OFF)  
)   
ON PRIMARY;  
```  
  
### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>G. Crear una tabla con una columna xml con tipo en una colección de esquemas XML  
 En el siguiente ejemplo se crea una tabla con una columna `xml` con tipo de la colección de esquemas XML `HRResumeSchemaCollection`. El `DOCUMENT` palabra clave especifica que cada instancia de la `xml` tipo de datos en *column_name* puede contener un único elemento de nivel superior.  
  
```  
CREATE TABLE HumanResources.EmployeeResumes   
   (LName nvarchar(25), FName nvarchar(25),   
    Resume xml( DOCUMENT HumanResources.HRResumeSchemaCollection) );  
```  
  
### <a name="h-creating-a-partitioned-table"></a>H. Crear una tabla con particiones  
 En el ejemplo siguiente se crea una función de partición para crear cuatro particiones en una tabla o en un índice. A continuación, se crea un esquema de partición en el que se especifican los grupos de archivos que van a contener cada una de las cuatro particiones. Finalmente, en el ejemplo se crea una tabla que utiliza el esquema de partición. En este ejemplo se asume que los grupos de archivos ya existen en la base de datos.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
GO  
  
CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg) ;  
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
    ON myRangePS1 (col1) ;  
GO  
```  
  
 En función de los valores de la columna `col1` de `PartitionTable`, las particiones se asignan de las maneras siguientes.  
  
|Grupo de archivos|test1fg|test2fg|test3fg|test4fg|  
|---------------|-------------|-------------|-------------|-------------|  
|**Partición**|1|2|3|4|  
|**Valores**|Col 1 \<= 1|col1 > 1 AND col1 \<= 100|col1 > 100 AND col1 \<= 1000|col1 > 1000|  
  
### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>I. Usar el tipo de datos uniqueidentifier en una columna  
 En el siguiente ejemplo se crea una tabla con una columna `uniqueidentifier`. En el ejemplo se utiliza una restricción PRIMARY KEY para impedir que los usuarios inserten valores duplicados, y se utiliza la función `NEWSEQUENTIALID()` de la restricción `DEFAULT` para proporcionar valores a las nuevas filas. Se aplica la propiedad ROWGUIDCOL a la columna `uniqueidentifier` de modo que se pueda hacer referencia a la misma mediante la palabra clave $ROWGUID.  
  
```  
CREATE TABLE dbo.Globally_Unique_Data  
    (guid uniqueidentifier   
        CONSTRAINT Guid_Default DEFAULT   
        NEWSEQUENTIALID() ROWGUIDCOL,  
    Employee_Name varchar(60)  
    CONSTRAINT Guid_PK PRIMARY KEY (guid) );  
```  
  
### <a name="j-using-an-expression-for-a-computed-column"></a>J. Usar una expresión para una columna calculada  
 En el siguiente ejemplo se muestra el uso de una expresión (`(low + high)/2`) para calcular la columna calculada `myavg`.  
  
```  
CREATE TABLE dbo.mytable   
    ( low int, high int, myavg AS (low + high)/2 ) ;  
```  
  
### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>K. Crear una columna calculada en función de una columna de tipo definido por el usuario  
 En el siguiente ejemplo se crea una tabla con una columna de tipo definido por el usuario `utf8string` dando por supuesto que el ensamblado del tipo y el propio tipo ya se han creado en la base de datos actual. Una segunda columna se define basándose en `utf8string`y utiliza el método `ToString()` de **type(class)** `utf8string` para calcular un valor para la columna.  
  
```  
CREATE TABLE UDTypeTable   
    ( u utf8string, ustr AS u.ToString() PERSISTED ) ;  
```  
  
### <a name="l-using-the-username-function-for-a-computed-column"></a>L. Usar la función USER_NAME para una columna calculada  
 En el siguiente ejemplo se utiliza la función `USER_NAME()` en la columna `myuser_name`.  
  
```  
CREATE TABLE dbo.mylogintable  
    ( date_in datetime, user_id int, myuser_name AS USER_NAME() ) ;  
```  
  
### <a name="m-creating-a-table-that-has-a-filestream-column"></a>M. Crear una tabla que tenga una columna FILESTREAM  
 En el ejemplo siguiente se crea una tabla que tiene una columna `FILESTREAM` `Photo`. Si una tabla tiene una o varias columnas `FILESTREAM`, la tabla debe tener una columna `ROWGUIDCOL`.  
  
```  
CREATE TABLE dbo.EmployeePhoto  
    (  
    EmployeeId int NOT NULL PRIMARY KEY,  
    ,Photo varbinary(max) FILESTREAM NULL  
    ,MyRowGuidColumn uniqueidentifier NOT NULL ROWGUIDCOL  
        UNIQUE DEFAULT NEWID()  
    );  
```  
  
### <a name="n-creating-a-table-that-uses-row-compression"></a>N. Crear una tabla que use compresión de fila  
 En el ejemplo siguiente se crea una tabla que usa la compresión de fila.  
  
```  
CREATE TABLE dbo.T1   
(c1 int, c2 nvarchar(200) )  
WITH (DATA_COMPRESSION = ROW);  
```  
  
 Para obtener ejemplos de compresión de datos adicionales, consulte [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>O. Crear una tabla que tenga columnas dispersas y un conjunto de columnas  
 En los ejemplos siguientes se muestra cómo crear una tabla que tenga una columna dispersa y una tabla que tenga dos columnas dispersas y un conjunto de columnas. En los ejemplos se utiliza la sintaxis básica. Para obtener ejemplos más complejos, vea [usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md) y [usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md).  
  
 En este ejemplo se crea una tabla que tiene una columna dispersa.  
  
```  
CREATE TABLE dbo.T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL ) ;  
```  
  
 En este ejemplo se crea una tabla que tiene dos columnas dispersas y un conjunto de columnas denominado `CSet`.  
  
```  
CREATE TABLE T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL,  
    c3 int SPARSE NULL,  
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ) ;  
```  
  
### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>P. Crear una tabla temporal con versión del sistema basadas en disco  
   
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Los ejemplos siguientes muestran cómo crear una tabla temporal vinculada a una nueva tabla de historial y cómo crear una tabla temporal vinculada a una tabla de historial existente. Tenga en cuenta que la tabla temporal debe tener una clave principal definida para estar habilitado para que la tabla esté habilitado para control de versiones del sistema. Para obtener ejemplos que muestran cómo agregar o quitar las versiones de sistema en una tabla existente, vea control de versiones de sistema en [ejemplos](../../t-sql/statements/alter-table-transact-sql.md#Example_Top). Para casos de uso, consulte [tablas temporales](../../relational-databases/tables/temporal-tables.md).  
  
 Este ejemplo crea una nueva tabla temporal vinculada a una nueva tabla de historial.  
  
```  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH (SYSTEM_VERSIONING = ON);  
```  
  
 Este ejemplo crea una nueva tabla temporal vinculada a una tabla de historial existente.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>Q. Crear una tabla temporal con versión del sistema con optimización para memoria  
   
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 En el ejemplo siguiente se muestra cómo crear una versión del sistema con optimización para memoria tabla temporal vinculada a una nueva tabla de historial basada en disco.  
  
 Este ejemplo crea una nueva tabla temporal vinculada a una nueva tabla de historial.  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 Este ejemplo crea una nueva tabla temporal vinculada a una tabla de historial existente.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="r-creating-a-table-with-encrypted-columns"></a>R. Creación de una tabla con columnas cifradas  
 En el ejemplo siguiente se crea una tabla con dos columnas cifradas. Para obtener más información, vea [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
```  
CREATE TABLE Customers (  
    CustName nvarchar(60)   
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = RANDOMIZED,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    SSN varchar(11) COLLATE  Latin1_General_BIN2  
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = DETERMINISTIC ,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    Age int NULL  
);  
```

### <a name="s-create-an-inline-filtered-index"></a>S. Crear un índice filtrado en línea 
Crea una tabla con un índice filtrado en línea.
  
  ```
  CREATE TABLE t1 
 (
      c1 int,
      index IX1  (c1) WHERE c1 > 0   
 )
GO
 ```
 
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [Eliminar tabla &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helpconstraint &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  



