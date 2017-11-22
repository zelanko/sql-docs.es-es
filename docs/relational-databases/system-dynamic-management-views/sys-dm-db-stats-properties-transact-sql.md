---
title: Sys.dm_db_stats_properties (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_stats_properties_TSQL
- sys.dm_db_stats_properties
- dm_db_stats_properties_TSQL
- dm_db_stats_properties
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_stats_properties
ms.assetid: 8a54889d-e263-4881-9fcb-b1db410a9453
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e2a1ebc3301372b490de9ec631c3cdb0743f264b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbstatsproperties-transact-sql"></a>sys.dm_db_stats_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve propiedades de estadísticas para el objeto de base de datos especificado (tabla o vista indizada) en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual. Para las tablas con particiones, vea el similar [sys.dm_db_incremental_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md). 
 
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_db_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Es el identificador del objeto en la base de datos actual para el que se han solicitado propiedades de una de sus estadísticas. *object_id* es **int**.  
  
 *stats_id*  
 Es el identificador de estadísticas para el *object_id*especificado. El identificador de estadísticas se puede obtener desde la vista de administración dinámica [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) . *stats_id* es **int**.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Identificador del objeto (tabla o vista indizada) para el que se devuelven las propiedades del objeto de estadísticas.|  
|stats_id|**int**|Identificador del objeto de estadísticas. Es único dentro de la vista indizada o la tabla. Para obtener más información, vea [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|  
|last_updated|**datetime2**|Fecha y hora de la última actualización del objeto de estadísticas.|  
|rows|**bigint**|Número total de filas que tenía la tabla o la vista indizada la última vez que se actualizaron las estadísticas. Si las estadísticas se filtran o corresponden a un índice filtrado, el número de filas puede ser inferior al número de filas de la tabla.|  
|rows_sampled|**bigint**|Número total de filas muestreadas para cálculos de estadísticas.|  
|pasos|**int**|Número de pasos del histograma. Para obtener más información, vea [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)no incluye la vista.|  
|unfiltered_rows|**bigint**|Número total de filas de la tabla antes de aplicar la expresión de filtro (para estadísticas filtradas). Si las estadísticas no están filtradas, unfiltered_rows es igual al valor devuelto en la columna rows.|  
|modification_counter|**bigint**|Número total de modificaciones para la columna de estadísticas iniciales (la columna en la que se ha generado el histograma) desde la última vez que se actualizaron las estadísticas.<br /><br /> Tablas optimizadas en memoria: iniciando [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] esta columna contiene: número total de modificaciones de la tabla desde que se actualizaron las estadísticas de tiempo de último o se ha reiniciado la base de datos.|  
|persisted_sample_percent|**float**|Conserva el porcentaje de ejemplo que se usan para las actualizaciones de estadísticas que no especifican explícitamente un porcentaje de muestreo. Si el valor es cero, no hay ningún porcentaje de ejemplo persistente se establece para esta estadística.<br /><br /> **Se aplica a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4|  
  
## <a name="remarks"></a>Comentarios  
 **Sys.dm_db_stats_properties** devuelve un conjunto de filas vacío en cualquiera de las condiciones siguientes:  
  
-   **object_id** o **stats_id** es NULL.  
  
-   El objeto especificado no se encuentra o no corresponde a una vista indizada o a una tabla.  
  
-   El identificador de estadísticas especificado no se corresponde con las estadísticas existentes para el identificador de objeto especificado.  
  
-   El usuario actual no tiene permisos para ver el objeto de estadísticas.  
  
 Este comportamiento permite el uso seguro de **sys.dm_db_stats_properties** cuando entre aplicado a las filas en las vistas como **sys.objects** y **sys.stats**.  
  
## <a name="permissions"></a>Permissions  
 Necesita que el usuario tenga permisos de selección en columnas de estadísticas o posea la tabla, o que el usuario sea miembro del rol fijo de servidor `sysadmin`, del rol fijo de base de datos `db_owner` o del rol fijo de base de datos `db_ddladmin`.  
  
## <a name="examples"></a>Ejemplos  

### <a name="a-simple-example"></a>A. Ejemplo sencillo
El ejemplo siguiente devuelve las estadísticas para el `Person.Person` tabla en la base de datos de AdventureWorks.

```
SELECT * FROM sys.dm_db_stats_properties (object_id('Person.Person'), 1);
``` 
  
### <a name="b-returning-all-statistics-properties-for-a-table"></a>B. Devolver propiedades de todas las estadísticas de una tabla  
 En el ejemplo siguiente se devuelven propiedades de todas las estadísticas que existen para la tabla TEST.  
  
```  
SELECT sp.stats_id, name, filter_definition, last_updated, rows, rows_sampled, steps, unfiltered_rows, modification_counter   
FROM sys.stats AS stat   
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE stat.object_id = object_id('TEST');  
```  
  
### <a name="c-returning-statistics-properties-for-frequently-modified-objects"></a>C. Devolver propiedades de estadísticas para objetos modificados frecuentemente  
 En el ejemplo siguiente se devuelven todas las tablas, vistas indizadas y estadísticas de la base de datos actual para las que la columna inicial se modificó más de 1000 veces desde la última actualización de estadísticas.  
  
```  
SELECT obj.name, obj.object_id, stat.name, stat.stats_id, last_updated, modification_counter  
FROM sys.objects AS obj   
INNER JOIN sys.stats AS stat ON stat.object_id = obj.object_id  
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE modification_counter > 1000;  
```  
  
## <a name="see-also"></a>Vea también  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Funciones y vistas de administración dinámica relacionada con objetos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [Sys.dm_db_incremental_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)  
 [Sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  

