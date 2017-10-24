---
title: ALTER FUNCTION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3da4c3a8e76a48db0eee940e969ddf24dc147149
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Modifica una función [!INCLUDE[tsql](../../includes/tsql-md.md)] o CLR existente, creada anteriormente por medio de la ejecución de la instrucción CREATE FUNCTION, sin cambiar los permisos y sin que afecte a ninguna otra función, procedimiento almacenado o desencadenador dependiente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]
```  

```
-- Transact-SQL Inline Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
```
  
```
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
```

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
} 

<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  

<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```
  
```
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
<method_specifier>::=  
    assembly_name.class_name.method_name  
 
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 Nombre del esquema al que pertenece la función definida por el usuario.  
  
 *nombre_función*  
 Es la función definida por el usuario que se va a cambiar.  
  
> [!NOTE]  
>  Los paréntesis después del nombre de la función son necesarios, aunque no se especifique un parámetro.  
  
 **@***parameter_name*  
 Es un parámetro de la función definida por el usuario. Es posible declarar uno o varios parámetros.  
  
 Una función puede tener un máximo de 2.100 parámetros. El usuario debe proporcionar el valor de cada parámetro declarado cuando se ejecuta la función, a menos que se defina un valor predeterminado para el parámetro.  
  
 Especifique un nombre de parámetro con un signo de arroba (**@**) como primer carácter. El nombre del parámetro debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Los parámetros son locales para la función; los mismos nombres de parámetro se pueden utilizar en otras funciones. Los parámetros solamente pueden ocupar el lugar de constantes; no se pueden utilizar en lugar de nombres de tablas, nombres de columnas o nombres de otros objetos de base de datos.  
  
> [!NOTE]  
>  No se respeta ANSI_WARNINGS al pasar parámetros de un procedimiento almacenado, una función definida por el usuario o al declarar y establecer variables en una instrucción de lote. Por ejemplo, si una variable se define como **char (3)**y, a continuación, establece en un valor mayor que tres caracteres, se truncan los datos para el tamaño definido y la INSERCIÓN o instrucción de actualización se realiza correctamente.  
  
 [ *type_schema_name.* ] *parameter_data_type*  
 Es el tipo de datos del parámetro y, de forma opcional, el esquema al que pertenece. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] se permiten funciones, todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto el **timestamp** tipo de datos. Para las funciones CLR, se permiten todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto **texto**, **ntext**, **imagen**, y **marca de tiempo** tipos de datos. Los tipos de datos no escalares **cursor** y **tabla** no se puede especificar como un tipo de datos de parámetro en la vista [!INCLUDE[tsql](../../includes/tsql-md.md)] o las funciones CLR.  
  
 Si *type_schema_name* no se especifica, el [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] busca el *parameter_data_type* en el siguiente orden:  
  
-   El esquema que contiene los nombres de los tipos de datos del sistema de SQL Server.  
  
-   El esquema predeterminado del usuario actual en la base de datos actual.  
  
-   El esquema **dbo** de la base de datos actual.  
  
 [  **=**  *predeterminado* ]  
 Es un valor predeterminado para el parámetro. Si un *predeterminado* se define un valor, la función se puede ejecutar sin especificar un valor para ese parámetro.  
  
> [!NOTE]  
>  Se pueden especificar valores de parámetros predeterminados para las funciones CLR excepto **varchar (max)** y **varbinary (max)** tipos de datos.  
  
 Cuando un parámetro de la función tiene un valor predeterminado, se debe especificar la palabra clave DEFAULT al llamar a la función para recuperar el valor predeterminado. Este comportamiento es distinto del uso de parámetros con valores predeterminados en los procedimientos almacenados, donde la omisión del parámetro implica especificar el valor predeterminado.  
  
 *return_data_type*  
 Es el valor devuelto de una función escalar definida por el usuario. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] se permiten funciones, todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto el **timestamp** tipo de datos. Para las funciones CLR, se permiten todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto **texto**, **ntext**, **imagen**, y **marca de tiempo** tipos de datos. Los tipos de datos no escalares **cursor** y **tabla** no se puede especificar como un tipo de datos de retorno en la vista [!INCLUDE[tsql](../../includes/tsql-md.md)] o las funciones CLR.  
  
 *function_body*  
 Especifica que una serie de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], que juntas no producen ningún efecto secundario (como modificar una tabla), definen el valor de la función. *function_body* solo se usa en funciones escalares y funciones con valores de tabla de múltiples instrucciones.  
  
 En las funciones escalares, *cuerpo_función* es una serie de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones que juntas se evalúan como un valor escalar.  
  
 En funciones con valores de tabla de múltiples instrucciones, *cuerpo_función* es una serie de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones que rellenan una tabla devuelven variable.  
  
 *scalar_expression*  
 Especifica que la función escalar devuelve un valor escalar.  
  
 TABLE  
 Especifica que el valor devuelto de la función con valores de tabla es una tabla. Sólo las constantes y  **@**  *local_variables* puede pasarse a funciones con valores de tabla.  
  
 En las funciones insertadas con valores de tabla, el valor devuelto de TABLE se define mediante una única instrucción SELECT. Las funciones insertadas no tienen variables devueltas asociadas.  
  
 En funciones con valores de tabla de múltiples instrucciones,  **@**  *return_variable* es una variable de tabla utilizada para almacenar y acumular las filas que se deben devolver como el valor de la función. **@***return_variable* se puede especificar sólo para [!INCLUDE[tsql](../../includes/tsql-md.md)] las funciones y no para funciones CLR.  
  
 *Seleccione stmt*  
 Es la instrucción SELECT individual que define el valor devuelto de una función insertada con valores de tabla.  
  
 NOMBRE externo \<method_specifier >*assembly_name.class_name*. *NombreMétodo*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el método de un ensamblado que se enlaza a la función. *ASSEMBLY_NAME* debe coincidir con un ensamblado existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos actual con la visibilidad activada. *CLASS_NAME* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador y debe existir como una clase en el ensamblado. Si la clase tiene un nombre calificado de espacio de nombres que utiliza un período (**.**) para separar las partes del espacio de nombres, el nombre de clase debe estar delimitado mediante corchetes (**[]**) o comillas (**""**). *NombreMétodo* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador y debe existir como un método estático en la clase especificada.  
  
> [!NOTE]  
>  De manera predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede ejecutar código CLR. Puede crear, modificar y quitar objetos de base de datos que hagan referencia a common language runtime módulos; Sin embargo, no se puede ejecutar estas referencias en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta que habilite la [opción clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar la opción, utilice [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 *\<*table_type_definition*>***(** { \<definición_de_columna > \<column_constraint > | \<definición_de_columna_calculada >} [ \<table_constraint >] [ **,**... *n* ]**)**  
 Define el tipo de datos de tabla para una función [!INCLUDE[tsql](../../includes/tsql-md.md)]. La declaración de tabla incluye definiciones de columna y restricciones de columna o de tabla.  
  
\<definición_de_tipo_de_tabla_clr > **(** { *column_name**data_type* } [ **,**...  *n*  ] **)** **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([vista previa en algunas regiones](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  
 Define los tipos de datos de tabla para una función CLR. La declaración de tabla solamente incluye nombres de columna y tipos de datos.  
  
 NULL | NO ES NULL  
 Admite solo para los compilados de forma nativa, escalares funciones definidas por el usuario. Para obtener más información, consulte [Scalar User-Defined funciones para OLTP en memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Indica si una función definida por el usuario se compila de forma nativa. Este argumento es necesario para las funciones definidas por el usuario compiladas de forma nativa, escalares.  
  
 El argumento NATIVE_COMPILATION es necesario al modificar la función y solo pueden usarse, si se ha creado la función con el argumento NATIVE_COMPILATION.  
  
 BEGIN ATOMIC CON  
 Admite solo de forma nativa, las funciones escalares definidas por el usuario y es necesario. Para obtener más información, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 El argumento SCHEMABINDING se requiere para las funciones definidas por el usuario compiladas de forma nativa, escalares.  
  
 **\<function_option >:: = y \<clr_function_option >:: =**  
  
 Especifica si la función tendrá una o más de las siguientes opciones.  
  
 ENCRYPTION  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica que [!INCLUDE[ssDE](../../includes/ssde-md.md)] cifra las columnas de vista de catálogo que contienen el texto de la instrucción ALTER FUNCTION. El uso de ENCRYPTION impide que la función se publique como parte de la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. ENCRYPTION no se puede especificar para funciones CLR.  
  
 SCHEMABINDING  
 Especifica que la función está enlazada a los objetos de base de datos a los que hace referencia. Esta condición impide que se realicen cambios en la función si otros objetos enlazados del esquema hacen referencia a ella.  
  
 El enlace de la función a los objetos a los que hace referencia solamente se quita cuando se ejecuta una de estas acciones:  
  
-   Se quita la función.  
  
-   La función se modifica con la instrucción ALTER sin especificar la opción SCHEMABINDING.  
  
Para obtener una lista de condiciones que deben cumplirse para que una función puede estar enlazada a un esquema, vea [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 Especifica la **OnNULLCall** atributo de una función con valores escalares. Si no se especifica, se utiliza CALLED ON NULL INPUT de manera predeterminada. Esto significa que el cuerpo de la función se ejecuta aunque se envíe NULL como argumento.  
  
 Si se especifica RETURNS NULL ON NULL INPUT en una función CLR, esto indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver NULL cuando cualquiera de los argumentos que recibe sea NULL, sin invocar realmente el cuerpo de la función. Si el método especificado en \<method_specifier > ya tiene un atributo personalizado que indica RETURNS NULL ON NULL INPUT, pero la instrucción ALTER FUNCTION indica CALLED ON NULL INPUT, la instrucción ALTER FUNCTION tiene prioridad. El **OnNULLCall** atributo no se puede especificar para las funciones con valores de tabla CLR.  
  
 Cláusula EXECUTE AS  
 Especifica el contexto de seguridad en el que se ejecuta la función definida por el usuario. Por lo tanto, es posible controlar la cuenta de usuario que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para validar los permisos en los objetos de base de datos a los que hace referencia la función.  
  
> [!NOTE]  
>  EXECUTE AS no se puede especificar para las funciones insertadas definidas por el usuario.  
  
 Para obtener más información, vea [EXECUTE AS &#40;cláusula de Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
**\<definición_de_columna >:: =**
  
 Define el tipo de datos de tabla. La declaración de tabla incluye definiciones de columna y restricciones. Para las funciones CLR, sólo *column_name* y *data_type* puede especificarse.  
  
 *column_name*  
 Es el nombre de una columna de la tabla. Los nombres de columna se deben ajustar a las reglas para los identificadores y deben ser únicos en la tabla. *column_name* puede tener de 1 a 128 caracteres.  
  
 *data_type*  
 Especifica el tipo de datos de la columna. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] se permiten funciones, todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto **marca de tiempo**. Para las funciones CLR, se permiten todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto **texto**, **ntext**, **imagen**, **char**, **varchar**, **varchar (max)**, y **marca de tiempo**. El tipo de datos no escalar **cursor** no se puede especificar como un tipo de datos de columna en la vista [!INCLUDE[tsql](../../includes/tsql-md.md)] o las funciones CLR.  
  
 PREDETERMINADO *expresiónConstante*  
 Especifica el valor suministrado para la columna cuando no se ha especificado explícitamente un valor durante una inserción. *expresiónConstante* es una constante, NULL o un valor de función de sistema. Se pueden aplicar definiciones con el valor DEFAULT a cualquier columna, excepto las que incluyen la propiedad IDENTITY. No se puede especificar DEFAULT para las funciones CLR con valores de tabla.  
  
 COLLATE *collation_name*  
 Especifica la intercalación de la columna. Si no se especifica, se asigna a la columna la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Para obtener una lista de y obtener más información, vea [nombre de intercalación de Windows &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) y [SQL nombre de intercalación de servidor &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 La cláusula COLLATE se puede utilizar para cambiar las intercalaciones solo de las columnas de la **char**, **varchar**, **nchar**, y **nvarchar** tipos de datos.  
  
 No se puede especificar COLLATE para las funciones con valores de tabla CLR.  
  
 ROWGUIDCOL  
 Indica que la nueva columna es una columna de identificador único global de fila. Solo un **uniqueidentifier** se puede designar la columna por tabla como columna ROWGUIDCOL. La propiedad ROWGUIDCOL se puede asignar solo a un **uniqueidentifier** columna.  
  
 La propiedad ROWGUIDCOL no exige que los valores almacenados en la columna sean únicos. Del mismo modo, tampoco genera automáticamente valores para nuevas filas insertadas en la tabla. Si desea generar valores únicos para cada columna, use la función NEWID en instrucciones INSERT. Puede especificar un valor predeterminado; sin embargo, no puede especificar NEWID como valor predeterminado.  
  
 IDENTITY  
 Indica que la nueva columna es una columna de identidad. Cuando se agrega una nueva fila a la tabla, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un valor incremental único para la columna. Las columnas de identidad se utilizan normalmente junto con las restricciones PRIMARY KEY como identificadores de fila exclusivos de la tabla. La propiedad IDENTITY se puede asignar a **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, o **numeric(p,0)** columnas. Solo se puede crear una columna de identidad para cada tabla. Las restricciones DEFAULT y los valores predeterminados enlazados no se pueden utilizar en las columnas de identidad. Debe especificar tanto el *inicialización* y *incremento* o ninguno. Si no se especifica ninguno, el valor predeterminado es (1,1).  
  
 No se puede especificar IDENTITY para las funciones CLR con valores de tabla.  
  
 *valor de inicialización*  
 Se trata del valor entero que se asignará a la primera fila de la tabla.  
  
 *incremento*  
 Es el valor entero para agregar a la *inicialización* valor para las filas sucesivas de la tabla.  
  
**\<column_constraint >:: = y \< table_constraint >:: =**
  
 Define la restricción para la columna o tabla especificada. Para las funciones CLR, el único tipo de restricción permitido es NULL. No se permiten las restricciones con nombre.  
  
 NULL | NOT NULL  
 Determina si se permiten valores NULL en la columna. NULL no es estrictamente una restricción, pero se puede especificar, al igual que NOT NULL. No se puede especificar NOT NULL para las funciones CLR con valores de tabla.  
  
 PRIMARY KEY  
 Es una restricción que exige la integridad de entidad para la columna especificada a través de un índice único. En las funciones con valores de tabla definidas por el usuario, la restricción PRIMARY KEY solamente se puede crear en una columna de cada tabla. No se puede especificar PRIMARY KEY para las funciones CLR con valores de tabla.  
  
 UNIQUE  
 Es una restricción que proporciona la integridad de entidad para una o varias columnas especificadas a través de un índice único. Las tablas pueden tener varias restricciones UNIQUE. No se puede especificar UNIQUE para las funciones CLR con valores de tabla.  
  
 CLUSTERED | NONCLUSTERED  
 Indica que se ha creado un índice clúster o no clúster para la restricción PRIMARY KEY o UNIQUE. Las restricciones PRIMARY KEY utilizan CLUSTERED y las restricciones UNIQUE, NONCLUSTERED.  
  
 CLUSTERED solamente se puede especificar para una restricción. Si se especifica CLUSTERED para una restricción UNIQUE y también se especifica una restricción PRIMARY KEY, esta última utilizará NONCLUSTERED.  
  
 No se pueden especificar CLUSTERED y NONCLUSTERED para las funciones CLR con valores de tabla.  
  
 CHECK  
 Es una restricción que exige la integridad del dominio al limitar los valores posibles que se pueden escribir en una o varias columnas. No se pueden especificar restricciones CHECK para las funciones CLR con valores de tabla.  
  
 *Filter*  
 Es una expresión lógica que devuelve TRUE o FALSE.  
  
 **\<definición_de_columna_calculada >:: =**  
  
 Especifica una columna calculada. Para obtener más información sobre las columnas calculadas, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 *column_name*  
 Es el nombre de la columna calculada.  
  
 *computed_column_expression*  
 Es una expresión que define el valor de una columna calculada.  
  
 **\<index_option >:: =**  
  
 Especifica las opciones de índice para el índice PRIMARY KEY o UNIQUE. Para obtener más información acerca de las opciones de índice, vea [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = { ON | OFF }  
 Especifica el relleno del índice. El valor predeterminado es OFF.  
  
 Valor de FILLFACTOR = *fillfactor*  
 Especifica un porcentaje que indica cómo el [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe realizar el nivel de hoja de cada página de índice durante la creación de índices o cambiar. *valor de FILLFACTOR* debe ser un valor entero entre 1 y 100. El valor predeterminado es 0.  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 Especifica la respuesta de error cuando una operación de inserción intenta insertar valores de clave duplicados en un índice único. La opción IGNORE_DUP_KEY se aplica solamente a operaciones de inserción realizadas tras crear o volver a generar el índice. El valor predeterminado es OFF.  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 Especifica si se vuelven a calcular las estadísticas de distribución. El valor predeterminado es OFF.  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 Especifica si se permiten los bloqueos de fila. El valor predeterminado es ON.  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 Especifica si se permiten bloqueos de página. El valor predeterminado es ON.  
  
## <a name="remarks"></a>Comentarios  
 No es posible utilizar ALTER FUNCTION para cambiar una función escalar por una función con valores de tabla, ni viceversa. Tampoco es posible utilizar ALTER FUNCTION para cambiar una función insertada por una función de múltiples instrucciones o viceversa. No se puede utilizar ALTER FUNCTION para cambiar una función [!INCLUDE[tsql](../../includes/tsql-md.md)] por una función CLR o viceversa.  
  
 Las siguientes instrucciones de Service Broker no puede incluirse en la definición de un [!INCLUDE[tsql](../../includes/tsql-md.md)] función definida por el usuario:  
  
-   EMPEZAR CONVERSACIÓN DE DIÁLOGO  
-   FINALIZAR CONVERSACIÓN  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   ENVIAR  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER para la función o para el esquema. Si la función especifica un tipo definido por el usuario, requiere el permiso EXECUTE para ese tipo.  
  
## <a name="see-also"></a>Vea también  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [DROP FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

