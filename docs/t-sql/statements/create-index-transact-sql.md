---
title: "Crear índice (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
caps.latest.revision: "223"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 92e32f9a86265376a67466aa389f29ec9608a061
ms.sourcegitcommit: 4a462c7339dac7d3951a4e1f6f7fb02a3e01b331
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2017
---
# <a name="create-index-transact-sql"></a>CREATE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea un índice relacional en una tabla o vista. También llama a un índice de almacén de filas porque es un índice de árbol b agrupado o no. Puede crear un índice de almacén de filas antes de que hay datos en la tabla. Utilizar un índice de almacén de filas para mejorar el rendimiento de las consultas, especialmente cuando las consultas, seleccione en columnas específicas o requieren valores que se va a ordenar en un orden concreto.  
  
  
> [!NOTE]  
>  Almacenamiento de datos SQL de Azure y almacenamiento de datos paralelos actualmente no admiten restricciones Unique. Los ejemplos que hacen referencia a las restricciones Unique solo son aplicables a SQL Server y base de datos de SQL Azure    
  
 **Ejemplos sencillos:**  
  
```  
-- Create a nonclustered index on a table or view  
CREATE INDEX i1 ON t1 (col1);  
```  
  
```  
--Create a clustered index on a table and use a 3-part name for the table  
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);  
```  
  
```  
-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint 
-- on 3 columns and specify the sort order for each column  
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);  
```  
  
 **Escenarios clave:**  
  
-   En SQL Server 2016 y base de datos de SQL Azure, utilice un índice no agrupado en un índice de almacén de columnas para mejorar el rendimiento de las consultas de almacenamiento de datos. Vea [índices de almacén de columnas - almacenamiento de datos](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
 **¿Necesita crear un tipo diferente de índice?**  
  
-   [Crear índice XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)  
  
-   [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
-   [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )   
    [ INCLUDE ( column_name [ ,...n ] ) ]  
    [ WHERE <filter_predicate> ]  
    [ WITH ( <relational_index_option> [ ,...n ] ) ]  
    [ ON { partition_scheme_name ( column_name )   
         | filegroup_name   
         | default   
         }  
    ]  
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<relational_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | STATISTICS_INCREMENTAL = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE | ROW | PAGE}   
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
     [ , ...n ] ) ]  
}  
  
<filter_predicate> ::=   
    <conjunct> [ AND <conjunct> ]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...n)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
Backward Compatible Relational Index  
Important   The backward compatible relational index syntax structure 
will be removed in a future version of SQL Server. Avoid using this 
syntax structure in new development work, and plan to modify 
applications that currently use the feature. Use the syntax structure 
specified in <relational_index_option> instead.  
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )   
    [ WITH <backward_compatible_index_option> [ ,...n ] ]  
    [ ON { filegroup_name | "default" } ]  
  
<object> ::=  
{  
    [ database_name. [ owner_name ] . | owner_name. ]   
    table_or_view_name  
}  
  
<backward_compatible_index_option> ::=  
{   
    PAD_INDEX  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB  
  | IGNORE_DUP_KEY  
  | STATISTICS_NORECOMPUTE   
  | DROP_EXISTING   
}  
```  

  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON [ database_name . [ schema ] . | schema . ] table_name   
        ( { column [ ASC | DESC ] } [ ,...n ] )  
    WITH ( DROP_EXISTING = { ON | OFF } )  
[;]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 UNIQUE  
 Crea un índice único en una tabla o una vista. Un índice único es aquel en el que no se permite que dos filas tengan el mismo valor de clave del índice. El índice clúster de una vista debe ser único.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] no admite la creación de un índice único sobre columnas que ya contengan valores duplicados, independientemente de si se ha establecido o no IGNORE_DUP_KEY en ON. Si se intenta, [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestra un mensaje de error. Se deben quitar los valores duplicados para poder crear un índice único en la columna o columnas. Las columnas que se utilizan en un índice único se deben establecer en NOT NULL, dado que varios valores NULL se consideran duplicados cuando se crea un índice único.  
  
 CLUSTERED  
 Crea un índice en el que el orden lógico de los valores de clave determina el orden físico de las filas correspondientes de la tabla. El nivel inferior, u hoja, de un índice clúster contiene las filas de datos reales de la tabla. Una tabla o vista permite un índice clúster al mismo tiempo.  
  
 Una vista con un índice clúster único se denomina vista indizada. La creación de un índice clúster único en una vista materializa físicamente la vista. Es necesario crear un índice clúster único en una vista para poder definir otros índices en la misma vista. Para obtener más información, vea [Crear vistas indexadas](../../relational-databases/views/create-indexed-views.md).  
  
 Cree el índice clúster antes de crear los índices no clúster. Los índices no clúster existentes en las tablas se vuelven a generar al crear un índice clúster.  
  
 Si no se especifica CLUSTERED, se crea un índice no clúster.  
  
> [!NOTE]  
>  Porque el nivel de hoja de un índice clúster y las páginas de datos son los mismos por definición, crear un índice agrupado y usar el ON *partition_scheme_name* u ON *filegroup_name* cláusula eficazmente mueve una tabla desde el grupo de archivos en el que se creó la tabla para el nuevo esquema de partición o grupo de archivos. Antes de crear tablas o índices en grupos de archivos específicos, compruebe cuáles están disponibles y que esos grupos de archivos tengan suficiente espacio disponible para el índice.  
  
 En algunos casos, al crear un índice clúster se pueden habilitar previamente los índices deshabilitados. Para obtener más información, consulte [habilitar índices y restricciones](../../relational-databases/indexes/enable-indexes-and-constraints.md) y [deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
 **NO AGRUPADO**  
 Crea un índice que especifica la ordenación lógica de una tabla. Con un índice no clúster, el orden físico de las filas de datos es independiente del orden indizado.  
  
 Cada tabla puede tener hasta 999 índices no clúster, independientemente de cómo se crean: de forma implícita con las restricciones PRIMARY KEY y UNIQUE, o explícita con CREATE INDEX.  
  
 Para las vistas indizadas, solo se pueden crear índices no clúster en una vista que ya tenga definido un índice clúster único.  
  
 El valor predeterminado es NONCLUSTERED.  
  
 *index_name*  
 Es el nombre del índice. Los nombres de índice deben ser únicos en una tabla o vista, pero no es necesario que sean únicos en una base de datos. Los nombres de índice deben seguir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *column*  
 Es la columna o columnas en las que se basa el índice. Especifique dos o más nombres de columna para crear un índice compuesto sobre los valores combinados de las columnas especificadas. Enumere las columnas que pueden incluirse en el índice compuesto, en orden de prioridad de ordenación, entre paréntesis después *nombre_tabla_o_vista*.  
  
 Hasta 32 columnas se pueden combinar en una clave de índice compuesto único. Todas las columnas de una clave del índice compuesto deben encontrarse en la misma tabla o vista. El tamaño máximo permitido de los valores de índice combinado es 900 bytes para un índice agrupado o 1700 para un índice no agrupado. Los límites son 16 columnas y 900 bytes para las versiones anteriores a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
 Las columnas de los tipos de datos de objetos grandes (LOB) **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**,  **varbinary (max)**, **xml**, o **imagen** no se puede especificar como columnas de clave para un índice. Además, no puede incluir una definición de vista **ntext**, **texto**, o **imagen** columnas, incluso si no que se hace referencia en la instrucción CREATE INDEX.  
  
 Puede crear índices en columnas de tipo definido por el usuario CLR si el tipo admite el orden binario. También puede crear índices en columnas calculadas que están definidas como invocaciones de método de una columna de tipo definido por el usuario, siempre que los métodos estén marcados como deterministas y no realicen operaciones de acceso a datos. Para obtener más información acerca de la indización de columnas de tipo definido por el usuario CLR, vea [tipos definidos por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 [ **ASC** | DESC]  
 Determina la dirección ascendente o descendente del orden de la columna de índice determinada. El valor predeterminado es ASC.  
  
 INCLUIR **(***columna* [ **,**... *n* ] **)**  
 Especifica las columnas que no son de clave que se agregarán en el nivel hoja del índice no clúster. El índice no clúster puede ser único o no único.  
  
 Los nombres de columna no se pueden repetir en la lista INCLUDE y no se pueden utilizar simultáneamente como columnas de clave y que no son de clave. Los índices no clúster siempre contienen las columnas de índice clúster si se define un índice clúster en la tabla. Para más información, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
 Se admiten todos los tipos de datos, a excepción de **text**, **ntext**e **image**. El índice se debe crear o reconstruir sin conexión (ONLINE = OFF) si cualquiera de las columnas sin clave especificadas son **varchar (max)**, **nvarchar (max)**, o **varbinary (max)** datos tipos.  
  
 Las columnas calculadas que son deterministas, y precisas o imprecisas, pueden ser columnas incluidas. Las columnas calculadas derivadas de **imagen**, **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, y **xml** tipos de datos pueden incluirse en columnas sin clave siempre que los tipos de datos de columna calculada esté disponible como una columna incluida. Para obtener más información, vea [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
 Para obtener información acerca de cómo crear un índice XML, vea [CREATE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-xml-index-transact-sql.md).  
  
 DONDE \<filter_predicate > crea un índice filtrado especificando qué filas desea incluir en el índice. El índice filtrado debe ser un índice no clúster en una tabla. Crea las estadísticas filtradas para las filas de datos en el índice filtrado.  
  
 El predicado de filtro utiliza la lógica de comparación simple y no puede hacer referencia a una columna calculada, a una columna UDT, a una columna de tipo de datos espacial o a una columna de tipo de datos hierarchyID. Las comparaciones que utilizan literales NULL no se admiten con los operadores de comparación. En su lugar, use los operadores IS NULL e IS NOT NULL.  
  
 A continuación, se muestran algunos ejemplos de predicados de filtro para la tabla `Production.BillOfMaterials`:  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Los índices filtrados no se aplican a los índices XML ni a los índices de texto completo. Para los índices UNIQUE, solo las filas seleccionadas deben tener valores de índice únicos. Los índices filtrados no admiten la opción IGNORE_DUP_KEY.  
  
 ON *partition_scheme_name***(***column_name***)**  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica el esquema de partición que define los grupos de archivos a los que se asignarán las particiones de un índice con particiones. El esquema de partición debe existir en la base de datos mediante la ejecución [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) o [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *column_name* especifica la columna en la que se crearán con particiones un índice con particiones. Esta columna debe coincidir con el tipo de datos, la longitud y la precisión del argumento de la partición de la función que *partition_scheme_name* está usando. *column_name* no está restringida a las columnas de la definición del índice. Puede especificar cualquier columna de la tabla base, excepto cuando un índice único, de creación de particiones *column_name* se debe elegir entre las que se usan como clave única. Esta restricción permite que [!INCLUDE[ssDE](../../includes/ssde-md.md)] compruebe la unicidad de los valores de clave en una única partición solamente.  
  
> [!NOTE]  
>  Cuando se crean particiones en un índice clúster no único, [!INCLUDE[ssDE](../../includes/ssde-md.md)] agrega de forma predeterminada la columna de partición a la lista de claves del índice clúster, en caso de que aún no se hubiera especificado. Cuando se crean particiones en un índice no clúster que tampoco es único, [!INCLUDE[ssDE](../../includes/ssde-md.md)] agrega la columna de partición como una columna sin clave (incluida) del índice, si aún no se especificó.  
  
 Si *partition_scheme_name* o *archivos* no se ha especificado y la tabla tiene particiones, el índice se sitúa en el mismo esquema de partición, con la misma columna de partición que la tabla subyacente.  
  
> [!NOTE]  
>  No se puede especificar un esquema de partición en un índice XML. Si se crean particiones en la tabla base, el índice XML usa el mismo esquema de partición que la tabla.  
  
 Para obtener más información acerca de las particiones de índices, [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 ON *filegroup_name*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Crea el índice especificado en el grupo de archivos especificado. Si no se ha especificado una ubicación y la tabla o vista no tiene particiones, el índice utiliza el mismo grupo de archivos que la tabla o vista subyacente. El grupo de archivos debe existir previamente.  
  
 ON **"**predeterminado**"**  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssCurrent](../../includes/sssdsfull-md.md)].  
  
 Crea el índice especificado en el grupo de archivos predeterminado.  
  
 El término predeterminado (default), en este contexto, no es una palabra clave. Es un identificador para el grupo de archivos predeterminado y debe delimitarse, como en ON **"**predeterminado**"** u ON **[**predeterminado**]**. Si se especifica "default", la opción QUOTED_IDENTIFIER debe tener el valor ON para la sesión actual. Esta es la configuración predeterminada. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 [FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL"}]  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la posición de datos FILESTREAM para la tabla cuando se crea un índice clúster. La cláusula FILESTREAM_ON permite mover los datos FILESTREAM a otro esquema de partición o a otro grupo de archivos FILESTREAM.  
  
 *filestream_filegroup_name* es el nombre de un grupo de archivos FILESTREAM. El grupo de archivos debe tener un archivo que se definen para el grupo de archivos mediante un [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) o [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrucción; en caso contrario, se produce un error.  
  
 Si se crean particiones de la tabla, la cláusula FILESTREAM_ON deberá incluirse y especificar un esquema de partición de grupos de archivos FILESTREAM que utilice la misma función de partición y columnas de partición que el esquema de partición para la tabla. En caso contrario, se produce un error.  
  
 Si la tabla no tiene particiones, no se pueden crear particiones en la columna FILESTREAM. Los datos FILESTREAM para la tabla deben estar almacenados en un grupo de archivos único que se especifica en la cláusula FILESTREAM_ON.  
  
 NULL de FILESTREAM_ON se puede especificar en una instrucción CREATE INDEX si se va a crear un índice clúster y la tabla no contiene una columna FILESTREAM.  
  
 Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 **\<objeto >:: =**  
  
 Es el objeto completo o no que se indizará.  
  
 *database_name*  
 Es el nombre de la base de datos.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la tabla o la vista.  
  
 *nombre_tabla_o_vista*  
 Es el nombre de la tabla o la vista que se va a indizar.  
  
 La vista debe definirse con SCHEMABINDING para crear un índice en ella. Es necesario crear un índice clúster único en una vista antes de crear los índices no clúster. Para obtener más información acerca de las vistas indizadas, vea la sección Comentarios.  
  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], el objeto puede ser una tabla almacenada con un índice de almacén de columnas agrupado.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]es compatible con el formato de nombre de tres partes *database_name***.** [*schema_name*]**.** *object_name* cuando el *database_name* es la base de datos actual o la *database_name* es tempdb y la *object_name*comienza con #.  
  
 **\<relational_index_option >:: =**  
  
 Especifica las opciones que se van a utilizar en la creación del índice.  
  
 PAD_INDEX = {ON | **OFF** }  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica el relleno del índice. El valor predeterminado es OFF.  
  
 ON  
 El porcentaje de espacio disponible especificado por *fillfactor* se aplica a las páginas de nivel intermedio del índice.  
  
 DESACTIVAR o *fillfactor* no se ha especificado  
 Las páginas de nivel intermedio se llenan casi al máximo de su capacidad y dejan espacio suficiente para al menos una fila del tamaño máximo que puede tener el índice, considerando el conjunto de claves incluidas en las páginas de nivel intermedio.  
  
 La opción PAD_INDEX solamente resulta útil si también se especifica FILLFACTOR, porque PAD_INDEX utiliza el mismo porcentaje especificado por FILLFACTOR. Si el porcentaje especificado para FILLFACTOR no es lo suficientemente grande como para admitir una fila, [!INCLUDE[ssDE](../../includes/ssde-md.md)] invalida internamente el porcentaje para permitir el valor mínimo. El número de filas de una página de índice intermedio es nunca inferior a dos, independientemente de lo bajo el valor de *fillfactor*.  
  
 En la sintaxis compatible con versiones anteriores, WITH PAD_INDEX es equivalente a WITH PAD_INDEX = ON.  
  
 Valor de FILLFACTOR  **=**  *fillfactor*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica un porcentaje que indica cuánto debe llenar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] el nivel hoja de cada página de índice durante la creación o nueva generación de los índices. *valor de FILLFACTOR* debe ser un valor entero entre 1 y 100. Si *fillfactor* es 100, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea índices con páginas hoja rellenadas en capacidad.  
  
 La configuración de FILLFACTOR solo se aplica cuando se crea o se vuelve a generar el índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mantiene dinámicamente el porcentaje especificado de espacio disponible de las páginas. Para ver el valor de factor de relleno, use la [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.  
  
> [!IMPORTANT]  
>  La creación de un índice clúster con un valor de FILLFACTOR menor que 100 afecta a la cantidad de espacio de almacenamiento que ocupan los datos, porque [!INCLUDE[ssDE](../../includes/ssde-md.md)] vuelve a distribuir los datos cuando crea el índice clúster.  
  
 Para obtener más información, vea [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica si se debe almacenar los resultados de ordenación temporales en **tempdb**. El valor predeterminado es OFF.  
  
 ON  
 Los resultados de orden intermedio que se usan para generar el índice se almacenan en **tempdb**. Esto puede reducir el tiempo necesario para crear un índice si **tempdb** está en un conjunto diferente de discos que en la base de datos de usuario. Sin embargo, esto aumenta la cantidad de espacio en disco utilizado durante la generación del índice.  
  
 OFF  
 Los resultados de orden intermedios se almacenan en la misma base de datos que el índice.  
  
 Además del espacio necesario en la base de datos de usuario para crear el índice, **tempdb** debe tener la misma cantidad de espacio adicional para almacenar los resultados de orden intermedio. Para obtener más información, consulte [opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 En la sintaxis compatible con versiones anteriores, WITH SORT_IN_TEMPDB es equivalente a WITH SORT_IN_TEMPDB = ON.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Especifica la respuesta de error cuando una operación de inserción intenta insertar valores de clave duplicados en un índice único. La opción IGNORE_DUP_KEY se aplica solamente a operaciones de inserción realizadas tras crear o volver a generar el índice. La opción no tiene ningún efecto cuando se ejecuta [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), o [actualización](../../t-sql/queries/update-transact-sql.md). El valor predeterminado es OFF.  
  
 ON  
 Se producirá un mensaje de advertencia cuando se inserten valores de clave duplicados en un índice único. Solo las filas que infrinjan la restricción de unicidad darán error.  
  
 OFF  
 Se producirá un mensaje de error cuando se inserten valores de clave duplicados en un índice único. Toda la operación INSERT se revertirá.  
  
 IGNORE_DUP_KEY no se puede establecer en ON para los índices creados en una vista, los índices que no sean únicos, los índices XML, los índices espaciales y los índices filtrados.  
  
 Para ver IGNORE_DUP_KEY, utilice [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 En la sintaxis compatible con versiones anteriores, WITH IGNORE_DUP_KEY es equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF**}  
 Especifica si se vuelven a calcular las estadísticas de distribución. El valor predeterminado es OFF.  
  
 ON  
 Las estadísticas obsoletas no se vuelven a calcular automáticamente.  
  
 OFF  
 Se habilita la actualización automática de las estadísticas.  
  
 Para restaurar la actualización automática de estadísticas, establezca STATISTICS_NORECOMPUTE en OFF o ejecute UPDATE STATISTICS sin la cláusula NORECOMPUTE.  
  
> [!IMPORTANT]  
>  Deshabilitar el cálculo automático de estadísticas de distribución puede impedir que el optimizador de consultas elija los planes de ejecución óptimos de las consultas relativas a la tabla.  
  
 En la sintaxis compatible con versiones anteriores, WITH STATISTICS_NORECOMPUTE es equivalente a WITH STATISTICS_NORECOMPUTE = ON.  
  
 STATISTICS_INCREMENTAL = {ON | **OFF** }  
 Cuando **ON**, son las estadísticas creadas por cada partición. Cuando **OFF**, se quita el árbol de estadísticas y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a calcular las estadísticas. El valor predeterminado es **OFF**.  
  
 Si no se admiten las estadísticas por partición, la opción se omite y se genera una advertencia. Las estadísticas incrementales no se admiten para los siguientes tipos de estadísticas:  
  
-   Estadísticas creadas con índices que no están alineados por partición con la tabla base.  
-   Estadísticas creadas sobre bases de datos secundarias legibles AlwaysOn.  
-   Estadísticas creadas sobre bases de datos de solo lectura.  
-   Estadísticas creadas sobre índices filtrados.  
-   Estadísticas creadas sobre vistas.  
-   Estadísticas creadas sobre tablas internas.  
-   Estadísticas creadas con índices espaciales o índices XML.  
  
 DROP_EXISTING = {ON | **OFF** }  
 Es una opción para quitar y volver a generar el índice agrupado o no existente con las especificaciones de la columna modificada y mantener el mismo nombre para el índice. El valor predeterminado es OFF.  
  
 ON  
 Especifica que se debe quitar y volver a generar el índice existente, que debe tener el mismo nombre que el parámetro *index_name*.  
  
 OFF  
 Especifica que no se quite y vuelva a generar el índice existente. SQL Server muestra un error si ya existe el nombre del índice especificado.  
  
 Con DROP_EXISTING, puede cambiar:  
  
-   Un índice no clúster de almacén de filas en un índice agrupado de almacén de filas.  
  
 Con DROP_EXISTING, no se puede cambiar:  
  
-   Un índice de almacén de filas agrupado a un índice no clúster de almacén de filas.  
  
-   Un índice de almacén de columnas agrupado a cualquier tipo de índice de almacén de filas.  
  
 En la sintaxis compatible con versiones anteriores, WITH DROP_EXISTING es equivalente a WITH DROP_EXISTING = ON.  
  
 ONLINE = {ON | **OFF** }  
 Especifica si las tablas subyacentes y los índices asociados están disponibles para realizar consultas y modificar datos durante la operación de índice. El valor predeterminado es OFF.  
  
> [!NOTE]  
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ON  
 Los bloqueos de tabla de larga duración no se mantienen durante la operación de indización. Durante la fase principal de la operación de índice, solo se mantiene un bloqueo preventivo en la tabla de origen. Esto habilita las consultas o actualizaciones en la tabla subyacente y en los índices. Al inicio de la operación, se mantiene un bloqueo compartido (S) en el objeto de origen durante un período de tiempo muy corto. Al final de la operación, se adquiere un bloqueo S (compartido) sobre el origen durante un corto período, si se está creando un índice no clúster; o bien, se adquiere un bloqueo SCH-M (modificación del esquema) cuando se crea o se quita un índice clúster en línea, y cuando se vuelve a crear un índice clúster o no clúster. ONLINE no se puede establecer en ON cuando se crea un índice en una tabla temporal local.  
  
 OFF  
 Los bloqueos de tabla se aplican durante la operación de índice. Una operación de índice sin conexión para crear, volver a crear o quitar un índice clúster, o para volver a crear o quitar un índice no clúster, adquiere un bloqueo de modificación del esquema (Sch-M) de la tabla. Esto evita que todos los usuarios tengan acceso a la tabla subyacente durante la operación. Una operación de índice sin conexión que crea un índice no clúster adquiere un bloqueo compartido (S) en la tabla. Esto evita que se realicen actualizaciones en la tabla subyacente, pero permite la realización de operaciones de lectura, como instrucciones SELECT.  
  
 Para obtener más información, consulte [cómo funcionan de las operaciones de índice en línea](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Los índices, incluidos los índices de las tablas temp globales, se pueden crear en línea, con las excepciones siguientes:  
  
-   Índice XML  
-   Índice en una tabla temp local  
-   Índice clúster único inicial en una vista.  
-   Índices clúster deshabilitados.  
-   Índice clúster si la tabla subyacente contiene tipos de datos LOB: **imagen**, **ntext**, **texto**y los tipos espaciales.  
-   **varchar (max)** y **varbinary (max)** columnas no pueden formar parte de un índice. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) y en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], cuando una tabla contiene **varchar (max)** o **varbinary (max)** pueden ser un índice clúster que contiene otras columnas, columnas generan o se vuelven a generar con el **ONLINE** opción. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]no permite la **en línea** opción cuando la tabla base contiene **varchar (max)** o **varbinary (max)** columnas.  
  
 Para más información, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
 ALLOW_ROW_LOCKS = { **ON** | {OFF}  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica si se permiten los bloqueos de fila. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de fila se admiten al obtener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila.  
  
 OFF  
 No se usan los bloqueos de fila.  
  
 ALLOW_PAGE_LOCKS = { **ON** | {OFF}  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica si se permiten bloqueos de página. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de página se permiten al obtener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página.  
  
 OFF  
 No se utilizan bloqueos de página.  
  
 MAXDOP = *max_degree_of_parallelism*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Invalida el **grado máximo de paralelismo** opción de configuración para la duración de la operación de índice. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
 *max_degree_of_parallelism* puede ser:  
  
 1  
 Suprime la generación de planes paralelos.  
  
 \>1  
 Restringe el número máximo de procesadores utilizados en una operación de índice paralelo al número especificado o a un número inferior, en función de la actual carga de trabajo del sistema.  
  
 0 (predeterminado)  
 Usa el número real de procesadores o menos, según la carga de trabajo actual del sistema.  
  
 Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operaciones de índice en paralelo no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 DATA_COMPRESSION  
 Especifica la opción de compresión de datos para el índice, número de partición o intervalo de particiones especificado. Las opciones son las siguientes:  
  
 Ninguno  
 No se comprimen el índice ni las particiones especificadas.  
  
 ROW  
 El índice o las particiones especificadas se comprimen mediante la compresión de fila.  
  
 PAGE  
 El índice o las particiones especificadas se comprimen mediante la compresión de página.  
  
 Para obtener más información acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
 EN las particiones **(** { \<partition_number_expression > | \<intervalo >} [ **,**...  *n*  ] **)** **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica las particiones a las que se aplica el valor DATA_COMPRESSION. Si el índice no tiene particiones, el argumento ON PARTITIONS generará un error. Si no se proporciona la cláusula ON PARTITIONS, la opción DATA_COMPRESSION se aplica a todas las particiones de un índice con particiones.  
  
 \<partition_number_expression > se puede especificar de las maneras siguientes:  
  
-   Proporcionar el número de una partición, por ejemplo: ON PARTITIONS (2).  
  
-   Proporcionar los números de partición de varias particiones separados por comas, por ejemplo: ON PARTITIONS (1, 5).  
  
-   Proporcionar intervalos y particiones individuales: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<intervalo > se puede especificar como números de partición separados por la palabra TO, por ejemplo: ON PARTITIONS (6 a 8).  
  
 Para establecer diferentes tipos de compresión de datos para distintas particiones, especifique la opción DATA_COMPRESSION más de una vez, por ejemplo:  
  
```  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
## <a name="remarks"></a>Comentarios  
 La instrucción CREATE INDEX se optimiza como cualquier otra consulta. Para guardar en operaciones de E/S, el procesador de consultas puede elegir examinar otro índice en lugar de realizar un recorrido de tabla. La operación de orden se puede eliminar en algunos casos. En equipos con varios procesadores, CREATE INDEX puede utilizar más procesadores para realizar las operaciones de examen y orden asociadas a la creación del índice, al igual que hacen otras consultas. Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 La operación de creación de índices se registra al mínimo si el modelo de recuperación de base de datos se establece en Registro masivo o Sencillo.  
  
 Los índices se pueden crear en una tabla temporal. Cuando se quita la tabla o finaliza la sesión, se quitan los índices.  
  
 Los índices admiten propiedades extendidas.  
  
## <a name="clustered-indexes"></a>Índices clúster  
 La creación de un índice clúster en una tabla (montón) o la eliminación y nueva creación de un índice clúster existente requiere área de espacio adicional disponible en la base de datos para acomodar la ordenación de datos y una copia temporal de la tabla original o datos del índice clúster existente. Para obtener más información acerca de los índices agrupados, consulte [crear índices agrupados](../../relational-databases/indexes/create-clustered-indexes.md).  
  
## <a name="nonclustered-indexes"></a>Índices no clúster  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], puede crear un índice no agrupado en una tabla almacenada como un índice de almacén de columnas agrupado. Si primero crea un índice no agrupado en una tabla almacenada como un índice agrupado o montón, el índice se conservará si más adelante se convierte en la tabla a un índice de almacén de columnas agrupado. Además, no es necesario quitar el índice no clúster cuando se vuelve a generar el índice de almacén de columnas agrupado.  
  
 Limitaciones y restricciones:  
  
-   La opción FILESTREAM_ON no es válida cuando se crea un índice no agrupado en una tabla almacenada como un índice de almacén de columnas agrupado.  
  
## <a name="unique-indexes"></a>Índices únicos  
 Cuando existe un índice único, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba si hay valores duplicados cada vez que se agregan datos con una operación de inserción. Las operaciones de inserción que generarían valores de clave duplicados se revierten y el [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestra un mensaje de error. Esto se cumple incluso si la operación de inserción cambia muchas filas pero crea un único duplicado. Si se intenta indicar datos donde existe un índice único y se ha especificado la cláusula IGNORE_DUP_KEY en ON, solo causarán un error las filas que infrinjan el índice UNIQUE.  
  
## <a name="partitioned-indexes"></a>Índices con particiones  
 La creación y el mantenimiento de los índices con particiones son similares a los de las tablas con particiones pero, al igual que en índices ordinarios, éstos son tratados como objetos de base de datos independientes. Puede tener un índice con particiones en una tabla que carezca de particiones, y puede tener un índice sin particiones en una tabla que tenga particiones.  
  
 Si crea un índice en una tabla con particiones y no especifica un grupo de archivos en el que desea ubicar el índice, se crean particiones en el índice de la misma manera que en la tabla subyacente. Esto se debe a que, de manera predeterminada, los índices se ubican en los mismos grupos de archivos que sus tablas subyacentes, y en una tabla con particiones del mismo esquema de partición que usa las mismas columnas de partición. Cuando el índice usa el mismo esquema de partición y la columna de partición que la tabla, el índice es *alineado* con la tabla.  
  
> [!WARNING]  
>  La creación y regeneración de índices no alineados en una tabla con más de 1.000 particiones es posible, pero no se admite. Si se hace, se puede degradar el rendimiento o consumir excesiva memoria durante estas operaciones. Se recomienda usar solo índices alineados cuando el número de particiones sea superior a 1.000.  
  
 Cuando se crean particiones en un índice clúster no único, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] agrega de forma predeterminada las columnas de partición a la lista de claves del índice clúster, en caso de que no se hubieran especificado aún.  
  
 Se pueden crear vistas indizadas en tablas con particiones de la misma manera que se hace con índices en tablas. Para obtener más información acerca de los índices con particiones, vea [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], las estadísticas no se crean examinando todas las filas de la tabla cuando se crea o se vuelve a generar un índice con particiones. En su lugar, el optimizador de consultas usa el algoritmo de muestreo predeterminado para generar estadísticas. Para obtener estadísticas sobre índices con particiones examinando todas las filas de la tabla, use CREATE STATISTICS o UPDATE STATISTICS con la cláusula FULLSCAN.  
  
## <a name="filtered-indexes"></a>Índices filtrados  
 Un índice filtrado es un índice no clúster optimizado, adecuado para las consultas que seleccionan un porcentaje pequeño de las filas de una tabla. Utiliza un predicado de filtro para indizar una parte de los datos de la tabla. Un índice filtrado bien diseñado puede mejorar el rendimiento de las consultas, reducir los costos de almacenamiento y de mantenimiento.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Opciones SET requeridas para los índices filtrados  
 Las opciones SET de la columna de valor requerido son necesarias siempre que se dé alguna de las condiciones siguientes:  
  
-   Se crea un índice filtrado.  
  
-   La operación INSERT, UPDATE, DELETE o MERGE modifica los datos de un índice filtrado.  
  
-   Se utiliza el índice filtrado por el optimizador de consultas para generar el plan de consulta.  
  
    |Opciones de Set|Valor requerido|Valor de servidor predeterminado|Valor predeterminado<br /><br /> Valor de OLE DB y ODBC|Valor predeterminado<br /><br /> predeterminado|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *Al establecer ANSI_WARNINGS en ON, ARITHABORT se establece de forma implícita en ON cuando el nivel de compatibilidad de base de datos está establecido en 90 o un valor superior. Si el nivel de compatibilidad de la base de datos está establecido en 80 o en un nivel inferior, debe configurarse explícitamente la opción ARITHABORT en ON.  
  
 Si las opciones SET son incorrectas, se pueden producir las condiciones siguientes:  
  
-   El índice filtrado no se crea.  
  
-   El [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y revierte cualquier instrucción INSERT, UPDATE, DELETE o MERGE que cambia los datos del índice.  
  
-   El optimizador de consultas no tiene en cuenta el índice en el plan de ejecución de ninguna instrucción Transact-SQL.  
  
 Para obtener más información acerca de los índices filtrados, vea [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
## <a name="spatial-indexes"></a>Índices espaciales  
 Para obtener información acerca de los índices espaciales, vea [CREATE SPATIAL INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-spatial-index-transact-sql.md) y [información general de los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="xml-indexes"></a>Índices XML  
 Para obtener información acerca de XML índices, vea [CREATE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-xml-index-transact-sql.md) y [XML Indexes &#40; SQL Server &#41; ](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="index-key-size"></a>Tamaño de clave de índice  
 El tamaño máximo de una clave de índice es 900 bytes para un índice agrupado y 1.700 bytes para un índice no agrupado. (Antes [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] el límite siempre era de 900 bytes.) Índices en **varchar** se pueden crear columnas que superen el límite de bytes si los datos existentes en las columnas no superar el límite en el momento en que se crea el índice; sin embargo, posterior acciones de inserción o actualización en las columnas que hacen que el tamaño total debe ser mayor que el límite se producirá un error. La clave de índice de un índice agrupado no puede contener columnas **varchar** con datos existentes en la unidad de asignación ROW_OVERFLOW_DATA. Si se crea un índice agrupado en una columna **varchar** y los datos existentes están en la unidad de asignación IN_ROW_DATA, no se realizarán correctamente las siguientes acciones de inserción o actualización en la columna que intenten insertar los datos de manera no consecutiva.  
  
 Los índices no clúster pueden incluir columnas que no son de clave en el nivel de hoja del índice. Estas columnas no tiene en cuenta el [!INCLUDE[ssDE](../../includes/ssde-md.md)] al calcular el tamaño de clave de índice. Para más información, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
> [!NOTE]  
>  Cuando se dividen las tablas, si las columnas de clave de la partición no están aún presentes en un índice clúster no único, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] las agrega al índice. El tamaño combinado de las columnas indizadas (sin contar las columnas incluidas) más cualquier columna de partición agregada no puede exceder 1800 bytes en un índice clúster no único.  
  
## <a name="computed-columns"></a>Columnas calculadas  
 Los índices se pueden crear en columnas calculadas. Además, las columnas calculadas pueden tener la propiedad PERSISTED. Esto significa que [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena los valores calculados en la tabla y los actualiza cuando se actualiza cualquier otra columna de la que depende la columna calculada. [!INCLUDE[ssDE](../../includes/ssde-md.md)] utiliza estos valores persistentes cuando crea un índice en la columna y cuando se hace referencia al índice en una consulta.  
  
 Para indizar una columna calculada, ésta debe ser determinista y precisa. No obstante, si se usa la propiedad PERSISTED, se amplía el tipo de columnas calculadas indizables para incluir:  
  
-   Las columnas calculadas basadas en [!INCLUDE[tsql](../../includes/tsql-md.md)], funciones CLR y métodos de tipos definidos por el usuario CLR que el usuario ha marcado como deterministas.  
  
-   Las columnas calculadas basadas en expresiones que son deterministas, como se definen en [!INCLUDE[ssDE](../../includes/ssde-md.md)], aunque imprecisas.  
  
 Las columnas calculadas persistentes requieren que se establezcan las siguientes opciones SET de la manera indicada en la sección anterior, "Opciones SET requeridas para vistas indizadas".  
  
 Las restricciones UNIQUE o PRIMARY KEY pueden contener una columna calculada siempre que cumplan con todas las condiciones de creación del índice. En concreto, la columna calculada debe ser determinista y precisa, o determinista y persistente. Para obtener más información acerca del determinismo, vea [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
 Las columnas calculadas derivadas de **imagen**, **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, y **xml** pueden ser tipos de datos como una columna sin clave incluida o de clave indizar siempre que el tipo de datos de columna calculada esté disponible como una columna de clave de índice o columna sin clave. Por ejemplo, no se puede crear un índice XML principal en una calculada **xml** columna. Si el tamaño de clave de índice supera los 900 bytes, se muestra un mensaje de advertencia.  
  
 La creación de un índice en una columna calculada puede producir un error en una operación de inserción o actualización que antes funcionaba. Este error podría ocurrir cuando la columna calculada produce un error aritmético. Por ejemplo, aunque la columna calculada `c` de la tabla siguiente produzca un error aritmético, la instrucción `INSERT` funcionará.  
  
```  
CREATE TABLE t1 (a int, b int, c AS a/b);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 En cambio, si después de crear la tabla crea un índice en la columna calculada `c`, la misma instrucción `INSERT` producirá un error.  
  
```  
CREATE TABLE t1 (a int, b int, c AS a/b);  
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 Para obtener más información, vea [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
## <a name="included-columns-in-indexes"></a>Columnas incluidas en índices  
 Las columnas que no son de clave, denominadas columnas incluidas, se pueden agregar en el nivel hoja de un índice no clúster para mejorar el rendimiento de las consultas al cubrir la consulta. Es decir, todas las columnas a las que se hace referencia en la consulta se incluyen en el índice como columnas de clave o que no son de clave. De este modo, el optimizador de consultas puede ubicar toda la información requerida con un examen del índice; no se tiene acceso a los datos de la tabla o del índice clúster. Para más información, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
## <a name="specifying-index-options"></a>Especificar opciones de índice  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] incluye opciones de índice nuevas y también modifica el modo en que se especifican las opciones. En la sintaxis compatible con versiones anteriores, WITH *option_name* es equivalente a WITH **(** \<option_name >  **=**  ON **)**. Al establecer opciones de índice, se aplican las siguientes reglas: 
  
-   Nuevas opciones de índice solo pueden especificarse mediante WITH **(***option_name*  **=**  ON | DESACTIVAR**)**.  
  
-   Las opciones no se pueden especificar utilizando la sintaxis compatible con versiones anteriores y la nueva sintaxis en la misma instrucción. Por ejemplo, si se especifica WITH **(**DROP_EXISTING**,** en línea  **=**  ON**)** provoca un error en la instrucción.  
  
-   Cuando se crea un índice XML, se deben especificar las opciones mediante WITH **(***option_name*  **=**  ON | DESACTIVAR**)**.  
  
## <a name="dropexisting-clause"></a>Cláusula DROP_EXISTING  
 Puede utilizar la cláusula DROP_EXISTING para volver a generar el índice, agregar o quitar columnas, modificar opciones, modificar el criterio de ordenación de las columnas o cambiar el grupo de archivos o el esquema de partición.  
  
 Si el índice exige una restricción PRIMARY KEY o UNIQUE, y la definición de índice no se ha modificado en absoluto, se quita el índice y se vuelve a crear conservando la restricción existente. Sin embargo, si se ha modificado la definición de índice, se genera un error en la instrucción. Para cambiar la definición de una restricción PRIMARY KEY o UNIQUE, quite la restricción y agregue una restricción con la nueva definición.  
  
 DROP_EXISTING mejora el rendimiento cuando se vuelve a crear un índice clúster (con el mismo conjunto de claves o con uno distinto) en una tabla que también tiene índices no clúster. DROP_EXISTING reemplaza la ejecución de una instrucción DROP INDEX en el antiguo índice clúster seguida de la ejecución de una instrucción CREATE INDEX para el nuevo índice clúster. Los índices no clúster se vuelven a generar una vez, siempre que la definición de índice haya cambiado. La cláusula DROP_EXISTING no vuelve a generar los índices no clúster cuando la definición de índice posee los mismos nombres de índice, clave y columnas de partición, atributo de unicidad y criterio de ordenación que el índice original.  
  
 Independientemente de si se vuelven a generar o no los índices no clúster, éstos siempre permanecen en sus esquemas de partición o grupos de archivos originales, y utilizan las funciones de partición originales. Si un índice clúster se vuelve a generar en un esquema de partición o grupo de archivos diferente, los índices no clúster no se mueven para coincidir con la nueva ubicación del índice clúster. Por lo tanto, es posible que incluso los índices no clúster alineados previamente con el índice clúster no se puedan alinear con éste. Para obtener más información sobre la alineación de índices con particiones, vea.  
  
 La cláusula DROP_EXISTING no volverá a ordenar los datos si se utilizan las mismas columnas de clave de índice en el mismo orden y con la misma disposición ascendente o descendente, a menos que la instrucción del índice especifique un índice no clúster y la opción ONLINE se establezca en OFF. Si se deshabilita el índice clúster, se debe establecer ONLINE en OFF para la operación CREATE INDEX WITH DROP_EXISTING. Si se deshabilita un índice no clúster y no se asocia con un índice clúster deshabilitado, se puede establecer ONLINE en OFF u ON para la operación CREATE INDEX WITH DROP_EXISTING.  
  
 Cuando se quitan o se vuelven a generar índices con 128 o más extensiones, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] aplaza las cancelaciones de asignación de página reales y los bloqueos asociados, hasta después de que se confirme la transacción.  
  
## <a name="online-option"></a>Opción ONLINE  
 Las directrices siguientes se aplican para el desarrollo de operaciones de índice en línea:  
  
-   La tabla subyacente no se podrá alterar, truncar ni quitar mientras haya una operación de índice en línea en curso.  
  
-   La operación de índice requiere un espacio en disco temporal adicional.  
  
-   Las operaciones en línea se pueden realizar en índices con particiones e índices que contienen columnas calculadas persistentes, o columnas incluidas.  
  
 Para más información, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
## <a name="row-and-page-locks-options"></a>Opciones de bloqueo de fila y página  
 Si ALLOW_ROW_LOCKS = ON y ALLOW_PAGE_LOCK = ON, se permiten los bloqueos de nivel de fila, página y tabla cuando se tiene acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] elige el bloqueo apropiado y puede cambiar de escala el bloqueo: de un bloqueo de fila o página a un bloqueo de tabla.  
  
 Si ALLOW_ROW_LOCKS = OFF y ALLOW_PAGE_LOCK = OFF, solo se permiten los bloqueos de nivel de tabla cuando se tiene acceso al índice.  
  
## <a name="viewing-index-information"></a>Ver información de índice  
 Para devolver información sobre índices, puede utilizar vistas de catálogo, funciones del sistema y procedimientos almacenados del sistema.  
  
## <a name="data-compression"></a>Data Compression  
 Compresión de datos se describe en el tema [compresión de datos](../../relational-databases/data-compression/data-compression.md). A continuación se muestran los puntos clave que se deben tener en cuenta:  
  
-   La compresión puede permitir que se almacenen más filas en una página, pero no cambia el tamaño máximo de la fila.  
  
-   Las páginas no hoja de un índice no tienen compresión de página pero pueden tener compresión de fila.  
  
-   Cada índice no clúster tiene una configuración de compresión individual y no hereda la configuración de compresión de la tabla subyacente.  
  
-   Cuando se crea un índice clúster en un montón, el índice clúster hereda el estado de compresión del montón, a menos que se especifique otro estado de compresión.  
  
 Las restricciones siguientes se aplican a los índices con particiones:  
  
-   No se puede cambiar la configuración de compresión de una partición única si la tabla tiene índices no alineados.  
  
-   La instrucción ALTER INDEX \<índice >... REBUILD PARTITION ... vuelve a generar la partición especificada del índice.  
  
-   La instrucción ALTER INDEX \<índice >... REBUILD WITH ... vuelve a generar todas las particiones del índice.  
  
 Para evaluar cómo afecta el cambio del estado de compresión a una tabla, índice o partición, use el procedimiento almacenado [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) .  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en la tabla o la vista. El usuario debe ser miembro del rol fijo de servidor **sysadmin** o de los roles fijos de base de datos **db_ddladmin** y **db_owner** .  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], no se puede crear:  
  
-   Un índice agrupado o no agrupado de almacén de filas en una tabla de almacenamiento de datos cuando ya existe un índice de almacén de columnas. Este comportamiento es diferente de SMP de SQL Server que permite a los índices de almacén de filas y columnstore coexistir en la misma tabla.  
  
-   No se puede crear un índice en una vista.  
  
## <a name="metadata"></a>Metadatos  
 Para ver información acerca de los índices existentes, puede consultar el [sys.indexes &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.  
  
## <a name="version-notes"></a>Notas de la versión  
 Base de datos SQL no admite opciones de grupo de archivos y filestream.  
  
## <a name="examples-all-versions-uses-the-adventureworks-database"></a>Ejemplos: Todas las versiones. Utiliza la base de datos de AdventureWorks.  
  
### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>A. Crear un índice no clúster de almacén de filas sencillos  
 Los ejemplos siguientes crean un índice no agrupado en el `VendorID` columna de la `Purchasing.ProductVendor` tabla.  
  
```  
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. Crear un índice compuesto no clúster de almacén de filas sencillos  
 En el ejemplo siguiente se crea un índice compuesto no clúster en el `SalesQuota` y `SalesYTD` columnas de la `Sales.SalesPerson` tabla.  
  
```  
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);  
```  
  
### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. Crear un índice en una tabla en otra base de datos  
 En el ejemplo siguiente se crea un índice no agrupado en el `VendorID` columna de la `ProductVendor` tabla el `Purchasing` base de datos.  
  
```  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);   
```  
  
### <a name="d-add-a-column-to-an-index"></a>D. Agregar una columna a un índice  
 En el ejemplo siguiente se crea el índice IX_FF con dos columnas de la tabla dbo. Tabla FactFinance.  La instrucción siguiente vuelve a generar el índice con una columna más y mantiene el nombre existente.  
  
```  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey ASC, DateKey ASC );  
  
--Rebuild and add the OrganizationKey  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey, DateKey, OrganizationKey DESC)  
WITH ( DROP_EXISTING = ON );  
 ```  
  
## <a name="examples-sql-server-azure-sql-database"></a>Ejemplos: SQL Server, base de datos SQL Azure  
  
### <a name="e-create-a-unique-nonclustered-index"></a>E. Crear un índice no clúster único  
 En el ejemplo siguiente se crea un índice no clúster único en la columna `Name` de la tabla `Production.UnitMeasure` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. El índice exigirá unicidad en los datos insertados en la columna `Name`.  
  
```  
CREATE UNIQUE INDEX AK_UnitMeasure_Name   
    ON Production.UnitMeasure(Name);  
```  
  
 La consulta siguiente prueba la restricción de unicidad intentando insertar una fila con el mismo valor que el de una fila existente.  
  
```  
--Verify the existing value.  
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';  
GO  
INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)  
    VALUES ('OC', 'Ounces', GetDate());  
```  
  
 El mensaje de error resultante es:  
  
```  
Server: Msg 2601, Level 14, State 1, Line 1  
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.  
```  
  
### <a name="f-use-the-ignoredupkey-option"></a>F. Use la opción IGNORE_DUP_KEY  
 El ejemplo siguiente muestra el efecto de la opción `IGNORE_DUP_KEY` al insertar varias filas en una tabla temporal primero con la opción establecida en `ON` y luego con la opción establecida en `OFF`. Se inserta una única fila en la tabla `#Test` que intencionadamente proporcionará un valor duplicado cuando se ejecuta la segunda instrucción `INSERT` de varias filas. Un recuento de las filas de la tabla devuelve el número de filas insertadas.  
  
```  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = ON);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 A continuación se muestran los resultados de la segunda instrucción `INSERT`.  
  
```  
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.  
  
Number of rows   
--------------   
38  
```  
  
 Observe que las filas insertadas desde la tabla `Production.UnitMeasure` que no infringieron la restricción de unicidad se insertaron correctamente. Se emitió una advertencia y se omitió la fila duplicada, pero no se revirtió la transacción completa.  
  
 Las mismas instrucciones se ejecutan nuevamente, pero con `IGNORE_DUP_KEY` establecido en `OFF`.  
  
```  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = OFF);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 A continuación se muestran los resultados de la segunda instrucción `INSERT`.  
  
```  
Server: Msg 2601, Level 14, State 1, Line 5  
Cannot insert duplicate key row in object '#Test' with unique index  
'AK_Index'. The statement has been terminated.  
  
Number of rows   
--------------   
1  
```  
  
 Observe que ninguna de las filas de la tabla `Production.UnitMeasure` se insertó en la tabla aunque solo una fila de la tabla infringió la restricción de índice `UNIQUE`.  
  
### <a name="g-using-dropexisting-to-drop-and-re-create-an-index"></a>G. Usar DROP_EXISTING para quitar y volver a crear un índice  
 En el ejemplo siguiente se quita y se vuelve a crear un índice existente en la columna `ProductID` de la tabla `Production.WorkOrder` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] utilizando la opción `DROP_EXISTING`. También se establecen las opciones `FILLFACTOR` y `PAD_INDEX` .  
  
```  
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID  
    ON Production.WorkOrder(ProductID)  
    WITH (FILLFACTOR = 80,  
        PAD_INDEX = ON,  
        DROP_EXISTING = ON);  
GO  
  
```  
  
### <a name="h-create-an-index-on-a-view"></a>H. Crear un índice en una vista  
 Este ejemplo siguiente crea una vista y un índice en esa vista. Se incluyen dos consultas que utilizan la vista indizada.  
  
```  
--Set the options to support indexed views.  
SET NUMERIC_ROUNDABORT OFF;  
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
    QUOTED_IDENTIFIER, ANSI_NULLS ON;  
GO  
--Create view with schemabinding.  
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
DROP VIEW Sales.vOrders ;  
GO  
CREATE VIEW Sales.vOrders  
WITH SCHEMABINDING  
AS  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
        OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
    FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
    WHERE od.SalesOrderID = o.SalesOrderID  
    GROUP BY OrderDate, ProductID;  
GO  
--Create an index on the view.  
CREATE UNIQUE CLUSTERED INDEX IDX_V1   
    ON Sales.vOrders (OrderDate, ProductID);  
GO  
--This query can use the indexed view even though the view is   
--not specified in the FROM clause.  
SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
    OrderDate, ProductID  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND ProductID BETWEEN 700 and 800  
        AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
GROUP BY OrderDate, ProductID  
ORDER BY Rev DESC;  
GO  
--This query can use the above indexed view.  
SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND DATEPART(mm,OrderDate)= 3  
        AND DATEPART(yy,OrderDate) = 2002  
GROUP BY OrderDate  
ORDER BY OrderDate ASC;  
GO  
  
```  
  
### <a name="i-create-an-index-with-included-non-key-columns"></a>I. Crear un índice con columnas (sin clave) incluidas  
 El ejemplo siguiente crea un índice no clúster con una columna de clave (`PostalCode`) y cuatro columnas que no son de clave (`AddressLine1`, `AddressLine2`, `City`, `StateProvinceID`). A continuación se presenta una consulta cubierta por el índice. Para mostrar el índice seleccionado por el optimizador de consultas, en la **consulta** menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione **mostrar Plan de ejecución real** antes de ejecutar la consulta.  
  
```  
CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
GO  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
GO  
```  
  
### <a name="j-create-a-partitioned-index"></a>J. Crear un índice con particiones  
 En el ejemplo siguiente se crea un índice no clúster con particiones en `TransactionsPS1`, un esquema de partición existente en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. En este ejemplo se supone que se ha instalado el ejemplo de índice con particiones.  
  
**Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID  
    ON Production.TransactionHistory (ReferenceOrderID)  
    ON TransactionsPS1 (TransactionDate);  
GO  
```  
  
### <a name="k-creating-a-filtered-index"></a>K. Crear un índice filtrado  
 En el ejemplo siguiente se crea un índice filtrado en la tabla Production.BillOfMaterials de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. El predicado de filtro puede incluir columnas que no son columnas de clave en el índice filtrado. El predicado de este ejemplo selecciona solo las filas en que EndDate no es NULL.  
  
```  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
### <a name="l-create-a-compressed-index"></a>L. Crear un índice comprimido  
 En el ejemplo siguiente se crea un índice en una tabla sin particiones utilizando la compresión de fila.  
  
```  
CREATE NONCLUSTERED INDEX IX_INDEX_1   
    ON T1 (C2)  
WITH ( DATA_COMPRESSION = ROW ) ;   
GO  
```  
  
 En el ejemplo siguiente se crea un índice en una tabla con particiones utilizando la compresión de fila en todas las particiones del índice.  
  
```  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH ( DATA_COMPRESSION = ROW ) ;  
GO  
```  
  
 En el ejemplo siguiente se crea un índice en una tabla con particiones utilizando la compresión de página en la partición `1` del índice y la compresión de fila en las particiones `2` a `4` del índice.  
  
```  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1),  
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4 ) ) ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="m-basic-syntax"></a>M. Sintaxis básica  
  
```  
CREATE INDEX IX_VendorID   
    ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID   
    ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID   
    ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="n-create-a-non-clustered-index-on-a-table-in-the-current-database"></a>N. Crear un índice no agrupado en una tabla en la base de datos actual  
 En el ejemplo siguiente se crea un índice no agrupado en el `VendorID` columna de la `ProductVendor` tabla.  
  
```  
CREATE INDEX IX_ProductVendor_VendorID   
    ON ProductVendor (VendorID);   
```  
  
### <a name="o-create-a-clustered-index-on-a-table-in-another-database"></a>O. Crear un índice agrupado en una tabla en otra base de datos  
 En el ejemplo siguiente se crea un índice no agrupado en el `VendorID` columna de la `ProductVendor` tabla el `Purchasing` base de datos.  
  
```  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID   
    ON Purchasing..ProductVendor (VendorID);   
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [Crear índice espacial &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Crear índice XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Sys.xml_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 

