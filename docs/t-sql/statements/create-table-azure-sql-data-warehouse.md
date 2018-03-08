---
title: Crear tabla (almacenamiento de datos SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 07/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f6e639bf97ed132b6ace7128b4cbe9b6f3ce474e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-azure-sql-data-warehouse"></a>Crear tabla (almacenamiento de datos SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Crea una nueva tabla en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 
Para entender las tablas y cómo utilizarlas, vea [tablas en el almacén de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/).

Nota: Las discusiones sobre almacenamiento de datos de SQL en este artículo aplican para almacenamiento de datos SQL y almacenamiento de datos paralelos a menos que se indique lo contrario. 
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>   
## <a name="syntax"></a>Sintaxis  
  
```  
-- Create a new table. 
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]   
    )  
    [ WITH [ <table_option> [ ,...n ] ) ]  
[;]  
   
<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ [ CONSTRAINT constraint_name ] DEFAULT constant_expression  ]
  
<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC 
    }  
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN -- default for SQL Data Warehouse
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }   
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )  
  
<data type> ::=   
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to SQL Data Warehouse 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to SQL Data Warehouse  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to SQL Data Warehouse  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>   
## <a name="arguments"></a>Argumentos  
 *database_name*  
 El nombre de la base de datos que contendrá la nueva tabla. El valor predeterminado es la base de datos actual.  
  
 *schema_name*  
 El esquema para la tabla. Especificar *esquema* es opcional. Si está en blanco, se utilizará el esquema predeterminado.  
  
 *table_name*  
 El nombre de la nueva tabla. Para crear una tabla temporal local, anteponga al nombre de tabla con #.  Para obtener explicaciones y directrices en las tablas temporales, vea [tablas temporales en el almacén de datos de SQL Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/). 
 
 *column_name*  
 El nombre de una columna de tabla.
   
### <a name="ColumnOptions"></a>Opciones de columna

 `COLLATE` *Windows_collation_name*  
 Especifica la intercalación de la expresión. La intercalación debe ser una de las intercalaciones de Windows compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de intercalaciones de Windows admitidas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [nombre de intercalación de Windows (Transact-SQL)](http://msdn.microsoft.com/library/ms188046\(v=sql11\)/).  
  
 `NULL` | `NOT NULL`  
 Especifica si `NULL` se permiten valores en la columna. El valor predeterminado es `NULL`.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 Especifica el valor de columna predeterminado.  
  
 | Argumento | Explicación |
 | -------- | ----------- |
 | *constraint_name* | El nombre opcional para la restricción. El nombre de la restricción es único dentro de la base de datos. El nombre puede ser volver a usar en otras bases de datos. |
 | *constant_expression* | El valor predeterminado para la columna. La expresión debe ser un valor literal o una constante. Por ejemplo, se permiten estas expresiones constantes: `'CA'`, `4`. No se permiten estas: `2+3`, `CURRENT_TIMESTAMP`. |
  

### <a name="TableOptions"></a>Opciones de la estructura de tabla
Para obtener instrucciones sobre cómo elegir el tipo de tabla, vea [la indización de tablas en el almacén de datos de SQL Azure](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/).
  
 `CLUSTERED COLUMNSTORE INDEX`  
Almacena la tabla como un índice de almacén de columnas agrupado. El índice de almacén de columnas agrupado se aplica a todos los datos de tablas. Este es el valor predeterminado para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 
 `HEAP`   
  Almacena la tabla como un montón. Este es el valor predeterminado para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 `CLUSTERED INDEX`( *index_column_name* [,...*n* ] )  
 Almacena la tabla como un índice clúster con una o varias columnas de clave. Almacena los datos por fila. Use *index_column_name* para especificar el nombre de una o varias columnas de clave en el índice.  Para obtener más información, vea las tablas de almacén de filas en la sección de comentarios generales.
 
 `LOCATION = USER_DB`   
 Esta opción está en desuso. Se acepta sintácticamente, pero ya no es necesaria y ya no afecta al comportamiento.   
  
### <a name="TableDistributionOptions"></a>Opciones de distribución de la tabla
Para entender cómo elegir el mejor método de distribución y utilizar tablas distribuidas, vea [distribuir tablas en el almacén de datos de SQL Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/).

`DISTRIBUTION = HASH`( *distribution_column_name* )   
Asigna cada fila a una distribución aplicando un algoritmo hash al valor almacenado en *distribution_column_name*. El algoritmo es determinista, lo que significa que siempre genera un valor hash el mismo valor para la misma distribución.  La columna de distribución debe definirse como NOT NULL desde todas las filas que tengan NULL se asigna a la misma distribución.

`DISTRIBUTION = ROUND_ROBIN`   
Distribuye uniformemente las filas a través de todas las distribuciones de un modo round robin. Este es el valor predeterminado para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].

`DISTRIBUTION = REPLICATE`    
Almacena una copia de la tabla en cada nodo de ejecución. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] en la tabla se almacena en una base de datos de distribución en cada nodo de ejecución. Para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], la tabla se almacena en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grupo de archivos que abarca el nodo de proceso. Este es el valor predeterminado para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
### <a name="TablePartitionOptions"></a>Opciones de partición de tabla
Para obtener instrucciones sobre el uso de particiones de tabla, vea [crear particiones de tablas en el almacén de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/).

 `PARTITION`( *partition_column_name* `RANGE` [ `LEFT`  |  `RIGHT` ] `FOR VALUES` ([ *boundary_value* [,...*n*] ] ))   
Crea una o varias particiones de tabla. Se trata de segmentos de tabla horizontales que permiten realizar operaciones en los subconjuntos de filas, independientemente de si la tabla se almacena como un montón, el índice clúster o el índice de almacén de columnas agrupado. A diferencia de la columna de distribución, las particiones de tabla no determinan la distribución donde se almacena cada fila. En su lugar, las particiones de tabla determinan cómo se agrupan y se almacenan en cada distribución de las filas.  
 
| Argumento | Explicación |
| -------- | ----------- |
|*partition_column_name*| Especifica la columna que [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] va a usar para las filas de la partición. Esta columna puede ser cualquier tipo de datos. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]Ordena los valores de columna de partición en orden ascendente. El orden de bajo a alto va de `LEFT` a `RIGHT` para el propósito de la `RANGE` especificación. |  
| `RANGE LEFT` | Especifica que el valor de límite pertenece a la partición de la izquierda (valores más bajos). El valor predeterminado es LEFT. |
| `RANGE RIGHT` | Especifica que el valor de límite pertenece a la partición de la derecha (valores más altos). | 
| `FOR VALUES`( *boundary_value* [,...*n*] ) | Especifica los valores de límite para la partición. *boundary_value* es una expresión constante. No puede ser NULL. Debe coincidir o ser implícitamente convertible al tipo de datos de *partition_column_name*. No se puede truncar durante la conversión implícita para que el tamaño y la escala del valor no coincide con el tipo de datos de *partition_column_name*<br></br><br></br>Si especifica la `PARTITION` cláusula, pero no especifica un valor de límite, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] creará una tabla con particiones con una partición. Si procede, que una división de la tabla en dos particiones en un momento posterior.<br></br><br></br>Si especifica un valor de límite, la tabla resultante tiene dos particiones; uno de los valores menores que el valor de límite y uno de los valores superiores al valor de límite. Tenga en cuenta que si se mueve una partición a una tabla sin particiones, la tabla sin particiones recibirá los datos, pero no tendrá los límites de partición en sus metadatos.| 
 
 Vea [crear una tabla con particiones](#PartitionedTable) en la sección ejemplos.

### <a name="DataTypes"></a>Tipos de datos
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]admite el uso más común tipos de datos. A continuación se muestra una lista de los tipos de datos admitidos junto con sus detalles y los bytes de almacenamiento. Para entender mejor los tipos de datos y cómo utilizarlas, vea [ tipos de datos de tablas en el almacén de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types).

Para una tabla de conversiones de tipos de datos, vea la sección conversiones implícitas de [CAST y CONVERT (Transact-SQL)](http://msdn.microsoft.com/library/ms187928/).

`datetimeoffset` [ ( *n* ) ]  
 El valor predeterminado de  *n*  es 7.  
  
 `datetime2` [ ( *n* ) ]  
Igual que `datetime`, salvo que puede especificar el número de fracciones de segundo. El valor predeterminado de  *n*  es `7`.  
  
|*n*valor|Precisión|Escala|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 Almacena la fecha y hora del día con 19 y 23 caracteres según el calendario gregoriano. Puede contener la fecha de año, mes y día. La hora contiene la hora, minutos y segundos. Como opción, puede mostrar tres dígitos de fracciones de segundo. El tamaño de almacenamiento es de 8 bytes.  
  
 `smalldatetime`  
 Almacena una fecha y una hora. Tamaño de almacenamiento es de 4 bytes.  
  
 `date`  
 Almacena una fecha con un máximo de 10 caracteres para año, mes y día según el calendario gregoriano. El tamaño de almacenamiento es de 3 bytes. Fecha se almacena como un entero.  
  
 `time` [ ( *n* ) ]  
 El valor predeterminado de  *n*  es `7`.  
  
 `float` [ ( *n* ) ]  
 Tipo de datos de número aproximados para su uso con datos numéricos de punto flotante. Datos de punto flotante es aproximado, lo que significa que no todos los valores del intervalo del tipo de datos se pueden representar exactamente. *n*Especifica el número de bits que se usa para almacenar la mantisa de la `float` en notación científica. Por lo tanto,  *n*  dicta el tamaño de almacenamiento y precisión. Si  *n*  se especifica, debe ser un valor entre `1` y `53`. El valor predeterminado de  *n*  es `53`.  
  
| *n*valor | Precisión | Tamaño de almacenamiento |  
| --------: | --------: | -----------: |  
| 1-24   | 7 dígitos  | 4 bytes      |  
| 25-53  | 15 dígitos | 8 bytes      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]trata  *n*  como uno de dos valores posibles. Si `1` <=   *n*   <=  `24`,  *n*  se trata como `24`. Si `25`  <=   *n*   <=  `53`,  *n*  se trata como `53`.  
  
 El [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float` cumple el estándar ISO para todos los valores de tipo de datos  *n*  de `1` a través de `53`. El sinónimo de doble precisión es `float(53)`.  
  
 `real` [ ( *n* ) ]  
 La definición de real es lo mismo que float. El sinónimo de `real` en ISO es `float(24)`.  
  
 `decimal`[( *precisión* [ *, escala* ])] | `numeric` [( *precisión* [ *, escala* ])]  
 Almacena los números de precisión y escala fijos.  
  
 *precisión*  
 El número total máximo de dígitos decimales que se puede almacenar, tanto a la izquierda como a la derecha del separador decimal. La precisión debe estar comprendido entre `1` y la precisión máxima de `38`. La precisión predeterminada es `18`.  
  
 *escala*  
 El número máximo de dígitos decimales que se puede almacenar a la derecha del separador decimal. *Escala* debe estar comprendido entre `0` a través de *precisión*. Solo se puede especificar *escala* si *precisión* se especifica. La escala predeterminada es `0`; por lo tanto, `0`  <=  *escala* <= *precisión*. Los tamaños de almacenamiento máximo varían según la precisión.  
  
| Precisión | Bytes de almacenamiento  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 Tipos de datos que representan los valores de divisa.  
  
| Tipo de datos | Bytes de almacenamiento |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 Tipos de datos numéricos exactos que utilizan datos enteros. El almacenamiento de información se muestra en la tabla siguiente.  
  
| Tipo de datos | Bytes de almacenamiento |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 Tipo de datos entero que puede tomar el valor de `1`, `0`, o ' NULL. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]optimiza el almacenamiento de columnas de tipo bit. Si hay columnas de tipo bit 8 o menos en una tabla, las columnas se almacenan como 1 byte. Si hay entre 9 y 16 bits columnas, las columnas se almacenan como 2 bytes y así sucesivamente.  
  
 `nvarchar`[(  *n*   |  `max` )]: `max` solo se aplica a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Datos de caracteres Unicode de longitud variable. *n*puede ser un valor comprendido entre 1 y 4000. `max` indica que el tamaño máximo de almacenamiento es de 2^31-1 bytes (2 GB). Tamaño de almacenamiento en bytes es dos veces el número de caracteres especificado + 2 bytes. Los datos especificados pueden tener una longitud de 0 caracteres.  
  
 `nchar` [ ( *n* ) ]  
 Datos de caracteres Unicode de longitud fija con una longitud de  *n*  caracteres. *n*debe estar comprendido entre `1` a través de `4000`. El tamaño de almacenamiento es dos veces  *n*  bytes.  
  
 `varchar`[(  *n*    |  `max` )]: `max` solo se aplica a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 Datos de caracteres no Unicode de longitud variable, con una longitud de  *n*  bytes. *n*debe estar comprendido entre `1` a `8000`. `max`indica que el tamaño máximo de almacenamiento es 2 ^ 31-1 bytes (2 GB). El tamaño de almacenamiento es la longitud real de los datos especificados + 2 bytes.  
  
 `char` [ ( *n* ) ]  
 Datos de caracteres no Unicode de longitud fija, con una longitud de  *n*  bytes. *n*debe estar comprendido entre `1` a `8000`. El tamaño de almacenamiento es  *n*  bytes. El valor predeterminado de  *n*  es `1`.  
  
 `varbinary`[(  *n*    |  `max` )]: `max` solo se aplica a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Datos binarios de longitud variable. *n*puede ser un valor de `1` a `8000`. `max` indica que el tamaño máximo de almacenamiento es de 2^31-1 bytes (2 GB). El tamaño de almacenamiento es la longitud real de los datos especificados + 2 bytes. El valor predeterminado de  *n*  es 7.  
  
 `binary` [ ( *n* ) ]  
 Datos binarios de longitud fija con una longitud de  *n*  bytes. *n*puede ser un valor de `1` a `8000`. El tamaño de almacenamiento es  *n*  bytes. El valor predeterminado de  *n*  es `7`.  
  
 `uniqueidentifier`  
 Es un GUID de 16 bytes.  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Permissions  
 Crear una tabla requiere un permiso en el `db_ddladmin` fijo de base de datos, o:
 - `CREATE TABLE`permiso en la base de datos
 - `ALTER SCHEMA`permiso en el esquema que va a contener la tabla. 

Crear una tabla con particiones requiere el permiso en el `db_ddladmin` fijo de base de datos, o

- `ALTER ANY DATASPACE`permiso
  
 El inicio de sesión que crea una tabla temporal local recibe `CONTROL`, `INSERT`, `SELECT`, y `UPDATE` permisos en la tabla.  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>Notas generales  
 
Para los límites mínimo y máximo, consulte [límites de capacidad de almacenamiento de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/). 
 
### <a name="determining-the-number-of-table-partitions"></a>Determinar el número de particiones de tabla
Cada tabla definida por el usuario se divide en varias tablas más pequeñas que se almacenan en ubicaciones independientes llamadas distribuciones. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]usa 60 distribuciones. En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], el número de distribuciones depende del número de nodos de cálculo.
 
Cada distribución contiene todas las particiones de tabla. Por ejemplo, si hay cuatro particiones de tabla y 60 distribuciones, habrá 320 particiones. Si la tabla es un índice de almacén de columnas agrupado, habrá un índice de almacén de columnas por partición, lo que significa que tendrá 320 índices de almacén de columnas.

Se recomienda el uso de menos particiones de tabla para asegurar que cada índice de almacén de columnas tiene suficientes filas para aprovechar las ventajas de los índices de almacén de columnas. Para obtener más información, consulte [crear particiones de tablas en el almacén de datos de SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/) y [la indización de tablas en el almacén de datos de SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)  

  
 ### <a name="rowstore-table-heap-or-clustered-index"></a>Tabla de almacén de filas (índice agrupado o montón)  
 Una tabla de almacén de filas es una tabla almacenada en el orden de fila por fila. Es un índice agrupado o montón. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]crea todas las tablas de almacén de filas con la compresión de página; Esto no es configurable por el usuario.   
 
 ### <a name="columnstore-table-columnstore-index"></a>Tabla de almacén de columnas (índice de almacén de columnas)
Una tabla de almacén de columnas es una tabla almacenada en el orden de columna por columna. El índice de almacén es la tecnología que administra los datos almacenados en una tabla de almacén de columnas.  El índice de almacén de columnas agrupado no afecta a cómo se distribuyen los datos; afecta a cómo se almacenan los datos dentro de cada distribución.

Para cambiar una tabla de almacén de filas a una tabla de almacén de columnas, quite todos los índices existentes en la tabla y crear un índice de almacén de columnas agrupado. Para obtener un ejemplo, vea [CREATE COLUMNSTORE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-columnstore-index-transact-sql.md).

Para más información, vea estos artículos:
- [Resumen de características con control de versiones de los índices de almacén de columnas](https://msdn.microsoft.com/library/dn934994/)
- [La indización de tablas en el almacén de datos de SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)
- [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md) 
 
<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede definir una restricción DEFAULT en una columna de distribución.  
  
 ### <a name="partitions"></a>Particiones
 Al utilizar particiones, la columna de partición no puede tener una intercalación exclusiva de Unicode. Por ejemplo, se produce un error en la siguiente instrucción.  
  
 `CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))`  
 
 Si *boundary_value* es un valor literal que se debe convertir implícitamente al tipo de datos en *partition_column_name*, se producirá una discrepancia. El valor literal que se muestra a través de la [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] vistas del sistema, pero el valor convertido se utiliza para [!INCLUDE[tsql](../../includes/tsql-md.md)] operaciones. 
 
  
 ### <a name="temporary-tables"></a>tablas temporales
 Las tablas temporales globales que comienzan por ## no son compatibles.  
  
 Tablas temporales locales tienen las siguientes limitaciones y restricciones:  
  
-   Son visibles solo en la sesión actual. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]coloca automáticamente al final de la sesión. Para quitar de ellas explicitlt, utilice la instrucción DROP TABLE.   
-   No se pueden cambiar. 
-   No pueden tener particiones o vistas.  
-   No se puede cambiar sus permisos. `GRANT`, `DENY`, y `REVOKE` las instrucciones no se puede usar con tablas temporales locales.   
-   Comandos de la consola de base de datos se bloquean para las tablas temporales.   
-   Si se usa más de una tabla temporal local dentro de un lote, cada uno debe tener un nombre único. Si se ejecuta el mismo lote varias sesiones y se crean la misma tabla temporal local, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] internamente anexa un sufijo numérico al nombre de tabla temporal local para mantener un nombre único para cada tabla temporal local.  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>Comportamiento de bloqueo  
 Toma un bloqueo exclusivo en la tabla. Toma un bloqueo compartido en los objetos de base de datos, esquema y SCHEMARESOLUTION.  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>Ejemplos de columnas

### <a name="ColumnCollation"></a> A. Especificar una intercalación de columna 
 En el ejemplo siguiente, la tabla `MyTable` se crea con dos intercalaciones de columna diferente. De forma predeterminada, la columna, `mycolumn1`, tiene la intercalación predeterminada Latin1_General_100_CI_AS_KS_WS. La columna `mycolumn2` tiene la intercalación Frisian_100_CS_AS.  
  
```  
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
  
```  
  
### <a name="DefaultConstraint"></a> B. Especificar una restricción DEFAULT para una columna  
 En el ejemplo siguiente se muestra la sintaxis para especificar un valor predeterminado para una columna. La columna de la colA tiene una restricción predeterminada denominada constraint_colA y un valor predeterminado de 0.  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>Ejemplos de tablas temporales

### <a name="TemporaryTable"></a> C. Crear una tabla temporal local  
 El ejemplo siguiente crea una tabla temporal local denominada #myTable. La tabla se especifica con un nombre de parte 3. El nombre de tabla temporal empieza por un símbolo #.   
  
```  
CREATE TABLE AdventureWorks.dbo.#myTable   
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```

<a name="ExTableStructure"></a>  
## <a name="examples-for-table-structure"></a>Ejemplos de la estructura de tabla

### <a name="ClusteredColumnstoreIndex"></a> D. Crear una tabla con un índice de almacén de columnas agrupado  
 En el ejemplo siguiente se crea una tabla distribuida con un índice de almacén de columnas agrupado. Cada distribución se almacenará como un almacén de columnas.  
  
 El índice de almacén de columnas agrupado no afecta a cómo se distribuyen los datos; datos siempre se distribuyen por fila. El índice de almacén de columnas agrupado afecta a cómo se almacenan los datos dentro de cada distribución.  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```  
 
<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>Ejemplos para la distribución de la tabla

### <a name="RoundRobin"></a> E. Crear una tabla de ROUND_ROBIN  
 En el ejemplo siguiente se crea una tabla de ROUND_ROBIN con tres columnas y sin particiones. Los datos se reparten entre todas las distribuciones. La tabla se crea con un índice de almacén de columnas en clúster, lo que se consigue un mejor rendimiento y compresión de datos que un índice clúster montón o almacén de filas.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> F. Crear una tabla hash está distribuido  
 En el ejemplo siguiente se crea la misma tabla que el ejemplo anterior. Sin embargo, para esta tabla, que se distribuyen filas (en la `id` columna) en lugar de forma aleatoria se propagan como una tabla de ROUND_ROBIN. La tabla se crea con un índice de almacén de columnas en clúster, lo que se consigue un mejor rendimiento y compresión de datos que un índice clúster montón o almacén de filas.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),   
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a name="Replicated"></a> G. Crear una tabla replicada  
 En el ejemplo siguiente se crea una tabla replicada similar a los ejemplos anteriores. Las tablas replicadas se copian por completo en cada nodo de ejecución. Con esta copia en cada nodo de proceso, se reduce el movimiento de datos para las consultas. En este ejemplo se crea con un índice agrupado, que proporciona una mejor compresión de datos de un montón y no puede contener filas suficientes para lograr buena compresión CLUSTERED COLUMNSTORE INDEX.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,   
    CLUSTERED INDEX (lastName)  
  );  
```  

<a name="ExTablePartitions"></a> 
## <a name="examples-for-table-partitions"></a>Ejemplos de las particiones de tabla

###  <a name="PartitionedTable"></a> H. Crear una tabla con particiones  
 En el ejemplo siguiente se crea la misma tabla, tal como se muestra en el ejemplo A, con la adición de partición RANGE LEFT en la `id` columna. Especifica valores de límite de cuatro particiones, que da como resultado cinco particiones.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
  (   
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX      
  )  
;  
```  
  
 En este ejemplo, se ordenarán los datos en las siguientes particiones:  
  
-   La partición 1: col < = 10   
-   Partición 2:10 < col < = 20   
-   Partición 3:20 < col < = 30   
-   Partición 4:30 < col < = 40   
-   Partición 5:40 < col  
  
 Si esta misma tabla está particionada RANGE RIGHT en lugar de RANGE LEFT (valor predeterminado), los datos se ordenarán en las siguientes particiones:  
  
-   La partición 1: col < 10  
-   Partición 2:10 < = col < 20   
-   Partición 3:20 < = col < 30    
-   Partición 4:30 < = col < 40   
-   Partición 5:40 < = col  
  
### <a name="OnePartition"></a> I. Crear una tabla con particiones con una partición  
 En el ejemplo siguiente se crea una tabla con particiones con una partición. No especifique los valores de límite, que da como resultado una partición.  
  
```  
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
    (   
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a name="DatePartition"></a> J. Crear una tabla con particiones de fecha  
 En el ejemplo siguiente se crea una nueva tabla denominada `myTable`, con la partición en un `date` columna. Al usar RANGE RIGHT y fechas para los valores de límite, coloca un mes de datos de cada partición.  
  
```  
CREATE TABLE myTable (  
    l_orderkey      bigint,       
    l_partkey       bigint,                                             
    l_suppkey       bigint,                                           
    l_linenumber    bigint,        
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH   
  (   
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES   
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
<a name="SeeAlso"></a>    
## <a name="see-also"></a>Vea también 
 
 [Crear tabla como SELECT &#40; Almacenamiento de datos SQL de Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [Eliminar tabla &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
