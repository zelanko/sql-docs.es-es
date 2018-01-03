---
title: "Instrucción ALTER INDEX (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 11/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tsql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER INDEX
- ALTER_INDEX_TSQL
dev_langs: t-sql
helpviewer_keywords:
- indexes [SQL Server], reorganizing
- ALTER INDEX statement
- indexes [SQL Server], disabling
- online index operations
- index reorganization [SQL Server]
- ALLOW_ROW_LOCKS option
- ALL keyword
- reorganizing indexes
- constraints [SQL Server], indexes
- row locks [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- locking [SQL Server], indexes
- partitioned indexes [SQL Server], rebuilding
- defragmenting indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- index modifications [SQL Server]
- indexes [SQL Server], modifying
- index options [SQL Server]
- modifying indexes
- index disabling [SQL Server]
- MAXDOP index option, ALTER INDEX statement
- spatial indexes [SQL Server], modifying
- indexes [SQL Server], options
- ALLOW_PAGE_LOCKS option
- page locks [SQL Server]
- index rebuild [SQL Server]
- index reorganize [SQL Server]
ms.assetid: b796c829-ef3a-405c-a784-48286d4fb2b9
caps.latest.revision: "222"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 48926573b515a1f40fa0db983d846b4e801abfd4
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="alter-index-transact-sql"></a>ALTER INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Modifica un índice existente de una tabla o una vista (relacional o XML) mediante su deshabilitación, regeneración o reorganización, o mediante el establecimiento de sus opciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
ALTER INDEX { index_name | ALL } ON <object>  
{  
      REBUILD {  
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]   
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]  
      }  
    | DISABLE  
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]  
    | SET ( <set_index_option> [ ,...n ] )   
    | RESUME [WITH (<resumable_index_options>,[…n])]
    | PAUSE
    | ABORT
}  
[ ; ]  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<rebuild_index_option > ::=  
{  
      PAD_INDEX = { ON | OFF }  
    | FILLFACTOR = fillfactor   
    | SORT_IN_TEMPDB = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | STATISTICS_INCREMENTAL = { ON | OFF }  
    | ONLINE = {   
          ON [ ( <low_priority_lock_wait> ) ]   
        | OFF } 
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | COMPRESSION_DELAY = {0 | delay [Minutes]}  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }   
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]  
}  
  
<single_partition_rebuild_index_option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | RESUMABLE = { ON | OFF } 
    | MAX_DURATION = <time> [MINUTES}     
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<reorganize_option>::=  
{  
       LOB_COMPACTION = { ON | OFF }  
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}  
}  
  
<set_index_option>::=  
{  
      ALLOW_ROW_LOCKS = { ON | OFF }  
    | ALLOW_PAGE_LOCKS = { ON | OFF }  
    | IGNORE_DUP_KEY = { ON | OFF }  
    | STATISTICS_NORECOMPUTE = { ON | OFF }  
    | COMPRESSION_DELAY= {0 | delay [Minutes]}  
}  

<resumable_index_option> ::=
 { 
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>  
 }
 
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )  
}  

```  
  
```  
-- Syntax for SQL Data Warehouse and Parallel Data Warehouse 
  
ALTER INDEX { index_name | ALL }  
    ON   [ schema_name. ] table_name  
{  
      REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ] 
      }  
    | DISABLE  
    | REORGANIZE [ PARTITION = partition_number ]  
}  
[;]  

<rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_index_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
  
```    
## <a name="arguments"></a>Argumentos  
 *index_name*  
 Es el nombre del índice. Los nombres de índice deben ser únicos en una tabla o vista, pero no es necesario que sean únicos en una base de datos. Los nombres de índice deben seguir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 ALL  
 Especifica todos los índices asociados a la tabla o vista independientemente del tipo de índice. Si se especifica ALL y uno o más índices se encuentran en un grupo de archivos sin conexión o de solo lectura o la operación especificada no está permitida en uno o más tipos de índices, se produce un error en la instrucción. En la siguiente tabla se enumeran las operaciones de índice y los tipos de índices no permitidos.  
  
|Utiliza la palabra clave ALL con esta operación|Se produce un error si la tabla tiene uno o más|  
|----------------------------------------|----------------------------------------|  
|REBUILD WITH ONLINE = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice de almacén de columnas: **se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|REBUILD PARTITION = *número_de_partición*|Índice sin particiones, índice XML, índice espacial o índice deshabilitado|  
|REORGANIZE|Índices que tienen ALLOW_PAGE_LOCKS establecido en OFF|  
|PARTICIÓN REORGANIZAR = *número_de_partición*|Índice sin particiones, índice XML, índice espacial o índice deshabilitado|  
|IGNORE_DUP_KEY = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice de almacén de columnas: **se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|ONLINE = ON|Índice XML<br /><br /> Índice espacial<br /><br /> Índice de almacén de columnas: **se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|
| REANUDABLES = ON  | Índices reanudables no compatibles con **todos los** palabra clave. <br /><br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)] |   
  
> [!WARNING]
>  Para obtener más información sobre las operaciones de índice que se pueden realizar en línea, consulte [directrices para operaciones de índice en línea](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

 Si se especifica ALL con PARTITION = *número_de_partición*, todos los índices deben estar alineados. Esto significa que se crean particiones basadas en las funciones de partición equivalentes. Utiliza ALL con PARTITION hace que todas las particiones de índice con el mismo *número_de_partición* se vuelven a generar u organizar. Para obtener más información acerca de los índices con particiones, vea [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 *database_name*  
 Es el nombre de la base de datos.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la tabla o la vista.  
  
 *nombre_tabla_o_vista*  
 Es el nombre de la tabla o vista asociada al índice. Para mostrar un informe de los índices en un objeto, utilice la [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]admite nombre_basedeDatos de formato de nombre de tres partes. [nombre_esquema]. nombre_tabla_o_vista cuando nombre_basedeDatos es la base de datos actual o nombre_basedeDatos es tempdb y nombre_tabla_o_vista comienza con #.  
  
 Volver a generar [WITH **(**\<rebuild_index_option > [ **,**... *n*]**)** ]  
 Especifica que el índice se volverá a generar con unas columnas, un tipo de índice, un atributo de unicidad y un criterio de ordenación idénticos. Esta cláusula es equivalente a [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md). REBUILD habilita un índice deshabilitado. Cuando se regenera un índice clúster, no se vuelven a generar los índices no clúster asociados, a menos que se especifique la palabra clave ALL. Si no se especifican opciones de índice, el índice existente los valores almacenados en las opciones [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) se aplican. Para las opciones del índice cuyo valor no se almacena en **sys.indexes**, se aplica el valor predeterminado indicado en la definición del argumento de la opción.  
  
 Si se especifica ALL y la tabla base es un montón, la operación de regeneración no tiene ningún efecto sobre la tabla. Se regeneran los índices no clúster asociados a la tabla.  
  
 Si el modelo de recuperación de base de datos está establecido como simple u optimizado para cargas masivas de registros, la operación de regeneración se puede registrar mínimamente.  
  
> [!NOTE]
>  Cuando se regenera un índice XML principal, la tabla de usuario subyacente no está disponible mientras dura esta operación.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Para los índices de almacén de columnas, la operación de regeneración:  
  
1.  No se utiliza el criterio de ordenación.  
  
2.  Adquiere un bloqueo exclusivo en la tabla o la partición mientras se produce la regeneración.  Los datos están desconectados y no disponibles durante la recompilación, aunque se use NOLOCK, RCSI o SI.  
  
3.  Vuelve a comprimir todos los datos del almacén de columnas. Hay dos copias del índice de almacén de columnas mientras se está produciendo la regeneración. Cuando se finaliza la recopilación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimina el índice original del almacén de columnas.  
  
 Para obtener más información acerca de cómo volver a generar índices de almacén de columnas, consulte [la desfragmentación de índices de almacén de columnas:](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
PARTITION  

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica que solamente se va a volver a generar o a reorganizar una partición de un índice. No se puede especificar la partición si *index_name* no es un índice con particiones.  
  
 PARTITION = ALL vuelve a generar todas las particiones.  
  
> [!WARNING]
>  La creación y regeneración de índices no alineados en una tabla con más de 1.000 particiones es posible, pero no se admite. Si se hace, se puede degradar el rendimiento o consumir excesiva memoria durante estas operaciones. Se recomienda usar solo índices alineados cuando el número de particiones sea superior a 1.000.  
  
 *número_de_partición*  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Es el número de partición de un índice con particiones que se va a volver a generar o a reorganizar. *número_de_partición* es una expresión constante que puede hacer referencia a variables. Estas incluyen variables o funciones de tipo definido por el usuario y funciones definidas por el usuario, pero no pueden hacer referencia a una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *número_de_partición* debe existir o se produce un error en la instrucción.  
  
 CON **(**\<single_partition_rebuild_index_option >**)**  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 SORT_IN_TEMPDB, MAXDOP y DATA_COMPRESSION son las opciones que se pueden especificar cuando se vuelve a generar una sola partición (partición =  *n* ). No es posible especificar índices XML en una operación para volver a generar una partición única.  
  
 DISABLE  
 Marca el índice como deshabilitado y no disponible para el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cualquier índice puede estar deshabilitado. La definición de índice de un índice deshabilitado se conserva en el catálogo del sistema sin datos del índice subyacente. La deshabilitación de un índice clúster evita que los usuarios obtengan acceso a los datos de la tabla subyacente. Para habilitar un índice, utilice ALTER INDEX REBUILD o CREATE INDEX WITH DROP_EXISTING. Para obtener más información, consulte [deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md) y [habilitar índices y restricciones](../../relational-databases/indexes/enable-indexes-and-constraints.md).  
  
 REORGANIZAR un índice de almacén de filas  
 Para los índices de almacén de filas, REORGANIZE especifica para reorganizar el nivel de hoja del índice.  La operación de REORGANIZACIÓN es:  
  
-   Siempre se realiza en línea. Esto significa que los bloqueos de tabla a largo plazo no se mantienen y que las consultas o actualizaciones en la tabla subyacente pueden continuar durante la transacción ALTER INDEX REORGANIZE.  
  
-   No se permite para un índice deshabilitado  
  
-   No se permite cuando ALLOW_PAGE_LOCKS está establecido en OFF  
  
-   No se revierte cuando se realiza dentro de una transacción y se revierte la transacción.  
  
REORGANIZE CON **(** LOB_COMPACTION = { **ON** | {OFF} **)**  
 Se aplica a los índices de almacén de filas.  
  
LOB_COMPACTION = ON  
  
-   Especifica que se debe compactar todas las páginas que contienen datos de estos tipos de datos de objetos grandes (LOB): imagen, texto, ntext, varchar (max), nvarchar (max), varbinary (max) y xml. Compactar estos datos puede reducir el tamaño de los datos en disco.  
  
-   Para un índice agrupado, se compactan todas las columnas LOB que figuran en la tabla.  
  
-   Para un índice no agrupado, esto compacta todas las columnas LOB que son columnas (incluidas) en el índice.  
  
-   REORGANIZAR todo realiza LOB_COMPACTION en todos los índices. Para cada índice, se compactan todas las columnas LOB en el índice agrupado, la tabla subyacente o las columnas incluidas en un índice no agrupado.  
  
LOB_COMPACTION = OFF  
  
-   Las páginas que contienen datos de objetos grandes no se compactan.  
  
-   OFF no tiene ningún efecto sobre un montón.  
  
REORGANIZAR un índice de almacén de columnas  
REORGANIZACIÓN se realiza en línea.  
  
Para los índices de almacén de columnas, REORGANIZAR comprime cada grupo de filas delta cerrados en el almacén de columnas como un grupo de filas comprimido.  
  
-   REORGANIZE no es necesario para mover grupos de filas delta cerrados en grupos de filas comprimidos. El proceso de motor de tupla (TM) de fondo se activa periódicamente para comprimir los grupos de filas delta cerrado. Se recomienda usar REORGANIZE al motor de tupla se retrasa. REORGANIZE puede comprimir grupos de filas de una forma más agresiva.  
  
-   Para comprimir todos los grupos de filas abierto y cerrado, vea la opción REORGANIZE con (COMPRESS_ALL_ROW_GROUPS) en esta sección.  
  
Para los índices de almacén de columnas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2016) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)], REORGANIZE realiza las siguientes optimizaciones adicionales de desfragmentación:  
  
-   Quita físicamente las filas de un grupo de filas al 10% o más de las filas se han eliminado lógicamente. Los bytes eliminados se reclaman en los medios físicos. Por ejemplo, si un grupo de filas comprimidos de 1 millón de filas tiene filas de 100 KB eliminadas, SQL Server quita las filas eliminadas y volver a comprimir el grupo de filas con 900 filas k. Guarda en el almacenamiento mediante la eliminación de filas eliminadas.  
  
-   Combina uno o varios grupos de filas comprimidos para aumentar las filas por grupo, hasta el máximo de 1,024,576 filas. Por ejemplo, si importa de forma masiva 5 procesos por lotes de 102.400 filas obtendrá 5 grupos de filas comprimidos. Si ejecuta REORGANIZE, obtener combinará estos grupos de filas en 1 grupo de filas comprimido de 512.000 filas de tamaño. Se supone que no había ningún diccionario limitaciones de tamaño o de memoria.  
  
-   Grupos de filas en el que el 10% o más de las filas se han eliminado lógicamente, SQL Server intentará combinar este grupo de filas con uno o varios grupos de filas.    Por ejemplo, 1 del grupo de filas se comprimió con 500.000 filas y 21 de grupo de filas se comprimió con el máximo de 1.048.576 filas.  21 de grupo de filas tiene 60% de las filas eliminadas que deja 409,830 filas. SQL Server, se favorece combinar estos dos grupos de filas para comprimir un nuevo grupo de filas que tiene 909,830 filas.  
  
REORGANIZAR CON (COMPRESS_ALL_ROW_GROUPS = {ON | **OFF** })  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2016) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)], el COMPRESS_ALL_ROW_GROUPS proporciona una manera de obligar a los grupos de filas delta abierto o cerrado en el almacén de columnas. Con esta opción, no es necesario volver a generar el índice de almacén de columnas para vaciar los grupos de filas delta.  Esto, combinado con lo otro remove y mezcla desfragmentación características hace que ya no es necesario volver a generar el índice en la mayoría de los casos.    
-   ON obliga a todos los grupos de filas en el almacén de columnas, independientemente del tamaño y el estado (cerrados o abiertos).  
  
-   DESACTIVAR obliga a todos los grupos de filas CLOSED en el almacén de columnas.  
  
ESTABLECER **(** \<set_index opción > [ **,**... *n*] **)**  
 Especifica las opciones del índice sin volver a generar ni organizar el índice. No es posible especificar SET para un índice deshabilitado.  
  
PAD_INDEX = { ON | OFF }  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica el relleno del índice. El valor predeterminado es OFF.  
  
 ON  
 El porcentaje de espacio disponible especificado por FILLFACTOR se aplica a páginas de nivel intermedio del índice. Si no se especifica FILLFACTOR al mismo tiempo que PAD_INDEX se establece en ON, el valor almacenado en de factor de relleno [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) se utiliza.  
  
 DESACTIVAR o *fillfactor* no se ha especificado  
 Las páginas de nivel intermedio se rellenan casi al máximo. Esto deja suficiente espacio para al menos una fila del tamaño máximo que puede tener el índice, según el conjunto de claves de las páginas intermedias.  
  
 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
Valor de FILLFACTOR = *fillfactor*  
 
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Especifica un porcentaje que indica cuánto debe llenar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] el nivel hoja de cada página de índice durante la creación o modificación de los índices. *valor de FILLFACTOR* debe ser un valor entero entre 1 y 100. El valor predeterminado es 0. Los valores de fill factor 0 y 100 son idénticos.  
  
 Un valor FILLFACTOR explícito solo se aplica la primera vez que se crea o se vuelve a generar el índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mantiene dinámicamente el porcentaje especificado de espacio disponible de las páginas. Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 Para ver el valor de factor de relleno, use **sys.indexes**.  
  
> [!IMPORTANT]
>  La creación o modificación de un índice clúster con un valor FILLFACTOR afecta a la cantidad de espacio de almacenamiento que ocupan los datos, dado que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] vuelve a distribuir los datos cuando crea el índice clúster.  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica si se deben almacenar los resultados de ordenación en **tempdb**. El valor predeterminado es OFF.  
  
 ON  
 Los resultados de orden intermedio que se usan para generar el índice se almacenan en **tempdb**. Si **tempdb** está en un conjunto de discos que en la base de datos de usuario diferente, esto puede reducir el tiempo necesario para crear un índice. Sin embargo, esto aumenta la cantidad de espacio en disco utilizado durante la generación del índice.  
  
 OFF  
 Los resultados de orden intermedios se almacenan en la misma base de datos que el índice.  
  
 Si no se necesita una operación de ordenación o si la ordenación se puede realizar en la memoria, se omite la opción SORT_IN_TEMPDB.  
  
 Para obtener más información, consulte [opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY  **=**  {ON | {OFF}  
 Especifica la respuesta de error cuando una operación de inserción intenta insertar valores de clave duplicados en un índice único. La opción IGNORE_DUP_KEY se aplica solamente a operaciones de inserción realizadas tras crear o volver a generar el índice. El valor predeterminado es OFF.  
  
 ON  
 Se producirá un mensaje de advertencia cuando se inserten valores de clave duplicados en un índice único. Solo las filas que infrinjan la restricción de unicidad darán error.  
  
 OFF  
 Se producirá un mensaje de error cuando se inserten valores de clave duplicados en un índice único. Toda la operación INSERT se revertirá.  
  
 No se puede establecer IGNORE_DUP_KEY en ON para los índices creados en una vista, índices no únicos, los índices XML, índices espaciales y los índices filtrados.  
  
 Para ver IGNORE_DUP_KEY, utilice [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 En la sintaxis compatible con versiones anteriores, WITH IGNORE_DUP_KEY es equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | {OFF}  
 Especifica si se vuelven a calcular las estadísticas de distribución. El valor predeterminado es OFF.  
  
 ON  
 Las estadísticas obsoletas no se vuelven a calcular automáticamente.  
  
 OFF  
 Se habilita la actualización automática de las estadísticas.  
  
 Para restaurar la actualización automática de estadísticas, establezca STATISTICS_NORECOMPUTE en OFF o ejecute UPDATE STATISTICS sin la cláusula NORECOMPUTE.  
  
> [!IMPORTANT]
> La deshabilitación del cálculo automático de estadísticas de distribución puede impedir que el optimizador de consultas elija los planes de ejecución óptimos para las consultas relativas a la tabla.  
  
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
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 En línea  **=**  {ON | **OFF** } \<tal como se aplica a rebuild_index_option >  
 Especifica si las tablas subyacentes y los índices asociados están disponibles para realizar consultas y modificar datos durante la operación de índice. El valor predeterminado es OFF.  
  
 Para un índice XML o un índice espacial, solo se admite ONLINE = OFF y, si ONLINE se establece en ON, se produce un error.  
  
> [!NOTE]
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de características que son compatibles con las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [ediciones y características admitidas en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ON  
 Los bloqueos de tabla de larga duración no se mantienen durante la operación de indización. Durante la fase principal de la operación de índice, solo se mantiene un bloqueo preventivo en la tabla de origen. De esta forma, las consultas o actualizaciones realizadas en la tabla y los índices subyacentes pueden continuar. Al principio de la operación, se mantiene un bloqueo compartido (S) sobre el objeto de origen durante un breve período. Al final de la operación, durante un breve período, se adquiere un bloqueo S sobre el origen si se está creando un índice no clúster; o se adquiere un bloqueo SCH-M (modificación del esquema) cuando se crea o se quita un índice clúster en línea o cuando se regenera un índice clúster o no clúster. ONLINE no se puede establecer en ON cuando se crea un índice en una tabla temporal local.  
  
 OFF  
 Los bloqueos de tabla se aplican durante la operación de índice. Una operación de índice sin conexión que crea, vuelve a generar o quita un índice clúster, un índice espacial o un índice XML, o vuelve a generar o quita un índice no clúster, adquiere un bloqueo de modificación del esquema (Sch-M) en la tabla. Esto evita que todos los usuarios tengan acceso a la tabla subyacente durante la operación. Una operación de índice sin conexión que crea un índice no clúster adquiere un bloqueo compartido (S) en la tabla. Esto evita que se realicen actualizaciones en la tabla subyacente, pero permite la realización de operaciones de lectura, como instrucciones SELECT.  
  
 Para obtener más información, consulte [cómo funcionan de las operaciones de índice en línea](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Los índices, incluidos los índices de las tablas temp globales, se pueden volver a generar en línea, con las excepciones siguientes:  
  
-   índices XML  
  
-   Índices en tablas temp locales  
  
-   Un subconjunto de un índice con particiones (un índice entero con particiones se puede regenerar en línea).  

-  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]antes de V12 y SQL Server anteriores a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], no permiten la `ONLINE` opción de generación de índice en clúster o volver a generar las operaciones cuando la tabla base contiene **varchar (max)** o **varbinary (max)** columnas.

REANUDABLES  **=**  {ON | **OFF**}

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

 Especifica si una operación de índice en línea es reanudable.

 En un índice en la operación es reanudable.

 DESACTIVAR el índice de la operación no es reanudable.

MAX_DURATION  **=**  *tiempo* [**minutos**] usa con **REANUDABLE = ON** (requiere **ONLINE = ON**).
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Indica el tiempo (valor entero especificado en minutos) que un reanudables en línea operación de índice se ejecuta antes de que se está en pausa. 

ALLOW_ROW_LOCKS  **=**  { **ON** | {OFF}  
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica si se permiten los bloqueos de fila. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de fila se admiten al obtener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila.  
  
 OFF  
 No se usan los bloqueos de fila.  
  
ALLOW_PAGE_LOCKS  **=**  { **ON** | {OFF}  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Especifica si se permiten bloqueos de página. El valor predeterminado es ON.  
  
 ON  
 Se permiten bloqueos de página cuando se tiene acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página.  
  
 OFF  
 No se utilizan bloqueos de página.  
  
> [!NOTE]
>  No es posible reorganizar un índice cuando ALLOW_PAGE_LOCKS está establecido en OFF.  
  
 MAXDOP  **=**  max_degree_of_parallelism  
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Invalida el **grado máximo de paralelismo** opción de configuración para la duración de la operación de índice. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
> [!IMPORTANT]
>  Aunque la opción MAXDOP se admite sintácticamente para todos los índices XML, ALTER INDEX utiliza en la actualidad un solo procesador para un índice espacial o un índice XML principal.  
  
 *max_degree_of_parallelism* puede ser:  
  
 1  
 Suprime la generación de planes paralelos.  
  
 \>1  
 Restringe el número máximo de procesadores utilizados en una operación de índice paralelo para el número especificado.  
  
 0 (predeterminado)  
 Usa el número real de procesadores o menos, según la carga de trabajo actual del sistema.  
  
 Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]
> Operaciones de índice en paralelo no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de características que son compatibles con las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [ediciones y características admitidas en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 COMPRESSION_DELAY  **=**  { **0** |*duración [minutos]* }  
 Esta característica está disponible a partir con[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
 Para una tabla basada en disco, retraso especifica el número mínimo de minutos que debe permanecer un grupo de filas delta en estado cerrado en el grupo de filas delta antes de que SQL Server puede comprimir en el grupo de filas comprimido. Puesto que las tablas basadas en disco no realizar el seguimiento de insertar y actualizar horas en filas individuales, SQL Server aplica el retraso a grupos de filas delta en estado cerrado.  
El valor predeterminado es 0 minutos.  
  
 El valor predeterminado es 0 minutos.  
  
 Para obtener recomendaciones sobre cuándo usar COMPRESSION_DELAY, vea índices de almacén de columnas para análisis operativos en tiempo real.  
  
 DATA_COMPRESSION  
 Especifica la opción de compresión de datos para el índice, número de partición o intervalo de particiones especificado. Las opciones son las siguientes:  
  
 Ninguno  
 No se comprimen el índice ni las particiones especificadas. Esto no se aplica a los índices de almacén de columnas.  
  
 ROW  
 El índice o las particiones especificadas se comprimen mediante la compresión de fila. Esto no se aplica a los índices de almacén de columnas.  
  
 PAGE  
 El índice o las particiones especificadas se comprimen mediante la compresión de página. Esto no se aplica a los índices de almacén de columnas.  
  
 COLUMNSTORE  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Solo se aplica a los índices de almacén de columnas, incluidos los clúster y no clúster. COLUMNSTORE especifica que se descomprima el índice o las particiones especificadas comprimidas con la opción COLUMNSTORE_ARCHIVE. Cuando se restablecen los datos, seguirán estando comprimidos con la compresión de almacén de columnas que se usa para todos los índices de almacén de columnas.  
  
 COLUMNSTORE_ARCHIVE  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Solo se aplica a los índices de almacén de columnas, incluidos los clúster y no clúster. COLUMNSTORE_ARCHIVE comprimirá aún más la partición especificada a un tamaño mínimo. Esto se puede usar para el archivado o para otras situaciones que requieran un tamaño de almacenamiento mínimo y pueda permitirse más tiempo para el almacenamiento y recuperación.  
  
 Para obtener más información acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
 EN las particiones **(** { \<partition_number_expression > | \<intervalo >} [**,**... n] **)**  
    
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. 
  
 Especifica las particiones a las que se aplica el valor DATA_COMPRESSION. Si el índice no tiene particiones, el argumento ON PARTITIONS generará un error. Si no se proporciona la cláusula ON PARTITIONS, la opción DATA_COMPRESSION se aplica a todas las particiones de un índice con particiones.  
  
 \<partition_number_expression > se puede especificar de las maneras siguientes:  
  
-   Proporcionar el número de una partición, por ejemplo: ON PARTITIONS (2).  
  
-   Proporcionar los números de partición de varias particiones separados por comas, por ejemplo: ON PARTITIONS (1, 5).  
  
-   Proporcione ambos rangos y particiones individuales: ON PARTITIONS (2, 4, 6 y 8).  
  
 \<intervalo > se puede especificar como números de partición separados por la palabra TO, por ejemplo: ON PARTITIONS (6 a 8).  
  
 Para establecer diferentes tipos de compresión de datos para distintas particiones, especifique la opción DATA_COMPRESSION más de una vez, por ejemplo:  
  
```sql  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
 En línea  **=**  {ON | **OFF** } \<tal como se aplica a single_partition_rebuild_index_option >  
 Especifica si se puede regenerar un índice o una partición de índice de una tabla subyacente en línea o sin conexión. Si **volver a generar** se realiza en línea (**ON**) los datos en esta tabla están disponibles para las consultas y modificar datos durante la operación de índice.  El valor predeterminado es **OFF**.  
  
 ON  
 Los bloqueos de tabla de larga duración no se mantienen durante la operación de indización. Durante la fase principal de la operación de índice, solo se mantiene un bloqueo preventivo en la tabla de origen. Se requiere un bloqueo S en la tabla en el inicio de la regeneración de índice y un bloqueo Sch-M en la tabla al final de la regeneración de índices en línea. Aunque ambos bloqueos son bloqueos de metadatos cortos, especialmente el bloqueo Sch-M debe esperar a que todas las transacciones de bloqueo se completen. Durante el tiempo de espera, bloqueo Sch-M bloquea las demás transacciones que esperen a este bloqueo al tener acceso a la misma tabla.  
  
> [!NOTE]
>  La reconstrucción de índices en línea puede establecer el *low_priority_lock_wait* opciones descritas más adelante en esta sección.  
  
 OFF  
 Los bloqueos de tabla se aplican durante la operación de índice. Esto evita que todos los usuarios tengan acceso a la tabla subyacente durante la operación.  
  
 Utilizar WAIT_AT_LOW_PRIORITY con **ONLINE = ON** solo.  
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Una recompilación de índices en línea tiene que esperar a las operaciones de bloqueo en esta tabla. **WAIT_AT_LOW_PRIORITY** indica que la operación de regeneración de índice en línea esperará bloqueos de prioridad baja, lo que permite a otras operaciones podrán continuar mientras está esperando la operación de generación de índice en línea. Si se omite la **WAIT AT LOW PRIORITY** opción es equivalente a `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. Para obtener más información, consulte [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md). 
  
 MAX_DURATION = *tiempo* [**minutos**]  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 El tiempo de espera (valor entero especificado en minutos) que esperarán con prioridad baja los bloqueos de la operación de recompilación de índices en línea cuando se ejecuta el comando DDL. Si la operación se bloquea durante la **MAX_DURATION** tiempo, uno de los **ABORT_AFTER_WAIT** acciones se ejecutarán. **MAX_DURATION** hora es siempre en minutos y la palabra **minutos** puede omitirse.  
 
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOQUEADORES** }]  
   
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 Ninguno  
 Se continúa esperando al bloqueo con prioridad normal.  
  
 SELF  
 Cierra la operación DDL de regeneración del índice en línea que se está ejecutando actualmente sin realizar ninguna acción.  
  
 BLOCKERS  
 Elimine todas las transacciones de usuario que bloqueen la operación DDL de regeneración de índice en línea de forma que la operación pueda continuar. El **BLOQUEADORES** opción requiere el inicio de sesión tenga **ALTER ANY CONNECTION** permiso.  
 
 RESUME 
 
**Se aplica a**: a partir de[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]  

Reanudar una operación de índice que se pausó manualmente o debido a un error.

MAX_DURATION se utiliza con **REANUDABLE = ON**

 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)]

La hora (un valor entero especificado en minutos) se ejecuta después de que se va a reanudar la operación de índice en línea reanudables. Una vez que expire el tiempo, la operación reanudable está en pausa si todavía se está ejecutando.

Utilizar WAIT_AT_LOW_PRIORITY con **REANUDABLE = ON** y **ONLINE = ON**.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
 Reanudar una regeneración de índice en línea después de una pausa tiene que esperar para operaciones de bloqueo en esta tabla. **WAIT_AT_LOW_PRIORITY** indica que la operación de regeneración de índice en línea esperará bloqueos de prioridad baja, lo que permite a otras operaciones podrán continuar mientras está esperando la operación de generación de índice en línea. Si se omite la **WAIT AT LOW PRIORITY** opción es equivalente a `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. Para obtener más información, consulte [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md). 


PAUSE
 
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 
  
Pausar una operación de regeneración del índice en línea reanudables.

ANULACIÓN

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

Anular una operación de índice en pausa o en ejecución que se ha declarado como reanudable. Tendrá que ejecutar explícitamente un **anular** operación de regeneración de un índice reanudable cancelación del comando. Error o interrumpir una operación de índice reanudables no termina su ejecución; en su lugar, la operación deja en un estado de pausa indefinido.
  
## <a name="remarks"></a>Comentarios  
 No es posible utilizar ALTER INDEX para volver a crear particiones en un índice o moverlo a un grupo de archivos distinto. No se puede usar esta instrucción para modificar la definición de índice; por ejemplo, para agregar o eliminar columnas o cambiar su orden. Utilice CREATE INDEX con la cláusula DROP_EXISTING para realizar estas operaciones.  
  
 Cuando no se especifica una opción de forma explícita, se aplica el valor actual. Por ejemplo, si no se especifica un valor FILLFACTOR en la cláusula REBUILD, se utilizará el valor de factor de relleno almacenado en el catálogo del sistema durante el proceso de regeneración. Para ver la configuración de opción de índice actual, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
> [!NOTE]
> Los valores de ONLINE, MAXDOP y SORT_IN_TEMPDB no se almacenan en el catálogo del sistema. A menos que se especifiquen en la instrucción de índice, se utiliza el valor predeterminado de la opción.
  
 En los equipos con varios procesadores, ALTER INDEX REBUILD, al igual que otras consultas, utiliza automáticamente más procesadores para realizar las operaciones de examen y orden asociadas a la modificación del índice. Al ejecutar ALTER INDEX REORGANIZE, con o sin LOB_COMPACTION, el **grado máximo de paralelismo** valor será una operación de subproceso única. Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 No es posible volver a organizar o generar un índice si el grupo de archivos en el que se encuentra está sin conexión o está definido como de solo lectura. Cuando se especifica la palabra clave ALL y hay uno o más índices en un grupo de archivos sin conexión o de solo lectura, se produce un error en la instrucción.  
  
## <a name="rebuilding-indexes"></a>Volver a generar índices  
 El proceso de volver a crear un índice quita y vuelve a crear el índice. Quita la fragmentación, utiliza espacio en disco al compactar las páginas según el valor de factor de relleno especificado o existente y vuelve a ordenar las filas del índice en páginas contiguas. Cuando se especifica ALL, todos los índices de la tabla se quitan y se vuelven a generar en una única transacción. No es necesario quitar las restricciones FOREIGN KEY por adelantado. Cuando se regeneran índices con 128 extensiones o más, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] difiere las cancelaciones de asignación de página y sus bloqueos asociados hasta después de la confirmación de la transacción.  
  
 Con frecuencia, cuando se vuelven a generar o se reorganizan los índices pequeños no se reduce la fragmentación. Las páginas de índices pequeños a veces se almacenan en extensiones mixtas. Las extensiones mixtas pueden estar compartidas por hasta ocho objetos, de modo que es posible que no se pueda reducir la fragmentación en un índice pequeño después de reorganizar o volver a generar dicho índice.  
  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], las estadísticas no se crean examinando todas las filas de la tabla cuando se crea o se vuelve a generar un índice con particiones. En su lugar, el optimizador de consultas usa el algoritmo de muestreo predeterminado para generar estadísticas. Para obtener estadísticas sobre índices con particiones examinando todas las filas de la tabla, use CREATE STATISTICS o UPDATE STATISTICS con la cláusula FULLSCAN.  
  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a veces se podía volver a generar un índice no clúster para corregir incoherencias provocadas por errores de hardware. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, aún es posible reparar estas incoherencias entre el índice y el índice clúster al volver a generar un índice no clúster sin conexión. Sin embargo, no es posible reparar las incoherencias de índices no clúster mediante la regeneración del índice en línea, ya que el mecanismo de regeneración con conexión usará el índice no clúster existente como base para la regeneración y, por tanto, persistirá la incoherencia. La regeneración del índice sin conexión hará que se examine el índice clúster (o montón) y eliminará la incoherencia. Para garantizar una regeneración del índice clúster, quite y vuelva a crear el índice no agrupado. Al igual que en las versiones anteriores, para recuperar incoherencias se recomienda restaurar los datos afectados desde una copia de seguridad. No obstante, es posible que pueda reparar las incoherencias del índice mediante la regeneración del índice no clúster sin conexión. Para obtener más información, vea [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
 Para volver a generar un índice de almacén de columnas clúster, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Adquiere un bloqueo exclusivo en la tabla o la partición mientras se produce la regeneración. Los datos están “sin conexión” y no disponibles durante la regeneración.  
  
2.  Desfragmenta el almacén de columnas físicamente eliminando filas que se han eliminado lógicamente de la tabla; los bytes eliminados se reclaman en los medios físicos.  
  
3.  Lee todos los datos del índice original de almacén de columnas, incluido el almacén delta. Combina los datos en grupos de filas nuevos y comprime los grupos de filas en el almacén de columnas.  
  
4.  Necesita espacio en los medios físicos para almacenar dos copias del índice de almacén de columnas mientras está teniendo lugar la regeneración. Cuando finaliza la regeneración, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimina el índice clúster de almacén de columnas original.  
  
## <a name="reorganizing-indexes"></a>Reorganizar índices  
 La reorganización de un índice usa muy pocos recursos del sistema. Desfragmenta el nivel hoja de los índices agrupados y no clúster de las tablas y las vistas al volver a ordenar físicamente las páginas de nivel hoja para que coincidan con el orden lógico de los nodos hoja, de izquierda a derecha. La reorganización también compacta las páginas de índice. La compactación se basa en el valor de factor de relleno existente. Para ver el valor de factor de relleno, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Cuando se especifica ALL, se reorganizan los índices relacionales, tanto agrupados como no clúster, y los índices XML. Cuando se especifica ALL, se aplican algunas restricciones; vea la definición de ALL en la sección Argumentos.  
  
 Para obtener más información, vea [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## <a name="disabling-indexes"></a>Deshabilitar índices  
 Al deshabilitar un índice, se impide que el usuario tenga acceso al mismo y, en el caso de los índices clúster, a los datos de la tabla subyacente. La definición de índice permanece en el catálogo del sistema. La deshabilitación de un índice no clúster o agrupado en una vista elimina físicamente los datos del índice. La deshabilitación de un índice clúster evita el acceso a los datos, aunque éstos permanecen en el árbol b hasta que el índice se quita o se vuelve a generar. Para ver el estado de un índice habilitado o deshabilitado, consulte el **is_disabled** columna en el **sys.indexes** vista de catálogo.  
  
 Si una tabla se encuentra en una publicación de replicación transaccional, no puede deshabilitar ningún índice que esté asociado con las columnas de clave principal. Estos índices son necesarios para la replicación. Para deshabilitar un índice, primero debe quitar la tabla de la publicación. Para obtener más información sobre la creación de publicaciones, vea [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Utilice la instrucción ALTER INDEX REBUILD o CREATE INDEX WITH DROP_EXISTING para habilitar el índice. No es posible volver a generar un índice clúster deshabilitado si la opción ONLINE está establecida en ON. Para obtener más información, vea [Deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
## <a name="setting-options"></a>Configurar opciones  
 Es posible establecer las opciones ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, IGNORE_DUP_KEY y STATISTICS_NORECOMPUTE de un índice especificado sin volver a generar u organizar ese índice. Los valores modificados se aplican inmediatamente al índice. Para ver esta configuración, use **sys.indexes**. Para obtener más información, consulte [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md).  
  
### <a name="row-and-page-locks-options"></a>Opciones de bloqueo de fila y página  
 Si ALLOW_ROW_LOCKS = ON y ALLOW_PAGE_LOCK = ON, se permiten los bloqueos de nivel de fila, página y tabla cuando se obtiene acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] elige el bloqueo apropiado y puede cambiar de escala el bloqueo: de un bloqueo de fila o página a un bloqueo de tabla.  
  
 Si ALLOW_ROW_LOCKS = OFF y ALLOW_PAGE_LOCK = OFF, solo se permiten los bloqueos de nivel de tabla cuando se tiene acceso al índice.  
  
 Si se especifica ALL al establecer las opciones de bloqueo de fila o página, la configuración se aplica a todos los índices. Cuando la tabla subyacente es un montón, la configuración se aplica de las siguientes formas:  
  
|||  
|-|-|  
|ALLOW_ROW_LOCKS = ON u OFF|Al montón y a cualquier índice no clúster asociado.|  
|ALLOW_PAGE_LOCKS = ON|Al montón y a cualquier índice no clúster asociado.|  
|ALLOW_PAGE_LOCKS = OFF|Completamente a los índices no clúster. Esto significa que no se permite ningún bloqueo de página en los índices no clúster. En el montón, los únicos bloqueos no permitidos para la página son los bloqueos compartidos (S), de actualización (U) y exclusivos (X). El [!INCLUDE[ssDE](../../includes/ssde-md.md)] aún puede adquirir un bloqueo de página de intención (IS, IU o IX) por motivos internos.|  
  
## <a name="online-index-operations"></a>Operaciones de índice en línea  
 Cuando se vuelve a generar un índice y la opción ONLINE está establecida en ON, los objetos subyacentes, las tablas y los índices asociados están disponibles para las consultas y la modificación de datos. También puede regenerar en línea una parte de un índice que resida en una sola partición. Los bloqueos de tabla exclusivos solo se mantienen un espacio de tiempo muy reducido durante el proceso de modificación.  
  
 La reorganización de un índice siempre se realiza en línea. El proceso no mantiene bloqueos a largo plazo y, por ello, no bloquea las consultas o las actualizaciones en ejecución.  
  
 Únicamente se pueden realizar operaciones de índice simultáneas en línea en la misma tabla o partición de tabla si se hace lo siguiente:  
  
-   Crear varios índices no clúster.  
-   Reorganizar diferentes índices en la misma tabla.  
-   Reorganizar diferentes índices mientras se vuelven a generar índices que no se superponen en la misma tabla.  
  
 Se producirá un error en todas las operaciones de índice en línea que se realizan al mismo momento. Por ejemplo, no es posible volver a generar dos o más índices en la misma tabla de forma simultánea ni crear un índice nuevo mientras se regenera un índice existente en la misma tabla.  

### <a name="resumable-indexes"></a>Operaciones de índice reanudables

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

ONLINE INDEX REBUILD se especifica como reanudables mediante el REANUDABLE = opción. 
-  La opción REANUDABLE no se conserva en los metadatos de un índice dado y solo se aplica a la duración de una instrucción DDL actual.  Por lo tanto, el REANUDABLE = ON cláusula debe especificarse explícitamente para habilitar resumability.
-  Tenga en cuenta dos opciones MAX_DURATION diferentes. Uno está relacionado con low_priority_lock_wait y el otro está relacionado con REANUDABLE = opción.
   -  Opción de MAX_DURATION es compatible con REANUDABLE = opción o **low_priority_lock_wait** opción de argumento. 
   -  MAX_DURATION para REANUDABLE opción especifica el intervalo de tiempo para un índice que se va a volver a generar. Una vez que se usa esta hora se pausó la reconstrucción de índices o se completa su ejecución. Usuario decide si se puede reanudar una recompilación de un índice en pausa. El **tiempo** en minutos para MAX_DURATION debe ser mayor que 0 minutos y menor o igual una semana (7 * 24 * 60 = 10080 minutos). Tener una pausa larga para una operación de índice puede afectar al rendimiento de DML en una tabla específica, así como la capacidad de disco de base de datos dado que ambos índices original y uno recién creado requieren espacio en disco y tenga que actualizarse durante las operaciones de DML. Si se omite la opción de MAX_DURATION, la operación de índice continuará hasta su finalización o hasta que se produce un error. 
-   El \<low_priority_lock_wait > argumento opción permite al usuario decidir cómo puede continuar la operación de índice cuando se bloquea en el bloqueo SCH-M.
 
-  Volver a ejecutar la instrucción ALTER INDEX REBUILD original con los mismos parámetros reanuda una operación de regeneración del índice en pausa. También puede reanudar una operación de regeneración del índice en pausa mediante la ejecución de la instrucción ALTER INDEX REANUDAR.
-  La opción SORT_IN_TEMPDB = ON no se admite la opción de índice reanudable 
-  El comando DDL con REANUDABLE = ON no se puede ejecutar dentro de una transacción explícita (no pueden formar parte de begin tran... bloque de confirmación).
-  Solo las operaciones de índice en pausa son reanudables.
-  Cuando se reanuda una operación de índice que está en pausa, puede cambiar el valor MAXDOP a un nuevo valor.  Si MAXDOP no se especifica cuando se reanuda una operación de índice que está en pausa, se toma el último valor MAXDOP. Si la opción MAXDOP no se especifica en absoluto para la operación de regeneración de índice, se toma el valor predeterminado.
- Para pausar inmediatamente la operación de índice, puede detener el comando en curso (Ctrl-C) o puede ejecutar el comando ALTER INDEX pausar o ejecute la instrucción KILL *session_id* comando. Una vez que el comando está en pausa se puede reanudar mediante la opción de reanudación.
-  El comando de anulación elimina la sesión que hospedan la regeneración de índice original y anula la operación de índice  
-  No hay recursos adicionales son necesarios para la reconstrucción de índices reanudables excepto para
   -    Espacio adicional necesario para mantener el índice que se está generando, incluido el tiempo cuando está en pausa índice
   -    Un estado DDL evitando cualquier modificación de DDL
-  La limpieza de registros fantasma se ejecutará durante la fase de pausa de índice, pero se pondrá en pausa durante la ejecución de índice   
La siguiente funcionalidad está deshabilitada para las operaciones de regeneración de índice reanudables
   -    Volver a generar un índice que está deshabilitado no es compatible con REANUDABLE = ON
   -    Comando ALTER INDEX REBUILD ALL
   -    ALTER TABLE con la reconstrucción de índices  
   -    Comando DDL con "RESUMEABLE = ON" no se puede ejecutar dentro de una transacción explícita (no pueden formar parte de begin tran... bloque de confirmación)
   -    Volver a generar un índice que tiene calculadas o columnas de marca de tiempo como columnas de clave.
-   En caso de la tabla base contiene columnas LOB reanudables en clúster regeneración de índice requiere un bloqueo Sch-M en el inicio de esta operación
   -    La opción SORT_IN_TEMPDB = ON no se admite la opción de índice reanudable 

> [!NOTE]
> El comando DDL se ejecuta hasta que se complete, pausa o se produce un error. En caso de que el comando pausa, se emitirá un error que indica que se pausó la operación y que no se completó la creación del índice. Para obtener más información sobre el estado actual del índice puede obtenerse de [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md). Como antes si se produce un error error se emitirán así. 

 Para más información, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
 ### <a name="waitatlowpriority-with-online-index-operations"></a>WAIT_AT_LOW_PRIORITY con operaciones de índice en línea  
  
 Para ejecutar la instrucción DDL para regenerar el índice en línea, todas las transacciones activas de bloqueo que se ejecutan en una tabla determinada deben completarse. Cuando la regeneración de índice en línea se ejecuta, bloquea todas las nuevas transacciones que están listas para iniciar la ejecución en esta tabla. Aunque la vigencia del bloqueo para volver a generar el índice en línea es muy corta, si se espera a que las transacciones abiertas en una tabla dada se completen y se bloquean las nuevas transacciones que se inician, se podría afectar significativamente al rendimiento, produciendo un retraso o un tiempo de espera en la carga de trabajo y se limitaría mucho el acceso a la tabla base. El **WAIT_AT_LOW_PRIORITY** opción permite al DBA para administrar bloqueos S-lock y Sch-M necesarios para el índice en línea se vuelve a generar y les permite seleccionar uno de los 3 opciones. En todos los casos de 3, si durante el tiempo de espera ( `(MAX_DURATION = n [minutes])` ), existen actividades de bloqueo, la regeneración de índices en línea se ejecuta inmediatamente sin esperar y se completa la instrucción DDL.  
  
## <a name="spatial-index-restrictions"></a>Restricciones de los índices espaciales  
 Cuando se regenera un índice espacial, la tabla de usuario subyacente no está disponible mientras dura esta operación, porque el índice espacial tiene un bloqueo del esquema.  
  
 No se puede modificar la restricción PRIMARY KEY de la tabla de usuario mientras se define un índice espacial en una columna de esa tabla. Para cambiar la restricción PRIMARY KEY, quite primero todos los índices espaciales de la tabla. Después de modificar la restricción PRIMARY KEY, puede volver a crear cada uno de los índices espaciales.  
  
 No se puede especificar ningún índice espacial en una operación para volver a generar una partición única. Sin embargo, se pueden especificar índices espaciales cuando se regeneran todas las particiones.  
  
 Para cambiar opciones específicas de un índice espacial, como BOUNDING_BOX o GRID, puede usar una instrucción CREATE SPATIAL INDEX que especifica DROP_EXISTING = ON, o quitar el índice espacial y crear uno nuevo. Para ver un ejemplo, consulte [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
## <a name="data-compression"></a>Data Compression  
 Para obtener más información sobre la compresión de datos, vea [Compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
 Para evaluar cómo afecta el cambio compresión de página y de fila a una tabla, un índice o una partición, use la [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) procedimiento almacenado.  
  
Las restricciones siguientes se aplican a los índices con particiones:  
  
-   Cuando se utiliza `ALTER INDEX ALL ...`, no se puede cambiar la configuración de compresión de una partición única si la tabla tiene índices no alineados.  
-   La instrucción ALTER INDEX \<índice >... REBUILD PARTITION ... vuelve a generar la partición especificada del índice.  
-   La instrucción ALTER INDEX \<índice >... REBUILD WITH ... vuelve a generar todas las particiones del índice.  
  
## <a name="statistics"></a>Estadísticas  
 Cuando se ejecuta **ALTER INDEX ALL...** en una tabla, solo las estadísticas asociadas con los índices se actualizan. Las estadísticas automáticas o manuales creadas en la tabla (en lugar de en un índice) no se actualizan.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar ALTER INDEX, se necesita, como mínimo, el permiso ALTER en la tabla o en la vista.  
  
## <a name="version-notes"></a>Notas de la versión  
  
-  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]no utiliza las opciones de grupo de archivos y filestream.  
-  Índices de almacén de columnas no están disponibles versiones anteriores a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. 
-  Operaciones de índices reanudables están disponibles a partir [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] y[!INCLUDE[ssSDS](../../includes/sssds-md.md)]   
  
## <a name="basic-syntax-example"></a>Ejemplo de sintaxis básica:   
  
```sql 
ALTER INDEX index1 ON table1 REBUILD;  
  
ALTER INDEX ALL ON table1 REBUILD;  
  
ALTER INDEX ALL ON dbo.table1 REBUILD;  
```

## <a name="examples-columnstore-indexes"></a>Ejemplos: Índices de almacén de columnas  
 Estos ejemplos se aplican a los índices de almacén de columnas.  
  
### <a name="a-reorganize-demo"></a>A. REORGANIZAR demostración  
 En este ejemplo se muestra cómo funciona el comando ALTER INDEX REORGANIZE.  Crea una tabla que tiene varios grupos de filas y, a continuación, se muestra cómo REORGANIZAR combina los grupos de filas.  
  
```sql  
-- Create a database   
CREATE DATABASE [ columnstore ];  
GO  
  
-- Create a rowstore staging table  
CREATE TABLE [ staging ] (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey     int  
     )  
  
-- Insert 10 million rows into the staging table.   
DECLARE @loop int  
DECLARE @AccountDescription varchar(50)  
DECLARE @AccountKey int  
DECLARE @AccountType varchar(50)  
DECLARE @AccountCode int  
  
SELECT @loop = 0  
BEGIN TRAN  
    WHILE (@loop < 300000)   
      BEGIN  
        SELECT @AccountKey = CAST (RAND()*10000000 as int);  
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);  
  
        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);  
  
        SELECT @loop = @loop + 1;  
    END  
COMMIT  
  
-- Create a table for the clustered columnstore index  
  
CREATE TABLE cci_target (  
     AccountKey              int NOT NULL,  
     AccountDescription      nvarchar (50),  
     AccountType             nvarchar(50),  
     AccountCodeAlternateKey int  
     )  
  
-- Convert the table to a clustered columnstore index named inxcci_cci_target;  
```sql
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;  
```  
  
 Utilice la opción TABLOCK para insertar filas en paralelo. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede ejecutar la operación INSERT INTO en paralelo cuando se utiliza TABLOCK.  
  
```sql  
INSERT INTO cci_target WITH (TABLOCK) 
SELECT TOP 300000 * FROM staging;  
```  
  
 Ejecute este comando para ver los grupos de filas delta abierto. El número de grupos de filas depende del grado de paralelismo.  
  
```sql  
SELECT *   
FROM sys.dm_db_column_store_row_group_physical_stats   
WHERE object_id  = object_id('cci_target');  
```  
  
 Ejecute este comando para forzar a todos los cerrado y grupos de filas OPEN en el almacén de columnas.  
  
```sql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
 Vuelva a ejecutar este comando y verá que los grupos de filas más pequeños se combinan en un grupo de filas comprimido.  
  
```sql  
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="b-compress-closed-delta-rowgroups-into-the-columnstore"></a>B. Comprimir los grupos de filas delta cerrados en el almacén de columnas  
 En este ejemplo se utiliza la REORGANIZACIÓN opción comprime cada grupo de filas delta cerrados en el almacén de columnas como un grupo de filas comprimido.   Esto no es necesario, pero es útil cuando el motor de tupla no comprime los grupos de filas CLOSED lo suficientemente rápido.  
  
```sql  
-- Uses AdventureWorksDW  
-- REORGANIZE all partitions  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
  
-- REORGANIZE a specific partition  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;  
```  
  
### <a name="c-compress-all-open-and-closed-delta-rowgroups-into-the-columnstore"></a>C. Comprimir todos abierto y cerrado grupos de filas delta al almacén de columnas  
 No se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede ejecutar REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON) para comprimir cada grupo de filas delta abierto y cerrado en el almacén de columnas como un grupo de filas comprimido. Esto vacía lo almacenes delta y obliga a todas las filas a comprimirse en el almacén de columnas. Esto es útil sobre todo después de realizar muchas operaciones de inserción porque estas operaciones almacenan las filas de uno o varios almacenes delta.  
  
 REORGANIZE combina grupos de filas para rellenar los grupos de filas hasta un número máximo de filas \<= 1,024,576. Por lo tanto, al comprimir todos los grupos de filas abierto y cerrado no terminará con una gran cantidad de grupos de filas comprimidos que solo tienen algunas filas en ellos. Desea que grupos de filas sea tan completa como sea posible reducir el tamaño comprimido y mejorar el rendimiento de las consultas.  
  
```sql  
-- Uses AdventureWorksDW2016  
-- Move all OPEN and CLOSED delta rowgroups into the columnstore.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
-- For a specific partition, move all OPEN AND CLOSED delta rowgroups into the columnstore  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
```  
  
### <a name="d-defragment-a-columnstore-index-online"></a>D. Desfragmentar un índice de almacén de columnas en línea  
 No se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], REORGANIZE comprimir más de los grupos de filas delta al almacén de columnas. También realiza la desfragmentación en línea. En primer lugar, reduce el tamaño de las vistas por quitar físicamente las filas eliminadas al 10% o más de las filas de un grupo de filas que se han eliminado.  A continuación, combina grupos de filas para formar grupos de filas mayor que tienen hasta el número máximo de 1,024,576 filas por grupos de filas.  Todos los grupos de filas que se cambian volver a obtengan comprimidos.  
  
> [!NOTE]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], volver a generar un índice de almacén de columnas ya no es necesario en la mayoría de los casos ya que REORGANIZE físicamente quita filas eliminadas y combina los grupos de filas. La opción COMPRESS_ALL_ROW_GROUPS obliga a grupos de filas delta abierto o cerrado todos en el almacén de columnas que anteriormente solo puede realizarse con una recompilación. REORGANIZAR está en línea y se produce en segundo plano, por lo que las consultas pueden continuar mientras la realiza la operación.  
  
```sql  
-- Uses AdventureWorks  
-- Defragment by physically removing rows that have been logically deleted from the table, and merging rowgroups.  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;  
```  
  
### <a name="e-rebuild-a-clustered-columnstore-index-offline"></a>E. Volver a generar un índice de almacén de columnas en clúster sin conexión  
Se aplica a: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])   
  
> [!TIP]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], se recomienda usar ALTER INDEX REORGANIZE en lugar de ALTER INDEX REBUILD.  
  
> [!NOTE]
> En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], REORGANIZE solo se usa para comprimir los grupos de filas CLOSED al almacén de columnas. La única manera de realizar operaciones de desfragmentación y para forzar a todos los grupos de filas delta al almacén de columnas es volver a generar el índice.  
  
 Este ejemplo muestra cómo volver a generar un índice de almacén de columnas agrupado y forzar a todos los grupos de filas delta al almacén de columnas. Este primer paso prepara una tabla FactInternetSales2 con un índice de almacén de columnas clúster e inserta los datos de las primeras cuatro columnas.  
  
```sql  
-- Uses AdventureWorksDW  
  
CREATE TABLE dbo.FactInternetSales2 (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2  
ON dbo.FactInternetSales2;  
  
INSERT INTO dbo.FactInternetSales2  
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey  
FROM dbo.FactInternetSales;  
  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Los resultados muestran que hay un grupo de filas abierto, lo que significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que se agreguen antes de que cierra el grupo de filas y mueve los datos en el almacén de columnas más filas. Esta instrucción siguiente vuelve a generar el índice de almacén de columnas agrupado, lo que obliga a todas las filas en el almacén de columnas.  
  
```sql  
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;  
SELECT * FROM sys.column_store_row_groups;  
```  
  
 Los resultados de la instrucción SELECT muestran que el grupo de filas es COMPRESSED, lo que significa que los segmentos de la columna del grupo de filas ahora están comprimidos y .almacenados en el almacén de columnas.  
  
### <a name="f-rebuild-a-partition-of-a-clustered-columnstore-index-offline"></a>F. Generar una partición de un índice de almacén de columnas en clúster sin conexión  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  
 
 Para volver a crear una partición de un índice de almacén de columnas agrupado grandes, utilice ALTER INDEX REBUILD con la opción de partición. En este ejemplo se vuelve a generar la partición 12. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se recomienda reemplazar REBUILD con REORGANIZE.  
  
```sql  
ALTER INDEX cci_fact3   
ON fact3  
REBUILD PARTITION = 12;  
```  
  
### <a name="g-change-a-clustered-columstore-index-to-use-archival-compression"></a>G. Cambiar un índice agrupado de almacenamiento en clúster para usar la compresión de archivo  
 No se aplica a:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 Puede reducir el tamaño de un índice de almacén de columnas agrupado aún más mediante la opción de compresión de datos COLUMNSTORE_ARCHIVE. Esto resulta práctico para los datos más antiguos que desea mantener en el almacenamiento más económico. Se recomienda usar solo en datos que no se accede con frecuencia como descomprimir es más lento que con la compresión de almacén de columnas normal.  
  
 En el ejemplo siguiente se vuelve a generar un índice de almacén de columnas clúster para usar la compresión archivada y, a continuación, se muestra cómo quitar la compresión de archivo. El resultado final usará solo la compresión de almacén de columnas.  
  
```sql  
--Prepare the example by creating a table with a clustered columnstore index.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL  
);  
  
CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);  
  
CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable  
ON SimpleTable  
WITH (DROP_EXISTING = ON);  
  
--Compress the table further by using archival compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);  
  
--Remove the archive compression and only use columnstore compression.  
ALTER INDEX cci_SimpleTable ON SimpleTable  
REBUILD  
WITH (DATA_COMPRESSION = COLUMNSTORE);  
GO  
```  
  
## <a name="examples-rowstore-indexes"></a>Ejemplos: Índices de almacén de filas  
  
### <a name="a-rebuilding-an-index"></a>A. Volver a generar un índice  
 En el siguiente ejemplo se regenera un único índice en la tabla `Employee` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;  
```  
  
### <a name="b-rebuilding-all-indexes-on-a-table-and-specifying-options"></a>B. Volver a generar todos los índices de una tabla y especificar opciones  
 En el siguiente ejemplo se especifica la palabra clave `ALL`. Esto vuelve a generar todos los índices asociados a la tabla Production.Product en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Se especifican tres opciones.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);  
```  
  
El ejemplo siguiente agrega la opción ONLINE, incluida la opción de bloqueo de prioridad baja, y agrega la opción de compresión de fila.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX ALL ON Production.Product  
REBUILD WITH   
(  
    FILLFACTOR = 80,   
    SORT_IN_TEMPDB = ON,  
    STATISTICS_NORECOMPUTE = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),   
    DATA_COMPRESSION = ROW  
);  
```  
  
### <a name="c-reorganizing-an-index-with-lob-compaction"></a>C. Reorganizar un índice con compactación LOB  
 En el siguiente ejemplo se reorganiza un único índice clúster en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Dado que el índice contiene un tipo de datos LOB en el nivel hoja, la instrucción también compacta todas las páginas que contienen datos de objetos grandes. Observe que no es necesario especificar la opción WITH (LOB_COMPACTION) dado que el valor predeterminado es ON.  
  
```sql  
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION);  
```  
  
### <a name="d-setting-options-on-an-index"></a>D. Establecer opciones en un índice  
 En el siguiente ejemplo se establecen varias opciones en el índice `AK_SalesOrderHeader_SalesOrderNumber` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON  
    Sales.SalesOrderHeader  
SET (  
    STATISTICS_NORECOMPUTE = ON,  
    IGNORE_DUP_KEY = ON,  
    ALLOW_PAGE_LOCKS = ON  
    ) ;  
GO
```  
  
### <a name="e-disabling-an-index"></a>E. Deshabilitar un índice  
 En el siguiente ejemplo se deshabilita un índice no clúster de la tabla `Employee` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```  
  
### <a name="f-disabling-constraints"></a>F. Deshabilitar restricciones  
 En el ejemplo siguiente se deshabilita una restricción PRIMARY KEY al deshabilitar el índice de clave principal en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos. La restricción FOREIGN KEY de la tabla subyacente se deshabilita automáticamente y aparece un mensaje de advertencia.  
  
```sql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;  
```  
  
El conjunto de resultados devuelve este mensaje de advertencia.  
  
```  
Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'  
on table 'EmployeeDepartmentHistory' referencing table 'Department'  
was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
```  
  
### <a name="g-enabling-constraints"></a>G. Habilitar restricciones  
 En el siguiente ejemplo se habilitan las restricciones PRIMARY KEY y FOREIGN KEY deshabilitadas en el ejemplo F.  
  
La restricción PRIMARY KEY se habilita al volver a generar el índice PRIMARY KEY.  
  
```sql  
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;  
```  
  
A continuación, se habilita la restricción FOREIGN KEY.  
  
```sql  
ALTER TABLE HumanResources.EmployeeDepartmentHistory  
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;  
GO  
```  
  
### <a name="h-rebuilding-a-partitioned-index"></a>H. Volver a generar un índice con particiones  
 En el siguiente ejemplo se vuelve a generar una única partición, el número de partición `5`, del índice con particiones `IX_TransactionHistory_TransactionDate` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. La partición 5 se vuelve a generar en línea y el tiempo de espera de 10 minutos para el bloqueo de prioridad baja se aplica independientemente a cada bloqueo adquirido por la operación de regeneración de índice. Si, durante este tiempo, el bloqueo no se puede obtener para completar la regeneración del índice, la instrucción de operación de la regeneración se anula.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```sql  
-- Verify the partitioned indexes.  
SELECT *  
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);  
GO  
--Rebuild only partition 5.  
ALTER INDEX IX_TransactionHistory_TransactionDate  
ON Production.TransactionHistory  
REBUILD Partition = 5   
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));  
GO  
```  
  
### <a name="i-changing-the-compression-setting-of-an-index"></a>I. Cambiar la configuración de compresión de un índice  
 En el ejemplo siguiente se vuelve a generar un índice en una tabla de almacén de filas sin particiones.  
  
```sql
ALTER INDEX IX_INDEX1   
ON T1  
REBUILD   
WITH (DATA_COMPRESSION = PAGE);  
GO  
```  
  
Para obtener ejemplos de compresión de datos adicionales, consulte [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
 
### <a name="j-online-resumable-index-rebuild"></a>J. Reconstrucción de índices reanudables en línea

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) y[!INCLUDE[ssSDS](../../includes/sssds-md.md)]   

 Los ejemplos siguientes muestran cómo usar la reconstrucción de índices reanudables en línea. 

1. Ejecutar una regeneración de índice en línea como operación reanudable con MAXDOP = 1.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, MAXDOP=1, RESUMABLE=ON) ;
   ```

2. Ejecutar el mismo comando nuevo (véase más arriba) después de una operación de índice se pausó, reanuda automáticamente la operación de regeneración del índice.

3. Ejecutar una regeneración de índice en línea como reanudable operación con el conjunto MAX_DURATION y 240 minutos.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE=ON, RESUMABLE=ON, MAX_DURATION=240) ; 
   ```
4. Pausar una recompilación de funcionamiento reanudables índice en línea.

   ```sql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```   
5. Reanudar una regeneración de índice en línea para una regeneración de índice que se ejecutó como reanudable operación especifica un nuevo valor de MAXDOP se establece en 4.

   ```sql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP=4) ;
   ```
6. Reanudar una operación de regeneración de índice en línea para una regeneración de índice en línea que se ejecutó como reanudables. Establecer MAXDOP a 2, el tiempo de ejecución para el índice que se está ejecutando como resmumable y 240 minutos y en el caso de un índice que se está bloqueado en espera de bloqueo 10 minutos y después eliminar todos los bloqueadores de elementos. 

   ```sql
      ALTER INDEX test_idx on test_table  
         RESUME WITH (MAXDOP=2, MAX_DURATION= 240 MINUTES, 
         WAIT_AT_LOW_PRIORITY (MAX_DURATION=10, ABORT_AFTER_WAIT=BLOCKERS)) ;
   ```      
7. Anular la operación de regeneración del índice reanudables que se está ejecutando o en pausa.

   ```sql
   ALTER INDEX test_idx on test_table ABORT ;
   ``` 
  
## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Crear índice espacial &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [Crear índice XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [Realizar operaciones de índice en línea](../../relational-databases/indexes/perform-index-operations-online.md)   
 [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
