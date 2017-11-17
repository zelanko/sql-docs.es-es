---
title: "CREAR el índice de almacén (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE INDEX
- COLUMNSTORE_INDEX_TSQL
- CREATE CLUSTERED COLUMNSTORE INDEX
- COLUMNSTORE_TSQL
- CREATE NONCLUSTERED COLUMNSTORE INDEX
- CREATE_NONCLUSTERED_COLUMNSTORE_INDEX_TSQL
- CREATE COLUMNSTORE INDEX
- CREATE_CLUSTERED_COLUMNSTORE_INDEX_TSQL
- COLUMNSTORE
dev_langs:
- TSQL
helpviewer_keywords:
- index creation [SQL Server], columnstore indexes
- columnstore index, creating
- CREATE COLUMNSTORE INDEX statement
- CREATE INDEX statement
ms.assetid: 7e1793b3-5383-4e3d-8cef-027c0c8cb5b1
caps.latest.revision: 76
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 0fb8883678dad7a62cac9c2109b093ee79e27b27
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="create-columnstore-index-transact-sql"></a>CREATE COLUMNSTORE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Convertir una tabla de almacén de filas en un índice de almacén de columnas agrupado o crear un índice no clúster de almacén de columnas. Usar un índice de almacén para ejecutar de forma eficaz los análisis operativos en tiempo real en una carga de trabajo OLTP o para mejorar el rendimiento de la compresión y la consulta de datos para las cargas de trabajo de almacenamiento de datos.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede crear la tabla como un índice de almacén de columnas agrupado.   Ya no es necesario crear primero una tabla de almacén de filas y, a continuación, convertirlo en un índice de almacén de columnas agrupado.  
  
Vaya a ejemplos:  
-   [Ejemplos para convertir una tabla de almacén de filas en el almacén de columnas](../../t-sql/statements/create-columnstore-index-transact-sql.md#convert)  
-   [Ejemplos para los índices no agrupados](../../t-sql/statements/create-columnstore-index-transact-sql.md#nonclustered)  
  
Vaya a escenarios:  
-   [Índices de almacén de columnas para análisis operativos en tiempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
-   [Índices de almacén de columnas para el almacenamiento de datos de](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
Aprende más:  
-   [Guía de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)  
-   [Resumen de características de los índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create a clustered columnstore index on disk-based table.  
CREATE CLUSTERED COLUMNSTORE INDEX index_name  
    ON [database_name. [schema_name ] . | schema_name . ] table_name  
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]  
[ ; ]  
  
--Create a non-clustered columnstore index on a disk-based table.  
CREATE [NONCLUSTERED]  COLUMNSTORE INDEX index_name   
    ON [database_name. [schema_name ] . | schema_name . ] table_name   
        ( column  [ ,...n ] )  
    [ WHERE <filter_expression> [ AND <filter_expression> ] ]
    [ WITH ( < with_option> [ ,...n ] ) ]  
    [ ON <on_option> ]   
[ ; ]  
  
<with_option> ::=  
      DROP_EXISTING = { ON | OFF } -- default is OFF  
    | MAXDOP = max_degree_of_parallelism 
    | ONLINE = { ON | OFF } 
    | COMPRESSION_DELAY  = { 0 | delay [ Minutes ] }  
    | DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { partition_number_expression | range } [ ,...n ] ) ]  
  
<on_option>::=  
      partition_scheme_name ( column_name )   
    | filegroup_name   
    | "default"   
  
<filter_expression> ::=  
      column_name IN ( constant [ ,...n ]  
    | column_name { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< } constant  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CLUSTERED COLUMNSTORE INDEX index_name   
    ON [ database_name . [ schema_name ] . | schema_name . ] table_name  
    [ WITH ( DROP_EXISTING = { ON | OFF } ) ] --default is OFF  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
CREATE CLUSTERED COLUMNSTORE INDEX  
Crear un índice de almacén de columnas agrupado en el que todos los datos se comprimen y almacenan por columna. El índice incluye todas las columnas de la tabla y almacena toda la tabla. Si la tabla existente es un índice agrupado o montón, la tabla se convierte en un índice de almacén de columnas agrupado. Si la tabla ya se almacena como un índice de almacén de columnas agrupado, el índice existente se quita y vuelve a generar.  
  
*index_name*  
Especifica el nombre para el nuevo índice.  
  
Si la tabla ya tiene un índice de almacén de columnas agrupado, puede especificar el mismo nombre que el índice existente, o puede usar la opción DROP EXISTING para especificar un nuevo nombre.  
  
ON [*database_name*. [*schema_name* ]. | *schema_name* . ] *table_name*  
   Especifica el nombre de una, dos o tres partes de la tabla que se almacenará como un índice clúster de almacén de columnas. Si la tabla es un montón o índice agrupado en la tabla se convierte de almacén de filas en un almacén de columnas. Si la tabla ya es un almacén de columnas, esta instrucción vuelve a generar el índice de almacén de columnas agrupado.  
  
por  
DROP_EXISTING = [DESACTIVADO] | ON  
   DROP_EXISTING = ON especifica que se quite el índice de almacén de columnas clúster existente y crear un nuevo índice de almacén de columnas.  

   El valor predeterminado, DROP_EXISTING = OFF espera que el nombre del índice es el mismo que el nombre existente. Se produce un error es el nombre del índice especificado ya existe.  
  
MAXDOP = *max_degree_of_parallelism*  
   Reemplaza la configuración del servidor existente para el grado máximo de paralelismo mientras dura la operación de índice. Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
   *max_degree_of_parallelism* los valores pueden ser:  
   - 1: suprime la generación de planes paralelos.  
   - \>1: limitar el número máximo de procesadores utilizados en una operación de índice en paralelo al número especificado o menos, según la carga de trabajo del sistema actual. Por ejemplo, si MAXDOP = 4, el número de procesadores que desea usar es 4 o menos.  
   - 0 (predeterminado): usa el número real de procesadores o menos, según la carga de trabajo actual del sistema.  
  
   Para obtener más información, consulte [configurar la max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md), y [configurar operaciones de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
 
COMPRESSION_DELAY = **0** | *retraso* [minutos]  
   Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

   Para una tabla basada en disco, *retraso* especifica el número mínimo de minutos que debe permanecer un grupo de filas delta en estado cerrado en el grupo de filas delta antes de que SQL Server puede comprimir en el grupo de filas comprimido. Puesto que las tablas basadas en disco no realizar el seguimiento de insertar y actualizar horas en filas individuales, SQL Server aplica el retraso a grupos de filas delta en estado cerrado.  
   El valor predeterminado es 0 minutos.  
   Para obtener recomendaciones sobre cuándo usar COMPRESSION_DELAY, vea [Introducción al almacén de columnas para análisis operativos en tiempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).  
  
DATA_COMPRESSION = COLUMNSTORE | COLUMNSTORE_ARCHIVE  
   Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
Especifica la opción de compresión de datos para la tabla, el número de partición o el intervalo de particiones especificados. Las opciones son las siguientes:   
COLUMNSTORE  
   Almacén de columnas es el valor predeterminado y especifica que se debe comprimir con la mayor compresión de almacén de columnas de rendimiento. Esta es la opción típica.  
  
COLUMNSTORE_ARCHIVE  
   COLUMNSTORE_ARCHIVE más comprime la tabla o partición para reducir su tamaño. Utilice esta opción para situaciones como archivado que requieran un tamaño menor de almacenamiento y pueda permitirse más tiempo para el almacenamiento y recuperación.  
  
   Para obtener más información acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  

ON  
   Con las opciones ON puede especificar opciones para el almacenamiento de datos, como un esquema de partición, un grupo de archivos específico o el grupo de archivos predeterminado. Si no se especifica la opción ON, el índice usa la configuración de partición o grupo de archivos de configuración de la tabla existente.  
  
   *partition_scheme_name* **(** *column_name* **)**  
   Especifica el esquema de partición de la tabla. El esquema de partición ya debe existir en la base de datos. Para crear el esquema de partición, vea [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md).  
 
   *column_name* especifica la columna en la que se particiona un índice con particiones. Esta columna debe coincidir con el tipo de datos, la longitud y la precisión del argumento de la partición de la función que *partition_scheme_name* está usando.  

   *filegroup_name*  
   Especifica el grupo de archivos para almacenar el índice clúster de almacén de columnas. Si no se especifica ninguna ubicación y la tabla no tiene particiones, el índice usa el mismo grupo de archivos que la tabla o la vista subyacente. El grupo de archivos debe existir previamente.  

   **"**predeterminado**"**  
   Para crear el índice en el grupo de archivos predeterminado, use "default" o [default].  
  
   Si se especifica "default", la opción QUOTED_IDENTIFIER debe tener el valor ON para la sesión actual. QUOTED_IDENTIFIER es ON de forma predeterminada. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
CREAR ÍNDICE DE ALMACÉN [NONCLUSTERED]  
Crear un índice no clúster de almacén de columnas en memoria en una tabla de almacén de filas almacenada como un índice agrupado o montón. El índice puede tener una condición de filtrado y no necesita incluir todas las columnas de la tabla subyacente. El índice de almacén de columnas requiere suficiente espacio para almacenar una copia de los datos. Es actualizable y se actualiza cuando se cambia la tabla subyacente. El índice de almacén de columnas en un índice agrupado permite análisis en tiempo real.  
  
*index_name*  
   Especifica el nombre del índice. *index_name* debe ser único dentro de la tabla, pero no tiene que ser único dentro de la base de datos. Los nombres de índice deben seguir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 **(** *columna* [ **,**... *n* ] **)**  
    Especifica las columnas que se van a almacenar. Un índice de almacén de columnas no clúster está limitado a 1024 columnas.  
   Cada columna debe ser de un tipo de datos compatible con los índices de almacén de columnas. Vea [limitaciones y restricciones](../../t-sql/statements/create-columnstore-index-transact-sql.md#LimitRest) para obtener una lista de los tipos de datos admitidos.  

ON [*database_name*. [*schema_name* ]. | *schema_name* . ] *table_name*  
   Especifica el uno, dos o tres partes de nombre de la tabla que contiene el índice.  

CON DROP_EXISTING = [DESACTIVADO] | ON  
   DROP_EXISTING = ON, se quita y vuelve a generar el índice existente. El nombre de índice especificado debe ser el mismo que el de un índice actualmente existente; sin embargo, la definición se puede modificar. Por ejemplo, puede especificar distintas columnas u opciones de índice.
  
   DROP_EXISTING = OFF, se muestra un error si ya existe el nombre del índice especificado. El tipo de índice no puede cambiarse utilizando DROP_EXISTING. En la sintaxis compatible con versiones anteriores, WITH DROP_EXISTING es equivalente a WITH DROP_EXISTING = ON.  

MAXDOP = *max_degree_of_parallelism*  
   Invalida el [configurar la max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) opción de configuración para la duración de la operación de índice. Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
   *max_degree_of_parallelism* los valores pueden ser:  
   - 1: suprime la generación de planes paralelos.  
   - \>1: limitar el número máximo de procesadores utilizados en una operación de índice en paralelo al número especificado o menos, según la carga de trabajo del sistema actual. Por ejemplo, si MAXDOP = 4, el número de procesadores que desea usar es 4 o menos.  
   - 0 (predeterminado): usa el número real de procesadores o menos, según la carga de trabajo actual del sistema.  
  
   Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operaciones de índice en paralelo no están disponibles en todas las ediciones de [!INCLUDE[msC](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
ONLINE = [ON | OFF]   
   Se aplica a: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], en únicamente los índices no agrupados.
ON especifica que el índice de almacén de columnas no clúster permanece en línea y disponible cuando la nueva copia del índice se va a compilar.

   DESACTIVAR especifica que el índice no está disponible para su uso durante la generación de la nueva copia. Puesto que éste es un índice no agrupado, la tabla base se conserva disponibles, que solo el índice de almacén de columnas no se utiliza para satisfacer las consultas hasta que finalice el nuevo índice. 

COMPRESSION_DELAY = **0** | \<retraso > [minutos]  
   Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
   Especifica un límite inferior en cuánto tiempo una fila debe permanecer en el grupo de filas delta antes de que se pueden migrar a un grupo de filas comprimido. Por ejemplo, un cliente puede decir que si una fila se ha modificado durante 120 minutos, que se pueda seleccionar para comprimir en formato de almacenamiento en columnas. Índice de almacén de columnas en tablas basadas en disco, no Mida el tiempo cuando una fila se inserta o actualiza, usamos el tiempo de filas cerrado delta como un proxy para la fila en su lugar. La duración predeterminada es 0 minutos. Una fila se migra al almacenamiento en columnas una vez que se ha acumulado en el grupo de filas delta 1 millón de filas y se ha marcado como cerrado.  
  
DATA_COMPRESSION  
   Especifica la opción de compresión de datos para la tabla, el número de partición o el intervalo de particiones especificados. Las opciones son las siguientes:  
COLUMNSTORE  
   Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Solo se aplica a los índices de almacén de columnas, incluidos los clúster y no clúster. Almacén de columnas es el valor predeterminado y especifica que se debe comprimir con la mayor compresión de almacén de columnas de rendimiento. Esta es la opción típica.  
  
COLUMNSTORE_ARCHIVE  
   Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
Solo se aplica a los índices de almacén de columnas, incluidos los clúster y no clúster. COLUMNSTORE_ARCHIVE más comprime la tabla o partición para reducir su tamaño. Esto se puede usar para el archivado o para otras situaciones que requieran un tamaño de almacenamiento mínimo y pueda permitirse más tiempo para el almacenamiento y recuperación.  
  
 Para obtener más información acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
DONDE \<filter_expression > [AND \<filter_expression >] se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
   Llama a un predicado de filtro, esto especifica qué filas desea incluir en el índice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]crea las estadísticas filtradas en las filas de datos en el índice filtrado.  
  
   El predicado de filtro utiliza la lógica de comparación simple. Las comparaciones que utilizan literales NULL no se admiten con los operadores de comparación. En su lugar, use los operadores IS NULL e IS NOT NULL.  
  
   A continuación, se muestran algunos ejemplos de predicados de filtro para la tabla `Production.BillOfMaterials`:  
   `WHERE StartDate > '20000101' AND EndDate <= '20000630'`    
   `WHERE ComponentID IN (533, 324, 753)`  
   `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
   
   Para obtener instrucciones sobre índices filtrados, vea [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
ON  
   Estas opciones especifican los grupos de archivos en el que se crea el índice.  
  
*partition_scheme_name* **(** *column_name* **)**  
   Especifica el esquema de partición que define los grupos de archivos en el que se asigna las particiones de un índice con particiones. El esquema de partición debe existir en la base de datos mediante la ejecución de [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). 
   *column_name* especifica la columna en la que se particiona un índice con particiones. Esta columna debe coincidir con el tipo de datos, la longitud y la precisión del argumento de la partición de la función que *partition_scheme_name* está usando. *column_name* no está restringida a las columnas de la definición del índice. Al crear particiones en un índice de almacén de columnas, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] agrega la columna de partición como una columna del índice, si no se especificó todavía.  
   Si *partition_scheme_name* o *archivos* no se ha especificado y la tabla tiene particiones, el índice se sitúa en el mismo esquema de partición, con la misma columna de partición que la tabla subyacente.  
   Un índice de almacén de columnas de una tabla con particiones debe estar alineado.  
   Para obtener más información acerca de las particiones de índices, vea [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  

*filegroup_name*  
   Especifica el nombre de un grupo de archivos en el que se va a crear el índice. Si *filegroup_name* no se ha especificado y la tabla no tiene particiones, el índice usa el mismo grupo de archivos que la tabla subyacente. El grupo de archivos debe existir previamente.  
 
**"**predeterminado**"**  
Crea el índice especificado en el grupo de archivos predeterminado.  
  
El término predeterminado (default), en este contexto, no es una palabra clave. Es un identificador para el grupo de archivos predeterminado y debe delimitarse, como en ON **"**predeterminado**"** u ON **[**predeterminado**]**. Si se especifica "default", la opción QUOTED_IDENTIFIER debe tener el valor ON para la sesión actual. Esta es la configuración predeterminada. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
##  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="GenRemarks"></a>Notas generales  
 Puede crearse un índice de almacén de columnas en una tabla temporal. Cuando se quita la tabla o finaliza la sesión, también se quita el índice.  
 
## <a name="filtered-indexes"></a>Índices filtrados  
Un índice filtrado es un índice no clúster optimizado, adecuado para las consultas que seleccionan un porcentaje pequeño de las filas de una tabla. Utiliza un predicado de filtro para indizar una parte de los datos de la tabla. Un índice filtrado bien diseñado puede mejorar el rendimiento de las consultas, reducir los costos de almacenamiento y de mantenimiento.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Opciones SET requeridas para los índices filtrados  
Las opciones SET de la columna de valor requerido son necesarias siempre que se dé alguna de las condiciones siguientes:  
- Se crea un índice filtrado.  
- La operación INSERT, UPDATE, DELETE o MERGE modifica los datos de un índice filtrado.  
- Se utiliza el índice filtrado por el optimizador de consultas para generar el plan de consulta.  
  
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
  
##  <a name="LimitRest"></a> Limitaciones y restricciones  

**Cada columna de un índice de almacén de columnas debe ser de uno de los tipos de datos empresariales comunes siguientes:** 
-   DateTimeOffset [(  *n*  )]  
-   datetime2 [(  *n*  )]  
-   datetime  
-   smalldatetime  
-   date  
-   tiempo [(  *n*  )]  
-   float [(  *n*  )]  
-   real [(  *n*  )]  
-   decimal [( *precisión* [ *, escala* ] **)** ]
-   numérico [( *precisión* [ *, escala* ] **)** ]    
-   money  
-   smallmoney  
-   bigint  
-   int  
-   smallint  
-   tinyint  
-   bit  
-   nvarchar [(  *n*  )] 
-   nvarchar (max) (se aplica a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y base de datos de SQL de Azure en premium tarifa, en los índices de almacén de columnas agrupado solo)   
-   nchar [(  *n*  )]  
-   varchar [(  *n*  )]  
-   varchar (max) (se aplica a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y base de datos de SQL de Azure en premium tarifa, en los índices de almacén de columnas agrupado solo)
-   Char [(  *n*  )]  
-   varbinary [(  *n*  )] 
-   varbinary (max) (se aplica a [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y base de datos de SQL de Azure en premium tarifa, en los índices de almacén de columnas agrupado solo)
-   binario [(  *n*  )]  
-   uniqueidentifier (se aplica a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores)
  
Si la tabla subyacente tiene una columna de un tipo de datos que no se admite para los índices de almacén de columnas, se debe omitir esa columna del índice no agrupado de almacén de columnas.  
  
**No se pueden incluir columnas que usan cualquiera de los siguientes tipos de datos en un índice de almacén de columnas:**
-   ntext, text e image  
-   nvarchar (max), varchar (max) y varbinary (max) (se aplica a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y las versiones anteriores y no agrupados) 
-   rowversion (y timestamp)  
-   sql_variant  
-   Tipos CLR (hierarchyid y tipos espaciales)  
-   xml  
-   uniqueidentifier (se aplica a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])  

**Índices no agrupados:**
-   No puede tener más de 1024 columnas.  
-   Una tabla con un índice de almacén de columnas no clúster puede tener restricciones UNIQUE, restricciones de clave principal o restricciones de clave externa, pero las restricciones no se pueden incluir en el índice de almacén de columnas no clúster.  
-   No se puede crear en una vista o una vista indizada.  
-   No puede incluir ninguna columna dispersa.  
-   No se puede cambiar mediante el uso de la **ALTER INDEX** instrucción. Para cambiar el índice no clúster, debe quitar y volver a crear el índice de almacén de columnas en su lugar. Puede usar **ALTER INDEX** para deshabilitar y volver a generar un índice de almacén de columnas.  
-   No se puede crear mediante el uso de la **INCLUDE** palabra clave.  
-   No puede incluir el **ASC** o **DESC** palabras clave para ordenar el índice. Los índices de almacén de columnas se ordenan de acuerdo con los algoritmos de compresión. La ordenación eliminaría muchas mejoras de rendimiento.  
-   No puede incluir columnas de objetos grandes (LOB) de tipo nvarchar (max), varchar (max) y varbinary (max) en índices de almacén de columnas no agrupado. Solo los índices de almacén de columnas agrupado admiten tipos de LOB, a partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] versión y la base de datos de SQL de Azure configurada en tarifa premium. Tenga en cuenta que las versiones anteriores no admiten tipos de LOB en los índices de almacén de columnas agrupados y no agrupados.


 **Índices de almacén de columnas no se puede combinar con las siguientes características:**  
-   Columnas calculadas A partir de SQL Server 2017, un índice de almacén de columnas agrupado puede contener una columna calculada no persistente. Sin embargo, en SQL Server 2017, índices de almacén de columnas agrupado no pueden contener columnas calculadas persistentes y no se puede crear índices no agrupados en columnas calculadas. 
-   Compresión de página y fila, y **vardecimal** el formato de almacenamiento (un índice de almacén de columnas ya está comprimido en un formato diferente).  
-   Replicación  
-   Secuencia de archivos

No puede utilizar los cursores o desencadenadores en una tabla con un índice de almacén de columnas agrupado. Esta restricción no se aplica a los índices no agrupados; Puede utilizar los cursores y desencadenadores en una tabla con un índice no clúster de almacén de columnas.

**Limitaciones específicas de SQL Server 2014**  
Estas limitaciones se aplican sólo a SQL Server 2014. En esta versión, introdujimos índices de almacén de columnas agrupado actualizable. Los índices no agrupados estaban siendo de solo lectura.  

-   Seguimiento de cambios. No puede utilizar el seguimiento de cambios con índices de almacén de columnas no agrupado (NCCI) porque son de solo lectura. Funciona para los índices de almacén de columnas agrupados (CCI).  
-   Captura de datos modificados. No puede utilizar el cambio de captura de datos para el índice de almacén de columnas no agrupado (NCCI) porque son de solo lectura. Funciona para los índices de almacén de columnas agrupados (CCI).  
-   Base de datos secundaria legible. No se puede tener acceso a un índice de almacén de columnas agrupado en clúster (CCI) de un elemento secundario legible de un grupo de disponibilidad siempre OnReadable.  Puede tener acceso a un índice de almacén de columnas no agrupado (NCCI) de una base de datos secundaria legible.  
-   Conjuntos de resultados activos múltiples (MARS). SQL Server 2014 utiliza MARS para las conexiones de solo lectura para tablas con un índice de almacén de columnas.    Sin embargo, SQL Server 2014 no es compatible con MARS para operaciones de DML (lenguaje) de manipulación de datos simultáneas en una tabla con un índice de almacén de columnas. Cuando esto ocurre, SQL Server termina las conexiones y anula las transacciones.  
  
 Para obtener información sobre las ventajas de rendimiento y las limitaciones de los índices de almacén de columnas, vea [información general de los índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md).
  
##  <a name="Metadata"></a> Metadatos  
 Todas las columnas de un índice de almacén de columnas se almacenan en los metadatos como columnas incluidas. El índice de almacén de columnas no tiene columnas de clave. Estas vistas del sistema proporcionan información sobre los índices de almacén de columnas.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  

##  <a name="convert"></a>Ejemplos para convertir una tabla de almacén de filas en el almacén de columnas  
  
### <a name="a-convert-a-heap-to-a-clustered-columnstore-index"></a>A. Convertir un montón en un índice clúster de almacén de columnas  
 En este ejemplo se crea una tabla como un montón y después se convierte en un índice clúster de almacén de columnas denominado cci_Simple. Esto cambia el almacenamiento de la tabla de un almacén de filas a un almacén de columnas.  
  
```  
CREATE TABLE SimpleTable(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_Simple ON SimpleTable;  
GO  
```  
  
### <a name="b-convert-a-clustered-index-to-a-clustered-columnstore-index-with-the-same-name"></a>B. Convertir un índice clúster en un índice clúster de almacén de columnas con el mismo nombre.  
 En este ejemplo se crea la tabla con un índice clúster y después se muestra la sintaxis para convertir el índice clúster en un índice clúster de almacén de columnas. Esto cambia el almacenamiento de la tabla de un almacén de filas a un almacén de columnas.  
  
```  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cl_simple ON SimpleTable  
WITH (DROP_EXISTING = ON);  
GO  
```  
  
### <a name="c-handle-nonclustered-indexes-when-converting-a-rowstore-table-to-a-columnstore-index"></a>C. Administrar índices no clúster al convertir una tabla de almacén de filas en un índice de almacén de columnas.  
 Este ejemplo muestra cómo tratar los índices no clúster al convertir una tabla de almacén de filas en un índice de almacén de columnas. En realidad, comenzando con [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ninguna acción especial es necesaria; [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define automáticamente y vuelve a generar los índices no clúster en el nuevo índice de almacén de columnas agrupado.  
  
 Si desea quitar los índices no clúster, utilice la instrucción DROP INDEX antes de crear el índice de almacén de columnas. La opción DROP EXISTING solo quita el índice agrupado que se va a convertir. No quita los índices no clúster.  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], no pudo crear un índice no agrupado en un índice de almacén de columnas. Este ejemplo muestra cómo en versiones anteriores es necesario quitar los índices no clúster antes de crear el índice de almacén de columnas.  
  
```  
  
--Create the table for use with this example.  
CREATE TABLE SimpleTable (  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
  
--Create two nonclustered indexes for use with this example  
CREATE INDEX nc1_simple ON SimpleTable (OrderDateKey);  
CREATE INDEX nc2_simple ON SimpleTable (DueDateKey);   
GO  
  
--SQL Server 2012 and SQL Server 2014: you need to drop the nonclustered indexes  
--in order to create the columnstore index.   
  
DROP INDEX SimpleTable.nc1_simple;  
DROP INDEX SimpleTable.nc2_simple;  
  
--Convert the rowstore table to a columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_simple ON SimpleTable;   
GO  
  
```  
  
### <a name="d-convert-a-large-fact-table-from-rowstore-to-columnstore"></a>D. Convertir una tabla de hechos grande de almacén de filas en almacén de columnas  
 En este ejemplo se explica cómo convertir una tabla de hechos grande desde una tabla de almacén de filas en una tabla de almacén de columnas.  
  
 Para convertir una tabla de almacén de filas en una tabla de almacén de columnas.  
  
1.  En primer lugar, cree una tabla pequeña para usar en este ejemplo.  
  
    ```  
    --Create a rowstore table with a clustered index and a non-clustered index.  
    CREATE TABLE MyFactTable (  
        ProductKey [int] NOT NULL,  
        OrderDateKey [int] NOT NULL,  
         DueDateKey [int] NOT NULL,  
         ShipDateKey [int] NOT NULL )  
    )  
    WITH (  
        CLUSTERED INDEX ( ProductKey )  
    );  
  
    --Add a non-clustered index.  
    CREATE INDEX my_index ON MyFactTable ( ProductKey, OrderDateKey );  
    ```  
  
2.  Quite todos los índices no clúster de la tabla de almacén de filas.  
  
    ```  
    --Drop all non-clustered indexes  
    DROP INDEX my_index ON MyFactTable;  
    ```  
  
3.  Quitar el índice clúster.  
  
    -   Haga esto solo si desea especificar un nuevo nombre para el índice cuando se convierta en un índice clúster de almacén de columnas. Si no se quita el índice agrupado, el nuevo índice de almacén de columnas agrupado tiene el mismo nombre.  
  
        > [!NOTE]  
        >  El nombre del índice será más fácil de recordar si usa su propio nombre. Todos los índices de almacén de filas agrupado utilizan el nombre predeterminado que es ' ClusteredIndex_\<GUID >'.  
  
    ```  
    --Process for dropping a clustered index.  
    --First, look up the name of the clustered rowstore index.  
    --Clustered rowstore indexes always use the DEFAULT name ‘ClusteredIndex_<GUID>’.  
    SELECT i.name   
    FROM sys.indexes i   
    JOIN sys.tables t  
    ON ( i.type_desc = 'CLUSTERED' ) WHERE t.name = 'MyFactTable';  
  
    --Drop the clustered rowstore index.  
    DROP INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09 ON MyDimTable;  
    ```  
  
4.  Convierta la tabla de almacén de filas en una tabla de almacén de columnas con un índice clúster de almacén de columnas.  
  
    ```  
    --Option 1: Convert to columnstore and name the new clustered columnstore index MyCCI.  
    CREATE CLUSTERED COLUMNSTORE INDEX MyCCI ON MyFactTable;  
  
    --Option 2: Convert to columnstore and use the rowstore clustered   
    --index name for the columnstore clustered index name.  
    --First, look up the name of the clustered rowstore index.  
    SELECT i.name   
    FROM sys.indexes i  
    JOIN sys.tables t   
    ON ( i.type_desc = 'CLUSTERED' )  
    WHERE t.name = 'MyFactTable';  
  
    --Second, create the clustered columnstore index and   
    --Replace ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    --with the name of your clustered index.  
    CREATE CLUSTERED COLUMNSTORE INDEX   
    ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
     ON MyFactTable  
    WITH DROP_EXISTING = ON;  
    ```  
  
### <a name="e-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>E. Convertir una tabla de almacén de columnas en una tabla de almacén de filas con un índice clúster  
 Para convertir una tabla de almacén de columnas en una tabla de almacén de filas con un índice clúster, use la instrucción CREATE INDEX con la opción DROP_EXISTING.  
  
```  
CREATE CLUSTERED INDEX ci_MyTable   
ON MyFactTable  
WITH ( DROP EXISTING = ON );  
```  
  
### <a name="f-convert-a-columnstore-table-to-a-rowstore-heap"></a>F. Convertir una tabla de almacén de columnas en un montón de almacenes de filas  
 Para convertir una tabla de almacén de columnas en un montón de almacenes de filas, simplemente quite el índice clúster de almacén de columnas.  
  
```  
DROP INDEX MyCCI   
ON MyFactTable;  
```  
  

### <a name="g-defragment-by-rebuilding-the-entire-clustered-columnstore-index"></a>G. Desfragmentar al volver a generar el índice agrupado de almacén de columnas completo  
   Se aplica a: SQL Server 2014  
  
 Hay dos maneras de volver a generar todo el índice clúster de almacén de columnas. Puede usar CREATE CLUSTERED COLUMNSTORE INDEX, o [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md) y la opción REBUILD. Con ambos métodos se obtienen los mismos resultados.  
  
> [!NOTE]  
>  A partir de SQL Server 2016, utilice ALTER INDEX REORGANIZE en lugar de volver a generar con los métodos descritos en este ejemplo.  
  
```  
--Determine the Clustered Columnstore Index name of MyDimTable.  
SELECT i.object_id, i.name, t.object_id, t.name   
FROM sys.indexes i   
JOIN sys.tables t  
ON (i.type_desc = 'CLUSTERED COLUMNSTORE')  
WHERE t.name = 'RowstoreDimTable';  
  
--Rebuild the entire index by using CREATE CLUSTERED INDEX.  
CREATE CLUSTERED COLUMNSTORE INDEX my_CCI   
ON MyFactTable  
WITH ( DROP_EXISTING = ON );  
  
--Rebuild the entire index by using ALTER INDEX and the REBUILD option.  
ALTER INDEX my_CCI  
ON MyFactTable  
REBUILD PARTITION = ALL  
WITH ( DROP_EXISTING = ON );  
  
```  
  
##  <a name="nonclustered"></a>Ejemplos para los índices no agrupados  
  
### <a name="a-create-a-columnstore-index-as-a-secondary-index-on-a-rowstore-table"></a>A. Crear un índice de almacén como un índice secundario en una tabla de almacén de filas  
 En este ejemplo se crea un índice no clúster de almacén de columnas en una tabla de almacén de filas. Índice de almacén de columnas solo puede crearse en esta situación. El índice de almacén de columnas necesita almacenamiento adicional porque contiene una copia de los datos en la tabla de almacén de filas. Este ejemplo crea una tabla simple y un índice clúster y, a continuación, muestra la sintaxis para crear un índice no clúster de almacén de columnas.  
  
```  
CREATE TABLE SimpleTable  
(ProductKey [int] NOT NULL,   
OrderDateKey [int] NOT NULL,   
DueDateKey [int] NOT NULL,   
ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED INDEX cl_simple ON SimpleTable (ProductKey);  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey);  
GO  
```  
  
### <a name="b-create-a-simple-nonclustered-columnstore-index-using-all-options"></a>B. Crea un índice de almacén de columnas no clúster sencillo utilizando todas las opciones  
 En el ejemplo siguiente se muestra la sintaxis para crear un índice no clúster de almacén de columnas usando todas las opciones.  
  
```  
CREATE NONCLUSTERED COLUMNSTORE INDEX csindx_simple  
ON SimpleTable  
(OrderDateKey, DueDateKey, ShipDateKey)  
WITH (DROP_EXISTING =  ON,   
    MAXDOP = 2)  
ON "default"  
GO  
```  
  
 Para obtener un ejemplo más complejo con tablas con particiones, vea [información general de los índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
### <a name="c-create-a-nonclustered-columnstore-index-with-a-filtered-predicate"></a>C. Crear un índice no clúster de almacén de columnas con un predicado filtrado  
 En el ejemplo siguiente se crea un índice de almacén de columnas no agrupado filtrado en la tabla Production.BillOfMaterials de la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos. El predicado de filtro puede incluir columnas que no son columnas de clave en el índice filtrado. El predicado de este ejemplo selecciona solo las filas en que EndDate no es NULL.  
  
```  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithEndDate'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED COLUMNSTORE INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
  
```  
  
###  <a name="ncDML"></a> D. Cambiar los datos de un índice no clúster de almacén de columnas  
   Se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].
  
 Una vez creado un índice no clúster de almacén de columnas en una tabla, no puede modificar directamente los datos de esa tabla. Una consulta con INSERT, UPDATE, DELETE o MERGE, se produce un error y devuelve un mensaje de error. Para agregar o modificar los datos de la tabla, puede hacer lo siguiente:  
  
-   Deshabilitar o quitar el índice de almacén de columnas. Después puede actualizar los datos de la tabla. Si deshabilita el índice de almacén de columnas, puede regenerar el índice de almacén de columnas cuando termine de actualizar los datos. Por ejemplo,  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Cargar datos en una tabla de ensayo que no tenga un índice de almacén de columnas. Genere un índice de almacén de columnas en la tabla de ensayo. Cambie la tabla de ensayo a una partición vacía de la tabla principal.  
  
-   Cambiar una partición de la tabla con el índice de almacén de columnas a una tabla de ensayo vacía. Si hay un índice de almacén de columnas en la tabla de ensayo, deshabilítelo. Realice las actualizaciones que desee. Genere (o regenere) el índice de almacén de columnas. Vuelva a cambiar la tabla de ensayo a la partición (ahora vacía) de la tabla principal.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-change-a-clustered-index-to-a-clustered-columnstore-index"></a>A. Cambiar un índice agrupado a un índice de almacén de columnas agrupado  
 Mediante la instrucción CREATE CLUSTERED COLUMNSTORE INDEX con DROP_EXISTING = ON, puede:  
  
-   Cambiar un índice clúster en un índice de almacén de columnas agrupado.  
  
-   Volver a generar un índice de almacén de columnas agrupado.  
  
 Este ejemplo crea la tabla xDimProduct como una tabla de almacén de filas con un índice agrupado y, a continuación, usa CREATE CLUSTERED COLUMNSTORE INDEX para convertir la tabla de una tabla de almacén de filas en una tabla de almacén de columnas.  
  
```  
-- Uses AdventureWorks  
  
IF EXISTS (SELECT name FROM sys.tables  
    WHERE name = N'xDimProduct'  
    AND object_id = OBJECT_ID (N'xDimProduct'))  
DROP TABLE xDimProduct;  
  
--Create a distributed table with a clustered index.  
CREATE TABLE xDimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey)  
WITH ( DISTRIBUTION = HASH(ProductKey),  
    CLUSTERED INDEX (ProductKey) )  
AS SELECT ProductKey, ProductAlternateKey, ProductSubcategoryKey FROM DimProduct;  
  
--Change the existing clustered index   
--to a clustered columnstore index with the same name.  
--Look up the name of the index before running this statement.  
CREATE CLUSTERED COLUMNSTORE INDEX <index_name>   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="b-rebuild-a-clustered-columnstore-index"></a>B. Volver a generar un índice de almacén de columnas agrupado  
 Basándose en el ejemplo anterior, en este ejemplo se utiliza CREATE CLUSTERED COLUMNSTORE INDEX para volver a generar el índice de almacén de columnas agrupado existente denominado cci_xDimProduct.  
  
```  
--Rebuild the existing clustered columnstore index.  
CREATE CLUSTERED COLUMNSTORE INDEX cci_xDimProduct   
ON xdimProduct   
WITH ( DROP_EXISTING = ON );  
```  
  
### <a name="c-change-the-name-of-a-clustered-columnstore-index"></a>C. Cambiar el nombre de un índice de almacén de columnas agrupado  
 Para cambiar el nombre de un índice de almacén de columnas agrupado, quite el índice de almacén de columnas clúster existente y, a continuación, vuelva a crear el índice con un nuevo nombre.  
  
 Se recomienda sólo realizando esta operación con una tabla pequeña o una tabla vacía. Tarda mucho tiempo para quitar un índice de almacén de columnas agrupado grandes y volver a generar con un nombre diferente.  
  
 Con el índice de almacén de columnas agrupado cci_xDimProduct del ejemplo anterior, en este ejemplo se quita el índice de almacén de columnas agrupado cci_xDimProduct y, a continuación, vuelve a crear el índice de almacén de columnas agrupado con el nombre mycci_xDimProduct.  
  
```  
--For illustration purposes, drop the clustered columnstore index.   
--The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xDimProduct;  
  
--Create a clustered index with a new name, mycci_xDimProduct.  
CREATE CLUSTERED COLUMNSTORE INDEX mycci_xDimProduct  
ON xdimProduct  
WITH ( DROP_EXISTING = OFF );  
```  
  
### <a name="d-convert-a-columnstore-table-to-a-rowstore-table-with-a-clustered-index"></a>D. Convertir una tabla de almacén de columnas en una tabla de almacén de filas con un índice clúster  
 Puede haber una situación que desea quitar un índice de almacén de columnas agrupado y crear un índice agrupado. La tabla se almacena en formato de almacén de filas. Este ejemplo convierte una tabla de almacén de columnas en una tabla de almacén de filas con un índice clúster con el mismo nombre. Ninguno de los datos se pierde. Todos los datos que se va a la tabla de almacén de filas y las columnas enumeradas se convierte en las columnas de clave en el índice agrupado.  
  
```  
--Drop the clustered columnstore index and create a clustered rowstore index.   
--All of the columns are stored in the rowstore clustered index.   
--The columns listed are the included columns in the index.  
CREATE CLUSTERED INDEX cci_xDimProduct    
ON xdimProduct (ProductKey, ProductAlternateKey, ProductSubcategoryKey, WeightUnitMeasureCode)  
WITH ( DROP_EXISTING = ON);  
  
```  
  
### <a name="e-convert-a-columnstore-table-back-to-a-rowstore-heap"></a>E. Convertir una tabla de almacén de columnas en un montón de almacén de filas  
 Use [DROP INDEX (SQL Server PDW)](http://msdn.microsoft.com/en-us/f59cab43-9f40-41b4-bfdb-d90e80e9bf32) para quitar el índice de almacén de columnas agrupado y convertir la tabla en un montón de almacén de filas. En este ejemplo se convierte en la tabla cci_xDimProduct en un montón de almacén de filas. La tabla sigue distribuirse, pero se almacena como un montón.  
  
```  
--Drop the clustered columnstore index. The table continues to be distributed, but changes to a heap.  
DROP INDEX cci_xdimProduct ON xdimProduct;  
```  


