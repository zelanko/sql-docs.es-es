---
title: Sys. dm_db_xtp_hash_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2bbaaaa6770c5644da227c7e64a9ff9e0fc2c13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68026840"
---
# <a name="sysdm_db_xtp_hash_index_stats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Estas estadísticas son útiles para entender y optimizar el número de depósitos. También se pueden utilizar para detectar los casos donde la clave de índice tiene muchos duplicados.  
  
 Una longitud promedio grande de la cadena indica que se aplica el algoritmo hash a muchas filas para el mismo cubo. Esto puede deberse a que:  
  
-   Si el número de depósitos vacíos es bajo o las longitudes de cadena promedio y máxima son similares, es probable que el número total de depósitos sea demasiado bajo. Esto hace que la aplicación del algoritmo hash a muchas claves de índice distintas dé como resultado el mismo cubo.  
  
-   Si el número de cubos vacíos es alto o la longitud de cadena máxima es alta en comparación con la longitud de cadena promedio, es probable que haya muchas filas con valores de clave de índice duplicados o que haya una asimetría en los valores de clave. Cuando se aplica el algoritmo hash a todas las filas que tienen el mismo valor de clave de índice se obtiene el mismo cubo, por lo que hay una longitud de cadena larga en ese cubo.  
  
Las longitudes de cadena largas pueden afectar significativamente al rendimiento de las operaciones DML en filas individuales, incluidas SELECT e INSERT. Las longitudes de cadena cortas, junto con un gran número de depósitos vacíos, indican que hay un bucket_count con un valor demasiado alto. Esto reduce el rendimiento de los exámenes de índice.  
  
> [!WARNING]
> **Sys. dm_db_xtp_hash_index_stats** examina toda la tabla. Por lo tanto, si hay tablas grandes en la base de datos, **Sys. dm_db_xtp_hash_index_stats** puede tardar mucho tiempo en ejecutarse.  
  
Para obtener más información, vea [índices de hash para tablas optimizadas para memoria](../../relational-databases/sql-server-index-design-guide.md#hash_index).  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|object_id|**int**|Identificador del objeto de la tabla primaria.|  
|xtp_object_id|**BIGINT**|IDENTIFICADOR de la tabla optimizada para memoria.|  
|index_id|**int**|El identificador de índice.|  
|total_bucket_count|**BIGINT**|El número total de cubos de hash del índice.|  
|empty_bucket_count|**BIGINT**|El número de cubos de hash vacíos del índice.|  
|avg_chain_length|**BIGINT**|La longitud promedio de las cadenas de filas sobre todos los cubos de hash del índice.|  
|max_chain_length|**BIGINT**|La longitud máxima de las cadenas de filas de los cubos de hash.|  
|xtp_object_id|**BIGINT**|IDENTIFICADOR de objeto de OLTP en memoria que corresponde a la tabla optimizada para memoria.|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  

## <a name="examples"></a>Ejemplos  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. Solución de problemas de número de cubos de índice de hash

La siguiente consulta se puede usar para solucionar problemas del número de cubos de índice de hash de una tabla existente. La consulta devuelve estadísticas sobre el porcentaje de cubos vacíos y la longitud de cadena de todos los índices de hash de las tablas de usuario.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

Para obtener más información sobre cómo interpretar los resultados de esta consulta, vea [solución de problemas de índices de hash para tablas optimizadas para memoria](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) .  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. Estadísticas de índice de hash para tablas internas

Ciertas características usan tablas internas que aprovechan los índices de hash, por ejemplo, los índices de almacén de columnas en las tablas optimizadas para memoria. La siguiente consulta devuelve estadísticas para los índices hash de las tablas internas que están vinculadas a las tablas de usuario.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

Tenga en cuenta que el BUCKET_COUNT del índice en las tablas internas no se puede cambiar, por lo que la salida de esta consulta debe considerarse solo informativa. no se requiere ninguna acción.  

No se espera que esta consulta devuelva ninguna fila a menos que esté usando una característica que aprovecha los índices de hash en las tablas internas. La siguiente tabla optimizada para memoria contiene un índice de almacén de columnas. Después de crear esta tabla, verá los índices de hash en las tablas internas.

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de tablas optimizadas para memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
