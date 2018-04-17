---
title: Sys.pdw_nodes_partitions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 94f7ab8cb379c2147446b67d9865e8ad415dcf84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodespartitions-transact-sql"></a>Sys.pdw_nodes_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada partición de todas las tablas y la mayoría de los tipos de índices en una [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] base de datos. Todas las tablas e índices contienen al menos una partición, si se crean particiones de forma explícita.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|partition_id|`bigint`|identificador de la partición. Es único en una base de datos.|  
|object_id|`int`|Id. del objeto al que pertenece esta partición. Todas las tablas o vistas se componen al menos de una partición.|  
|index_id|`int`|Id. del índice dentro del objeto al que pertenece esta partición.|  
|partition_number|`int`|Número de partición basado en uno en el índice o el montón propietario. Para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], el valor de esta columna es 1.|  
|hobt_id|`bigint`|Id. del montón de datos o el árbol b que contiene las filas de esta partición.|  
|rows|`bigint`|Número aproximado de filas de esta partición. |  
|data_compression|`int`|Indica el estado de compresión para cada partición:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|`nvarchar(60)`|Indica el estado de compresión para cada partición. Los valores posibles son NONE, ROW y PAGE.|  
|pdw_node_id|`int`|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>Ejemplo A: filas de la presentación en cada partición dentro de cada distribución 

Se aplica a: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
Para mostrar el número de filas de cada partición dentro de cada distribución, utilice [DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) .

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>Ejemplo B: vistas del sistema de usos para ver las filas de cada partición de cada distribución de una tabla

Se aplica a: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
Esta consulta devuelve el número de filas de cada partición de cada distribución de la tabla `myTable`.  
 
```  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

