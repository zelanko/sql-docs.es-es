---
title: "CREATE (función) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
caps.latest.revision: 162
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: c74e3a3322dcc2268fa8e386fda5d55f59be98c5
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una función definida por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Una función definida por el usuario es una rutina de [!INCLUDE[tsql](../../includes/tsql-md.md)] o Common Language Runtime (CLR) que acepta parámetros, realiza una acción, como un cálculo complejo, y devuelve el resultado de esa acción como un valor. El valor devuelto puede ser un valor escalar (único) o una tabla. Utilice esta instrucción para crear una rutina reutilizable que se pueda utilizar de estas formas:  
  
-   En instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] como SELECT  
  
-   En las aplicaciones que llaman a la función  
  
-   En la definición de otra función definida por el usuario  
  
-   Para parametrizar una vista o mejorar la funcionalidad de una vista indizada  
  
-   Para definir una columna en una tabla  
  
-   Para definir una restricción CHECK en una columna  
  
-   Para reemplazar un procedimiento almacenado  
  
-   Usar una función insertada como un predicado de filtro para una directiva de seguridad  
  
> [!NOTE]  
>  La integración de CLR de .NET Framework en SQL Server se describe en este tema. Integración de CLR no se aplica a la base de datos de SQL Azure.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
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
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
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
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>Argumentos
*O ALTER*  
 **Se aplica a**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Condicionalmente, se modifica la función solo si ya existe. 
 
> [!NOTE]  
>  Sintaxis [o ALTER] opcional para CLR está disponible a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU1.   
 
 *schema_name*  
 Nombre del esquema al que pertenece la función definida por el usuario.  
  
 *nombre_función*  
 Nombre de la función definida por el usuario. Los nombres de función deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md) y debe ser único dentro de la base de datos y su esquema.  
  
> [!NOTE]  
>  Los paréntesis después del nombre de la función son necesarios, aunque no se especifique un parámetro.  
  
 @*parameter_name*  
 Es un parámetro de la función definida por el usuario. Es posible declarar uno o varios parámetros.  
  
 Una función puede tener un máximo de 2.100 parámetros. El usuario debe proporcionar el valor de cada parámetro declarado cuando se ejecuta la función, a menos que se defina un valor predeterminado para el parámetro.  
  
 Especifique un nombre de parámetro con una arroba (@) como primer carácter. El nombre del parámetro debe cumplir las mismas reglas que los identificadores. Los parámetros son locales para la función; los mismos nombres de parámetro se pueden utilizar en otras funciones. Los parámetros solamente pueden ocupar el lugar de constantes; no se pueden utilizar en lugar de nombres de tablas, nombres de columnas o nombres de otros objetos de base de datos.  
  
> [!NOTE]  
>  ANSI_WARNINGS no se respeta al pasar parámetros en un procedimiento almacenado o una función definida por el usuario, ni cuando se declaran y se establecen variables en una instrucción por lotes. Por ejemplo, si una variable se define como **char (3)**y, a continuación, establece en un valor mayor que tres caracteres, se truncan los datos para el tamaño definido y la INSERCIÓN o instrucción de actualización se realiza correctamente.  
  
 [ *type_schema_name*. ] *parameter_data_type*  
 Es el tipo de datos del parámetro y, de forma opcional, el esquema al que pertenece. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] se permiten funciones, todos los tipos de datos, incluidos los tipos definidos por el usuario CLR y tipos de tabla definidos por el usuario, excepto el **timestamp** tipo de datos. Para las funciones CLR, se permiten todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto **texto**, **ntext**, **imagen**definida por el usuario, tipos de tablas y  **marca de tiempo** tipos de datos. Los tipos de datos no escalares, **cursor** y **tabla**, no se puede especificar como un tipo de datos de parámetro en la vista [!INCLUDE[tsql](../../includes/tsql-md.md)] o las funciones CLR.  
  
 Si *type_schema_name* no se especifica, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] busca el *scalar_parameter_data_type* en el siguiente orden:  
  
-   El esquema que contiene los nombres de los tipos de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El esquema predeterminado del usuario actual en la base de datos actual.  
  
-   El esquema **dbo** de la base de datos actual.  
  
 [=*predeterminado* ]  
 Es un valor predeterminado para el parámetro. Si un *predeterminado* se define un valor, la función se puede ejecutar sin especificar un valor para ese parámetro.  
  
> [!NOTE]  
>  Se pueden especificar valores de parámetros predeterminados para las funciones CLR excepto para la **varchar (max)** y **varbinary (max)** tipos de datos.  
  
 Cuando un parámetro de la función tiene un valor predeterminado, se debe especificar la palabra clave DEFAULT al llamar a la función para recuperar el valor predeterminado. Este comportamiento es distinto del uso de parámetros con valores predeterminados en los procedimientos almacenados, donde la omisión del parámetro implica especificar el valor predeterminado. Sin embargo, la palabra clave DEFAULT no se requiere cuando se invoca una función escalar mediante la instrucción EXECUTE.  
  
 READONLY  
 Indica que el parámetro no se puede actualizar ni modificar en la definición de la función. Si el tipo de parámetro es un tipo de tabla definido por el usuario, se debe especificar READONLY.  
  
 *return_data_type*  
 Es el valor devuelto de una función escalar definida por el usuario. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] se permiten funciones, todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto el **timestamp** tipo de datos. Para las funciones CLR, se permiten todos los tipos de datos, incluidos los tipos definidos por el usuario CLR, excepto el **texto**, **ntext**, **imagen**, y **timestamp**tipos de datos. Los tipos de datos no escalares, **cursor** y **tabla**, no se puede especificar como un tipo de datos de retorno en la vista [!INCLUDE[tsql](../../includes/tsql-md.md)] o las funciones CLR.  
  
 *function_body*  
 Especifica que una serie de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], que juntas no producen ningún efecto secundario (como modificar una tabla), definen el valor de la función. *function_body* solo se usa en funciones escalares y funciones con valores de tabla de múltiples instrucciones.  
  
 En las funciones escalares, *cuerpo_función* es una serie de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones que juntas se evalúan como un valor escalar.  
  
 En funciones con valores de tabla de múltiples instrucciones, *cuerpo_función* es una serie de [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones que rellenan una tabla devuelven variable.  
  
 *scalar_expression*  
 Especifica el valor escalar que devuelve la función escalar.  
  
 TABLE  
 Especifica que el valor devuelto de la función con valores de tabla es una tabla. Sólo las constantes y @*local_variables* puede pasarse a funciones con valores de tabla.  
  
 En las funciones insertadas con valores de tabla, el valor devuelto de TABLE se define mediante una única instrucción SELECT. Las funciones insertadas no tienen variables devueltas asociadas.  
  
 En funciones con valores de tabla de múltiples instrucciones, @*return_variable* es una variable de tabla utilizada para almacenar y acumular las filas que se deben devolver como el valor de la función. @*return_variable* se puede especificar sólo para [!INCLUDE[tsql](../../includes/tsql-md.md)] las funciones y no para funciones CLR.  
  
> [!WARNING]  
>  Unirse a una tabla de múltiples instrucciones con valores de función en un **FROM** cláusula es posible, pero puede provocar un rendimiento bajo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede usar todas las técnicas optimizadas frente a ciertas instrucciones que se pueden incluir en una función de múltiples instrucciones, ya que conllevaría que el plan de consulta no alcanzase un nivel óptimo. Para lograr el mejor rendimiento, siempre que sea posible, use combinaciones entre las tablas base en lugar de funciones.  
  
 *select_stmt*  
 Es la instrucción SELECT individual que define el valor devuelto de una función insertada con valores de tabla.  
  
 ORDEN (\<order_clause >) especifica el orden en el que se devuelven resultados de la función con valores de tabla. Para obtener más información, vea la sección "Instrucciones para usar el criterio de ordenación" más adelante en este tema.  
  
 NOMBRE externo \<method_specifier > *assembly_name*. *CLASS_NAME*. *NombreMétodo* **se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el ensamblado y el método al que deberá hacer referencia el nombre de la función creada.  
  
-   *ASSEMBLY_NAME* -debe coincidir con un valor en la `name` columna de   
    `SELECT * FROM sys.assemblies;`.  
    Este es el nombre que se utilizó en la instrucción `CREATE ASSEMBLY`.  
  
-   *CLASS_NAME* -debe coincidir con un valor en la `assembly_name` columna de  
    `SELECT * FROM sys.assembly_modules;`.  
    A menudo el valor contiene un punto incrustado. En tales casos, el código Transact-SQL sintaxis requiere que el valor se limite con un par de corchetes recta [], o con un par de comillas dobles "".  
  
-   *NombreMétodo* -debe coincidir con un valor en la `method_name` columna de   
    `SELECT * FROM sys.assembly_modules;`.  
    El método debe ser estático.  
  
 En un ejemplo típico de MyFood.DLL, en el que todos los tipos están en el espacio de nombres MyFood, el valor de `EXTERNAL NAME` podría ser:   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
>  De manera predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede ejecutar código CLR. Puede crear, modificar y quitar objetos de base de datos que hagan referencia a common language runtime módulos; Sin embargo, no se puede ejecutar estas referencias en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta que habilite la [opción clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar esta opción, utilice [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 *\<*table_type_definition *>*  ({ \<definición_de_columna > \<column_constraint > | \<definición_de_columna_calculada >}    [ \<table_constraint >] [ ,... *n*  ]) Define el tipo de datos de la tabla para una [!INCLUDE[tsql](../../includes/tsql-md.md)] función. La declaración de tabla incluye definiciones de columna y restricciones de columna o de tabla. La tabla se coloca siempre en el grupo de archivos principal.  
  
 \<definición_de_tipo_de_tabla_clr > ({ *column_name**data_type* } [ ,... *n*  ]) **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([vista previa en algunas regiones](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)). |  
  
 Define los tipos de datos de tabla para una función CLR. La declaración de tabla solamente incluye nombres de columna y tipos de datos. La tabla se coloca siempre en el grupo de archivos principal.  
  
 NULL | NO ES NULL  
 Admite solo para los compilados de forma nativa, escalares funciones definidas por el usuario. Para obtener más información, consulte [Scalar User-Defined funciones para OLTP en memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Indica si una función definida por el usuario se compila de forma nativa. Este argumento es necesario para las funciones definidas por el usuario compiladas de forma nativa, escalares.  
  
 BEGIN ATOMIC CON  
 Admite solo de forma nativa, las funciones escalares definidas por el usuario y es necesario. Para obtener más información, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 El argumento SCHEMABINDING se requiere para las funciones definidas por el usuario compiladas de forma nativa, escalares.  
  
 EXECUTE AS  
 EXECUTE AS es necesario para las funciones definidas por el usuario compiladas de forma nativa, escalares.  
  
 **\<function_option >:: = y \<clr_function_option >:: =** 
  
 Especifica que la función tendrá una o más de las siguientes opciones.  
  
 ENCRYPTION  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] convertirá el texto original de la instrucción CREATE FUNCTION a un formato confuso. La salida de los datos confusos no es directamente visible en ninguna de las vistas de catálogo. Los usuarios que no disponen de acceso a las tablas del sistema o a los archivos de base de datos no pueden recuperar el texto protegido. Sin embargo, el texto estará disponible para los usuarios con privilegios que pueden tener acceso a las tablas del sistema sobre el [puerto DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) o directamente a los archivos de base de datos. Además, los usuarios que pueden adjuntar un depurador al proceso del servidor pueden recuperar el procedimiento original de la memoria en tiempo de ejecución. Para obtener más información acerca del acceso a los metadatos del sistema, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 El uso de esta opción impide que la función se publique como parte de la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opción no se puede especificar para funciones CLR.  
  
 SCHEMABINDING  
 Especifica que la función está enlazada a los objetos de base de datos a los que hace referencia. Cuando se especifica SCHEMABINDING, los objetos base no se pueden modificar de una forma que afecte a la definición de la función. En primer lugar, se debe modificar o quitar la propia definición de la función para quitar las dependencias en el objeto que se va a modificar.  
  
 El enlace de la función a los objetos a los que hace referencia solamente se quita cuando se ejecuta una de estas acciones: 
  
-   Se quita la función.  
  
-   La función se modifica con la instrucción ALTER sin especificar la opción SCHEMABINDING.  
  
 Una función se puede enlazar a esquema solamente si se cumplen las siguientes condiciones:  
  
-   La función es una función de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Las funciones definidas por el usuario y las vistas a las que hace referencia la función también están enlazadas al esquema.  
  
-   La función hace referencia a los objetos utilizando un nombre en dos partes.  
  
-   La función y los objetos a los que hace referencia pertenecen a la misma base de datos.  
  
-   El usuario que ejecutó la instrucción CREATE FUNCTION tiene permisos REFERENCES para los objetos de base de datos a los que hace referencia la función.  
  
 DEVUELVE NULL EN LA ENTRADA NULL | **LLAMA EN LA ENTRADA NULL**  
 Especifica la **OnNULLCall** atributo de una función con valores escalares. Si no se especifica, se utiliza CALLED ON NULL INPUT de manera predeterminada. Esto significa que el cuerpo de la función se ejecuta aunque se envíe NULL como argumento.  
  
 Si se especifica RETURNS NULL ON NULL INPUT en una función CLR, esto indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver NULL cuando cualquiera de los argumentos que recibe sea NULL, sin invocar realmente el cuerpo de la función. Si el método de una función CLR especifica en \<method_specifier > ya tiene un atributo personalizado que indica RETURNS NULL ON NULL INPUT, pero la instrucción CREATE FUNCTION indica CALLED ON NULL INPUT, la toma de la instrucción CREATE FUNCTION precedencia. El **OnNULLCall** atributo no se puede especificar para las funciones con valores de tabla CLR. 
  
 Cláusula EXECUTE AS  
 Especifica el contexto de seguridad en el que se ejecuta la función definida por el usuario. Por lo tanto, puede controlar qué cuenta de usuario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza para validar los permisos en los objetos de base de datos que se hace referencia a la función.  
  
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
 Especifica la intercalación de la columna. Si no se especifica, se asigna a la columna la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Para obtener una lista de y obtener más información acerca de las intercalaciones, vea [nombre de intercalación de Windows &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) y [SQL nombre de intercalación de servidor &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
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
  
 PAD_INDEX = {ON | **OFF** }  
 Especifica el relleno del índice. El valor predeterminado es OFF.  
  
 Valor de FILLFACTOR = *fillfactor*  
 Especifica un porcentaje que indica cómo el [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe realizar el nivel de hoja de cada página de índice durante la creación de índices o cambiar. *valor de FILLFACTOR* debe ser un valor entero entre 1 y 100. El valor predeterminado es 0.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Especifica la respuesta de error cuando una operación de inserción intenta insertar valores de clave duplicados en un índice único. La opción IGNORE_DUP_KEY se aplica solamente a operaciones de inserción realizadas tras crear o volver a generar el índice. El valor predeterminado es OFF.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF** }  
 Especifica si se vuelven a calcular las estadísticas de distribución. El valor predeterminado es OFF.  
  
 ALLOW_ROW_LOCKS = { **ON** | {OFF}  
 Especifica si se permiten los bloqueos de fila. El valor predeterminado es ON.  
  
 ALLOW_PAGE_LOCKS = { **ON** | {OFF}  
 Especifica si se permiten bloqueos de página. El valor predeterminado es ON.  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Si una función definida por el usuario no se crea con la cláusula SCHEMABINDING, los cambios que se realicen en los objetos subyacentes pueden afectar a la definición de la función y generar resultados inesperados al invocarla. Recomendamos implementar uno de los siguientes métodos para garantizar que la función no queda sin actualizar como consecuencia de los cambios realizados en sus objetos subyacentes:  
  
-   Especifique la cláusula WITH SCHEMABINDING al crear la función. Así se asegura de que no se pueden modificar los objetos a los que se hace referencia en la definición de la función a menos que también se modifique la función.  
  
-   Ejecute el [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) procedimiento almacenado después de modificar cualquier objeto que se especifica en la definición de la función.  
  
## <a name="data-types"></a>Tipos de datos  
 Si se especifican parámetros en una función CLR, deben ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos tal y como se ha definido previamente para *scalar_parameter_data_type*. Para obtener información acerca de cómo comparar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de sistema de tipos de datos de integración de CLR o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipos de datos de common language runtime, vea [asignación de datos de parámetro de CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hacer referencia al método correcto cuando está sobrecargado en una clase, el método indicado en \<method_specifier > debe tener las siguientes características: 
  
-   Recibir el mismo número de parámetros que se especifica en [ ,...*n* ].  
  
-   Recibir todos los parámetros por valor y no por referencia.  
  
-   Utilizar tipos de parámetros que sean compatibles con los especificados en la función de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si el tipo de datos devuelto de la función CLR especifica un tipo de tabla (RETURNS TABLE), el tipo de datos devuelto del método en \<method_specifier > debe ser de tipo **IEnumerator** o **IEnumerable**, y se supone que el creador de la función implementa la interfaz. A diferencia de [!INCLUDE[tsql](../../includes/tsql-md.md)] funciones, las funciones CLR no pueden incluir restricciones KEY, UNIQUE o CHECK principal en \<table_type_definition >. Los tipos de datos de las columnas especificadas en \<table_type_definition > deben coincidir con los tipos de las columnas correspondientes del conjunto de resultados devuelto por el método en \<method_specifier > en tiempo de ejecución. Esta comprobación del tipo no se lleva a cabo en el momento de crear la función. 
  
 Para obtener más información acerca de cómo programar funciones CLR, vea [funciones definidos](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md).  
  
## <a name="general-remarks"></a>Notas generales  
 Se pueden invocar funciones escalares cuando se utilizan expresiones escalares. Esto incluye las columnas calculadas y las definiciones de restricciones CHECK. Funciones escalares también se pueden ejecutar mediante el uso de la [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) instrucción. Las funciones escalares deben invocarse como mínimo con el nombre de dos partes de la función. Para obtener más información sobre los nombres de varias partes, vea [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). Las funciones con valores de tabla se pueden invocar cuando se admiten expresiones de tabla en la cláusula FROM de instrucciones SELECT, INSERT, UPDATE o DELETE. Para obtener más información, consulte [funciones definidas por el usuario ejecute](../../relational-databases/user-defined-functions/execute-user-defined-functions.md).  
  
## <a name="interoperability"></a>Interoperabilidad  
 Las siguientes instrucciones son válidas en una función:  
  
-   Instrucciones de asignación.  
  
-   Instrucciones de control de flujo, excepto las instrucciones TRY...CATCH.  
  
-   Instrucciones DECLARE que definen variables de datos locales y cursores locales.  
  
-   Instrucciones SELECT que contienen listas de selección con expresiones que asignan valores a variables locales.  
  
-   Operaciones de cursor que hacen referencia a cursores locales que se declaran, abren, cierran y cuya asignación se cancela en la función. Solamente se permiten las instrucciones FETCH que asignan valores a las variables locales mediante la cláusula INTO; no se permiten las instrucciones FETCH que devuelven datos al cliente.  
  
-   Instrucciones INSERT, UPDATE y DELETE que modifican variables de tabla locales.  
  
-   Instrucciones EXECUTE que llaman a procedimientos almacenados extendidos.  
  
-   Para obtener más información, consulte [definido por el usuario crear funciones &#40; motor de base de datos &#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
### <a name="computed-column-interoperability"></a>Interoperabilidad de columna calculada  
 Las funciones tienen las propiedades siguientes. Los valores de estas propiedades determinan si las funciones se pueden utilizar en columnas calculadas, que pueden ser persistentes o indizadas.  
  
|Propiedad|Description|Notas|  
|--------------|-----------------|-----------|  
|**IsDeterministic**|La función es determinista o no determinista.|En las funciones deterministas, se permite el acceso a los datos locales. Por ejemplo, se consideran deterministas las funciones que devuelven siempre el mismo resultado al llamarlas, utilizando un conjunto específico de valores de entrada y con el mismo estado de la base de datos.|  
|**IsPrecise**|La función es precisa o imprecisa.|Las funciones imprecisas contienen operaciones, como operaciones de punto flotante.|  
|**IsSystemVerified**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede comprobar las propiedades de precisión y determinismo de la función.||  
|**SystemDataAccess**|La función tiene acceso a los datos del sistema (catálogos del sistema o tablas del sistema virtuales) en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].||  
|**UserDataAccess**|La función tiene acceso a los datos del usuario en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Incluye las tablas temporales y las definidas por el usuario, pero no las variables de tabla.|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] determina automáticamente las propiedades de precisión y determinismo de las funciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El usuario puede especificar las propiedades de acceso a datos y determinismo de las funciones CLR. Para obtener más información, consulte [información general de CLR Integration personalizado atributos](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820).  
  
 Para mostrar los valores actuales de estas propiedades, use [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
 Se deben crear las funciones de manera que el enlace de esquema sea determinista.  
  
 Una columna calculada que llama a una función definida por el usuario se puede utilizar en un índice cuando la función definida por el usuario tiene los siguientes valores de propiedades:  
  
-   **IsDeterministic** = true  
  
-   **IsSystemVerified** = true (a menos que la columna calculada sea persistente)  
  
-   **UserDataAccess** = false  
  
-   **SystemDataAccess** = false  
  
 Para obtener más información, vea [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>Llamar a procedimientos almacenados extendidos desde funciones  
 Cuando se llama a un procedimiento almacenado extendido desde una función, no se puede devolver al cliente el conjunto de resultados. Cualquier API ODS que devuelva conjuntos de resultados al cliente devolverá FAIL. El procedimiento almacenado extendido se puede volver a conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; sin embargo, no debería intentar combinar la misma transacción como la función que invocó el procedimiento almacenado extendido.  
  
 Como ocurre con las invocaciones desde un proceso por lotes o un procedimiento almacenado, el procedimiento almacenado extendido se ejecutará en el contexto de la cuenta de seguridad de Windows en la que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El propietario del procedimiento almacenado debe tener esto en cuenta al otorgar permisos EXECUTE a los usuarios.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Las funciones definidas por el usuario no se pueden utilizar para realizar acciones que modifican el estado de la base de datos.  
  
 Las funciones definidas por el usuario no pueden tener una cláusula OUTPUT INTO que tenga una tabla como destino.  
  
 Las siguientes instrucciones de [!INCLUDE[ssSB](../../includes/sssb-md.md)] no se pueden incluir en la definición de una función [!INCLUDE[tsql](../../includes/tsql-md.md)] definida por el usuario:  
  
-   EMPEZAR CONVERSACIÓN DE DIÁLOGO  
  
-   FINALIZAR CONVERSACIÓN  
  
-   GET CONVERSATION GROUP  
  
-   MOVE CONVERSATION  
  
-   RECEIVE  
  
-   ENVIAR  
  
 Las funciones definidas por el usuario se pueden anidar; es decir, una función definida por el usuario puede llamar a otra. El nivel de anidamiento aumenta cuando se empieza a ejecutar la función llamada y disminuye cuando se termina de ejecutar la función llamada. Las funciones definidas por el usuario se pueden anidar hasta un máximo de 32 niveles. Si se superan los niveles máximos de anidamiento, la cadena completa de funciones de llamada produce un error. Cualquier referencia a código administrado desde una función [!INCLUDE[tsql](../../includes/tsql-md.md)] definida por el usuario cuenta como uno de los 32 niveles de anidamiento. Los métodos invocados desde el código administrado no cuentan para este límite.  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>Usar el criterio de ordenación en funciones CLR con valores de tabla  
 Cuando utilice la cláusula ORDER en funciones CLR con valores de tabla, siga estas instrucciones:  
  
-   Debe asegurarse de que los resultados siempre se ordenan según el criterio especificado. Si los resultados no están en el orden especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un mensaje de error cuando se ejecute la consulta.  
  
-   Si se especifica una cláusula ORDER, el resultado de la función con valores de tabla debe estar ordenado según la intercalación de la columna (explícita o implícita). Por ejemplo, si la intercalación de la columna es chino (especificado en el archivo DDL para la función con valores de tabla u obtenido a partir de la intercalación de la base de datos), los resultados devueltos deben estar ordenados según las reglas de ordenación chinas.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre comprueba la cláusula ORDER, si se especifica, durante la devolución de resultados, independientemente de si el procesador de consultas la utiliza para realizar más optimizaciones o no. Utilice la cláusula ORDER solamente si sabe que será útil para el procesador de consultas.  
  
-   El procesador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza de forma automática la cláusula ORDER en los siguientes casos:  
  
    -   Consultas Insert en las que la cláusula ORDER es compatible con un índice.  
  
    -   Cláusulas ORDER BY que son compatibles con la cláusula ORDER.  
  
    -   Agregados, donde GROUP BY es compatible con la cláusula ORDER.  
  
    -   Agregados DISTINCT donde las columnas distintas son compatibles con la cláusula ORDER.  
  
 La cláusula ORDER no garantiza que los resultados estarán ordenados al ejecutar una consulta SELECT, a menos que también se especifique la cláusula ORDER BY en la consulta. Vea [sys.function_order_columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md) para obtener información acerca de cómo consultar las columnas incluidas en el criterio de ordenación para las funciones con valores de tabla.  
  
## <a name="metadata"></a>Metadatos  
 En la siguiente tabla se enumeran las vistas de catálogo del sistema que puede utilizar para devolver metadatos sobre las funciones definidas por el usuario.  
  
|Vista del sistema|Description|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Vea el ejemplo E en la siguiente sección de ejemplos.|  
|[Sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Muestra información sobre funciones definidas por el usuario CLR.|  
|[Sys.Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Muestra información sobre los parámetros definidos en funciones definidas por el usuario.|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|Muestra los objetos subyacentes a los que hace referencia una función.|  
  
## <a name="permissions"></a>Permissions  
 Se requiere el permiso CREATE FUNCTION en la base de datos y el permiso ALTER en el esquema en el que se va a crear la función. Si la función especifica un tipo definido por el usuario, requiere el permiso EXECUTE para ese tipo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>A. Usar una función con valores escalares definida por el usuario que calcula la semana ISO  
 En el ejemplo siguiente se crea la función definida por el usuario `ISOweek`. Esta función usa un argumento de fecha para calcular el número de semana ISO. Para que esta función calcule correctamente, se debe invocar `SET DATEFIRST 1` antes de llamar a la función.  
  
 El ejemplo también muestra el uso de la [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) cláusula para especificar el contexto de seguridad en el que se puede ejecutar un procedimiento almacenado. En el ejemplo, la opción `CALLER` especifica que el procedimiento se ejecutará en el contexto del usuario que lo llama. Las demás opciones que puede especificar son SELF, OWNER y *nombre_usuario*.  
  
 Esta es la llamada a la función. Observe que el valor de `DATEFIRST` es `1`.  
  
```tsql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Crear una función alineada con valores de tabla  
 El ejemplo siguiente devuelve una función insertada con valores de tabla en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Devuelve tres columnas `ProductID`, `Name` y la suma de los totales del año hasta la fecha por tienda como `YTD Total` para cada producto vendido en el almacén.  
  
```tsql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 Para invocar la función, ejecute esta consulta.    

```tsql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>C. Crear una función con valores de tabla de múltiples instrucciones  
 En el ejemplo siguiente se crea la función con valores de tabla `fn_FindReports(InEmpID)` en la base de datos AdventureWorks2012. Cuando se suministra un identificador de empleado válido, la función devuelve una tabla de todos los empleados que están bajo las órdenes de ese empleado tanto directa como indirectamente. La función utiliza la expresión de tabla común (CTE) recursiva para producir la lista jerárquica de empleados. Para obtener más información sobre las CTE recursivas, vea [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
```tsql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>D. Crear una función CLR  
 En el ejemplo se crea la función CLR `len_s`. Antes de crear la función, el ensamblado `SurrogateStringFunction.dll` se registra en la base de datos local.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```tsql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 Para obtener un ejemplo de cómo crear una función con valores de tabla CLR, vea [CLR Table-Valued funciones](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md).  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>E. Mostrar la definición de [!INCLUDE[tsql](../../includes/tsql-md.md)] funciones definidas por el usuario  
  
```tsql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 La definición de funciones creadas con la opción ENCRYPTION no se puede ver con sys.sql_modules; sin embargo, se muestra otra información acerca de las funciones cifradas.  
  
## <a name="see-also"></a>Vea también  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [DROP FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [OBJECTPROPERTYEX &#40; Transact-SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Funciones definidas por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear directiva de seguridad &#40; Transact-SQL &#41;](../../t-sql/statements/create-security-policy-transact-sql.md)  
  
 


