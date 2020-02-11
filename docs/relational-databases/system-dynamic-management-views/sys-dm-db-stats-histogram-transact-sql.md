---
title: Sys. dm_db_stats_histogram (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_stats_histogram
- sys.dm_db_stats_histogram_TSQL
- dm_db_stats_histogram
- dm_db_stats_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_histogram dynamic management function
ms.assetid: 1897fd4a-8d51-461e-8ef2-c60be9e563f2
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e5a79a4ab38fd1cb7d118624fd170219aa90a94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096253"
---
# <a name="sysdm_db_stats_histogram-transact-sql"></a>sys.dm_db_stats_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Devuelve el histograma de estadísticas para el objeto de base de datos especificado (tabla o vista indizada) en la base de datos actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Similar a `DBCC SHOW_STATISTICS WITH HISTOGRAM`.

> [!NOTE] 
> Esta DMF está disponible a partir [!INCLUDE[ssSQL15](../../includes/ssSQL15-md.md)] de SP1 Cu2

## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_db_stats_histogram (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Es el identificador del objeto en la base de datos actual para el que se han solicitado propiedades de una de sus estadísticas. *object_id* es de **tipo int**.  
  
 *stats_id*  
 Es el identificador de estadísticas para el *object_id*especificado. El identificador de estadísticas se puede obtener desde la vista de administración dinámica [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) . *stats_id* es de **tipo int**.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id |**int**|Identificador del objeto (tabla o vista indizada) para el que se devuelven las propiedades del objeto de estadísticas.|  
|stats_id |**int**|Identificador del objeto de estadísticas. Es único dentro de la vista indizada o la tabla. Para obtener más información, vea [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|  
|step_number |**int** |Número de pasos del histograma. |
|range_high_key |**sql_variant** |Valor de columna límite superior de un paso del histograma. El valor de columna también se denomina valor de clave.|
|range_rows |**impuestos** |Número calculado de filas cuyo valor de columna está comprendido en un paso del histograma, sin incluir el límite superior. |
|equal_rows |**impuestos** |Número calculado de filas cuyo valor de columna es igual al límite superior del paso del histograma. |
|distinct_range_rows |**BIGINT** |Número calculado de filas que tienen un valor de columna distinto en un paso del histograma, sin incluir el límite superior. |
|average_range_rows |**impuestos** |Número promedio de filas con valores de columna duplicados dentro de un paso del histograma, excluido el límite superior (`RANGE_ROWS / DISTINCT_RANGE_ROWS` para `DISTINCT_RANGE_ROWS > 0`). |
  
 ## <a name="remarks"></a>Observaciones  
 
 El conjunto de `sys.dm_db_stats_histogram` resultados de devuelve información `DBCC SHOW_STATISTICS WITH HISTOGRAM` similar a y `object_id`también `stats_id`incluye, `step_number`y.

 Dado que la `range_high_key` columna es un tipo de datos sql_variant, puede que tenga `CAST` que `CONVERT` usar o si un predicado realiza una comparación con una constante que no es de cadena.

### <a name="histogram"></a>Histograma
  
 Un histograma mide la frecuencia de aparición de cada valor distinto en un conjunto de datos. El optimizador de consultas calcula un histograma de los valores de la primera columna de clave del objeto de estadísticas; para ello, selecciona los valores de la columna tomando una muestra estadística de las filas o realizando un análisis completo de todas las filas de la tabla o vista. Si el histograma se crea a partir de muestras de un conjunto de filas, los totales almacenados para el número de filas y el número de valores distintos son las estimaciones y no es necesario que sean números enteros.  
  
 Para crear el histograma, el optimizador de consultas ordena los valores de columna, calcula el número de valores que coinciden con cada valor de columna distinto y, a continuación, agrupa los valores de columna en un máximo de 200 pasos de histograma contiguos. Cada paso incluye un intervalo de valores de columna seguido de un valor de columna de límite superior. El intervalo incluye todos los valores de columna posibles comprendidos entre los valores límite (sin incluir los propios valores límite). El valor de columna ordenado más pequeño es el valor del límite superior del primer paso del histograma.  
  
 En el diagrama siguiente se muestra un histograma con seis pasos. El área a la izquierda del primer valor límite superior es el primer paso.  
  
 ![](../../relational-databases/system-dynamic-management-views/media/histogram_2.gif "Histogram")  
  
 En cada paso del histograma:  
  
-   La línea gruesa representa el valor de límite superior (*range_high_key*) y el número de veces que tiene lugar (*equal_rows*).  
  
-   El área de color sólido situada a la izquierda de *range_high_key* representa el rango de valores de columna y el número medio de veces que tiene lugar cada valor de columna (*average_range_rows*). El valor de *average_range_rows* en el primer paso del histograma siempre es 0.  
  
-   Las líneas de puntos representan los valores muestreados que se utilizan para estimar el número total de valores distintos en el intervalo (*distinct_range_rows*) y el número total de valores del intervalo (*range_rows*). El optimizador de consultas utiliza *range_rows* y *distinct_range_rows* para calcular *average_range_rows* y no almacena los valores de las muestras.  
  
 El optimizador de consultas define los pasos del histograma en función de su importancia estadística. Utiliza un algoritmo de diferencias máximas para minimizar el número de pasos del histograma a la vez que minimiza las diferencias entre los valores límite. El número máximo de pasos es 200. El número de pasos del histograma puede ser menor que el número de valores distintos, incluso para las columnas con menos de 200 puntos de límite. Por ejemplo, una columna con 100 valores distintos puede tener un histograma con menos de 100 puntos de límite.  
  
## <a name="permissions"></a>Permisos  

Necesita que el usuario tenga permisos de selección en columnas de estadísticas o posea la tabla, o que el usuario sea miembro del rol fijo de servidor `sysadmin`, del rol fijo de base de datos `db_owner` o del rol fijo de base de datos `db_ddladmin`.

## <a name="examples"></a>Ejemplos  

### <a name="a-simple-example"></a>A. Ejemplo sencillo    
En el ejemplo siguiente se crea y rellena una tabla simple. Después crea las estadísticas en `Country_Name` la columna.

```sql
CREATE TABLE Country
(Country_ID int IDENTITY PRIMARY KEY,
Country_Name varchar(120) NOT NULL);
INSERT Country (Country_Name) VALUES ('Canada'), ('Denmark'), ('Iceland'), ('Peru');

CREATE STATISTICS Country_Stats  
    ON Country (Country_Name) ;  
```   
La clave principal ocupa `stat_id` el número 1, por `sys.dm_db_stats_histogram` lo `stat_id` que debe llamar a para el número 2 para devolver `Country` el histograma de estadísticas de la tabla.    
```sql     
SELECT * FROM sys.dm_db_stats_histogram(OBJECT_ID('Country'), 2);
```

### <a name="b-useful-query"></a>B. Consulta útil:   
```sql  
SELECT hist.step_number, hist.range_high_key, hist.range_rows, 
    hist.equal_rows, hist.distinct_range_rows, hist.average_range_rows
FROM sys.stats AS s
CROSS APPLY sys.dm_db_stats_histogram(s.[object_id], s.stats_id) AS hist
WHERE s.[name] = N'<statistic_name>';
```

### <a name="c-useful-query"></a>C. Consulta útil:
En el ejemplo siguiente se selecciona `Country` de la tabla con un `Country_Name`predicado en la columna.

```sql  
SELECT * FROM Country 
WHERE Country_Name = 'Canada';
```

En el ejemplo siguiente se examina la estadística creada anteriormente en `Country` la tabla `Country_Name` y la columna para el paso del histograma que coincide con el predicado de la consulta anterior.

```sql  
SELECT ss.name, ss.stats_id, shr.steps, shr.rows, shr.rows_sampled, 
    shr.modification_counter, shr.last_updated, sh.range_rows, sh.equal_rows
FROM sys.stats ss
INNER JOIN sys.stats_columns sc 
    ON ss.stats_id = sc.stats_id AND ss.object_id = sc.object_id
INNER JOIN sys.all_columns ac 
    ON ac.column_id = sc.column_id AND ac.object_id = sc.object_id
CROSS APPLY sys.dm_db_stats_properties(ss.object_id, ss.stats_id) shr
CROSS APPLY sys.dm_db_stats_histogram(ss.object_id, ss.stats_id) sh
WHERE ss.[object_id] = OBJECT_ID('Country') 
    AND ac.name = 'Country_Name'
    AND sh.range_high_key = CAST('Canada' AS CHAR(8));
```
  
## <a name="see-also"></a>Consulte también  
[DBCC SHOW_STATISTICS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
[Funciones y vistas de administración dinámica relacionadas con objetos (Transact-SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
