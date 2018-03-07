---
title: Crear tipo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 145f60bcec81e8a29761a44146df025f66a21b80
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-type-transact-sql"></a>CREATE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea un tipo de datos de alias o un tipo definido por el usuario en la base de datos actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La implementación de un tipo de datos de alias se basa en un tipo nativo del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un tipo definido por el usuario se implementa a través de una clase de un ensamblado en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR). Para enlazar un tipo definido por el usuario para su implementación, el ensamblado CLR que contiene la implementación del tipo en primer lugar debe estar registrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md).  
  
 De manera predeterminada, la posibilidad de ejecutar código de CLR está desactivada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede crear, modificar y quitar objetos de base de datos que hagan referencia a módulos de código administrado, pero estas referencias no se ejecutarán en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que la [clr enabled (opción)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) se habilita mediante [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
 
> [!NOTE]  
>  La integración de CLR de .NET Framework en SQL Server se describe en este tema. Integración de CLR no se aplica a Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Disk-Based Type Syntax  
CREATE TYPE [ schema_name. ] type_name  
{   
    FROM base_type   
    [ ( precision [ , scale ] ) ]  
    [ NULL | NOT NULL ]   
  | EXTERNAL NAME assembly_name [ .class_name ]   
  | AS TABLE ( { <column_definition> | <computed_column_definition> }  
        [ <table_constraint> ] [ ,...n ] )    
} [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   
    [ NULL | NOT NULL ]  
    [   
        DEFAULT constant_expression ]   
      | [ IDENTITY [ ( seed ,increment ) ]   
    ]  
    [ ROWGUIDCOL ] [ <column_constraint> [ ...n ] ]   
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
                [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH ( <index_option> [ ,...n ] )   
        ]  
  | CHECK ( logical_expression )   
}   
  
<computed_column_definition> ::=  
  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH ( <index_option> [ ,...n ] )  
        ]  
    | CHECK ( logical_expression )   
]   
  
<table_constraint> ::=  
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
    ( column [ ASC | DESC ] [ ,...n ] )   
        [   
    WITH ( <index_option> [ ,...n ] )   
        ]  
    | CHECK ( logical_expression )   
}   
  
<index_option> ::=  
{  
    IGNORE_DUP_KEY = { ON | OFF }  
}  
```  
  
```  
-- Memory-Optimized Table Type Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> }  
    |  [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ]    } )
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   [ NULL | NOT NULL ]    [  
      [ IDENTITY [ (1 , 1) ]  
    ]  
    [ <column_constraint> [ ... n ] ]    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
{ PRIMARY KEY {   NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count) 
                | NONCLUSTERED } }  
  
< table_constraint > ::=  
{ PRIMARY KEY { NONCLUSTERED HASH (column [ ,... n ] ) 
                   WITH (BUCKET_COUNT = bucket_count) 
               | NONCLUSTERED  (column [ ASC | DESC ] [ ,... n ] )  } }  
  
<column_index> ::=  
  INDEX index_name  
{ { [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count) 
     | NONCLUSTERED } }  
  
< table_index > ::=  
  INDEX constraint_name  
{ { [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count) 
 |  [NONCLUSTERED]  (column [ ASC | DESC ] [ ,... n ] )} }  
  
<table_option> ::=  
{  
    [MEMORY_OPTIMIZED = {ON | OFF}]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 Es el nombre del esquema al que pertenece el tipo de datos de alias o el tipo definido por el usuario.  
  
 *TYPE_NAME*  
 Es el nombre del tipo de datos de alias o del tipo definido por el usuario. Nombres de tipo deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *base_type*  
 Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporcionado en el que se basa el tipo de datos de alias de tipo de datos. *base_type* es **sysname**, no tiene ningún valor predeterminado y puede ser uno de los siguientes valores:  
  
|||||  
|-|-|-|-|  
|**bigint**|**binario (**  *n*  **)**|**bit**|**Char (**  *n*  **)**|  
|**date**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**nchar (**  *n*  **)**|**ntext**|**numeric**|  
|**nvarchar (**  *n*  &#124; **max)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**time**|  
|**tinyint**|**uniqueidentifier**|**varbinary (**  *n*  &#124; **max)**|**varchar (**  *n*  &#124; **max)**|  
  
 *base_type* también puede ser cualquier sinónimo del tipo de datos que se asigna a uno de estos tipos de datos del sistema.  
  
 *precisión*  
 Para **decimal** o **numérico**, es un entero no negativo que indica el número total máximo de dígitos decimales que se pueden almacenar, tanto a la izquierda y a la derecha del separador decimal. Para obtener más información, vea [decimal y numeric &#40; Transact-SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *escala*  
 Para **decimal** o **numérico**, es un entero no negativo que indica el número máximo de dígitos decimales que se pueden almacenar a la derecha del separador decimal, y debe ser menor o igual que la precisión . Para obtener más información, vea [decimal y numeric &#40; Transact-SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** | NO ES NULL  
 Especifica si el tipo puede contener un valor NULL. Si no se especifica, el valor predeterminado es NULL.  
  
 *ASSEMBLY_NAME*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ensamblado al que hace referencia a la implementación del tipo definido por el usuario en common language runtime. *ASSEMBLY_NAME* debe coincidir con un ensamblado existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos actual.  
  
> [!NOTE]  
>  EXTERNAL_NAME no está disponible en una base de datos independiente.  
  
 **[.** *CLASS_NAME***]**   
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la clase en el ensamblado que implementa el tipo definido por el usuario. *CLASS_NAME* debe ser un identificador válido y debe existir como una clase en el ensamblado con visibilidad de ensamblado. *CLASS_NAME* distingue mayúsculas de minúsculas, independientemente de la intercalación de base de datos y debe coincidir exactamente con el nombre de clase en el ensamblado correspondiente. El nombre de clase puede ser un nombre calificado de espacio de nombres entre corchetes (**[]**) si el lenguaje de programación que se usa para escribir la clase usa el concepto de espacios de nombres, como C#. Si *class_name* no se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se da por supuesto es el mismo que *type_name*.  
  
 \<definición_de_columna >  
 Define las columnas para un tipo de tabla definido por el usuario.  
  
 \<tipo de datos >  
 Define el tipo de datos en una columna para un tipo de tabla definido por el usuario. Para obtener más información acerca de los tipos de datos, vea [tipos de datos &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md). Para obtener más información acerca de las tablas, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<column_constraint >  
 Define las restricciones de columna para un tipo de tabla definido por el usuario. Las restricciones compatibles incluyen PRIMARY KEY, UNIQUE y CHECK. Para obtener más información acerca de las tablas, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<definición_de_columna_calculada >  
 Define una expresión de columna calculada como una columna en un tipo de tabla definido por el usuario. Para obtener más información acerca de las tablas, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<table_constraint >  
 Define una restricción de tabla para un tipo de tabla definido por el usuario. Las restricciones compatibles incluyen PRIMARY KEY, UNIQUE y CHECK.  
  
 \<index_option >  
 Especifica la respuesta de error para valores de clave duplicados en una operación de inserción de varias filas en un índice clúster o no clúster único. Para obtener más información acerca de las opciones de índice, vea [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 Debe especificar los índices de columna y de tabla como parte de la instrucción CREATE TABLE. CREATE INDEX y DROP INDEX no se admiten en las tablas optimizadas para memoria.  
  
 MEMORY_OPTIMIZED  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica si el tipo de tabla está con optimización para memoria. Esta opción está desactivada de forma predeterminada; la tabla (tipo) no es una tabla con optimización para memoria (tipo). Los tipos de tablas optimizadas para memoria son tablas de usuario cuyo esquema se conserva en el disco de forma similar al de otras tablas de usuario.  
  
 BUCKET_COUNT  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica el número de cubos que se deben crear en el índice hash. El valor máximo para BUCKET_COUNT en índices hash es 1 073 741 824. Para obtener más información acerca de números de depósitos, consulte [índices para tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md). *bucket_count* es un argumento requerido.  
  
 HASH  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica que se ha creado un índice HASH. Se admiten índices hash solo en tablas optimizadas en memoria.  
  
## <a name="remarks"></a>Comentarios  
 La clase del ensamblado que se hace referencia en *assembly_name*, junto con sus métodos, debe cumplir todos los requisitos para implementar un tipo definido por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información acerca de estos requisitos, consulte [tipos definidos](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 Existen algunas consideraciones adicionales, entre las que se pueden citar las siguientes:  
  
-   La clase puede tener métodos sobrecargados, pero éstos solo se pueden llamar desde el código administrado, no desde [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Cualquier miembro estático se debe declarar como **const** o **readonly** si *assembly_name* es SAFE o EXTERNAL_ACCESS.  
  
 Dentro de una base de datos solo puede haber un tipo definido por el usuario registrado con cualquier tipo especificado que se haya cargado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde CLR. Si se crea un tipo definido por el usuario a partir de un tipo de CLR para el que ya existe un tipo definido por el usuario en la base de datos, CREATE TYPE genera un error. Esta restricción es necesaria para evitar la ambigüedad durante la resolución de tipos SQL si un tipo CLR se puede asignar a más de un tipo definido por el usuario.  
  
 Si no devuelve un método mutador en el tipo de *void*, no se ejecuta la instrucción CREATE TYPE.  
  
 Para modificar un tipo definido por el usuario, debe volver a crearlo después de haberlo quitado mediante una instrucción DROP TYPE.  
  
 A diferencia de los tipos definidos por el usuario que se crean mediante **sp_addtype**, **público** rol de base de datos no se concede automáticamente el permiso REFERENCES en tipos que se crean mediante CREATE TYPE. Este permiso debe concederse por separado.  
  
 En tipos de tabla definidos por el usuario, estructurados de tipos definidos por el usuario que se utilizan en *column_name* \<tipo de datos > forman parte del ámbito de esquema de base de datos en el que se define el tipo de tabla. Para tener acceso a los tipos definidos por el usuario estructurados en un ámbito diferente dentro de la base de datos, utilice nombres de dos partes.  
  
 En los tipos de tabla definidos por el usuario, la clave principal en las columnas calculadas debe ser PERSISTED y NOT NULL.  
  
## <a name="memory-optimized-table-types"></a>Tipos de tablas con optimización para memoria  
 A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], el proceso de los datos de un tipo de tabla se puede realizar en la memoria principal y no en el disco. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Para obtener ejemplos de código que muestra cómo crear tipos de tabla optimizada en memoria, vea [crear una tabla con optimización para memoria y un procedimiento con almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CREATE TYPE en la base de datos actual y el permiso ALTER en *schema_name*. Si no se especifica *schema_name* , se aplican las reglas de resolución de nombres predeterminadas para determinar el esquema del usuario actual. Si *assembly_name* se especifica, un usuario debe poseer el ensamblado o tener el permiso REFERENCES en él.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. Crear un tipo de alias basado en el tipo de datos varchar  
 En el ejemplo siguiente se crea un tipo de alias basado en el tipo de datos `varchar` suministrado por el sistema.  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. Crear un tipo definido por el usuario  
 En el ejemplo siguiente se crea un tipo `Utf8String` que hace referencia a clase `utf8string` en el ensamblado `utf8string`. Antes de crear el tipo, se registra el ensamblado `utf8string` en la base de datos local. Reemplace la parte binaria de la instrucción CREATE ASSEMBLY con una descripción válida.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>C. Crear un tipo de tabla definido por el usuario  
 En el siguiente ejemplo se crea un tipo de tabla definido por el usuario con dos columnas. Para obtener más información acerca de cómo crear y usar parámetros con valores de tabla, vea [usar parámetros &#40; motor de base de datos &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREAR ENSAMBLADOS &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [TIPO de COLOCACIÓN &#40; Transact-SQL &#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
