---
title: Sys.dm_db_partition_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_partition_stats
- dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_partition_stats dynamic management view
ms.assetid: 9db9d184-b3a2-421e-a804-b18ebcb099b7
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d59bf08d70a59dedae4ae940c810d70dba0f6c4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbpartitionstats-transact-sql"></a>sys.dm_db_partition_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información de página y recuento de filas de cada partición en la base de datos actual.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_db_partition_stats**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Id. de la partición. Es único en la base de datos. Este es el mismo valor que el **partition_id** en el **sys.partitions** vista de catálogo|  
|**object_id**|**int**|Id. de objeto de la tabla o vista indizada de la que esta partición forma parte.|  
|**index_id**|**int**|Id. del montón o índice del que esta partición forma parte.<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster.<br /><br /> > 1 = Índice no clúster|  
|**partition_number**|**int**|Número de partición en base 1 en el índice o montón.|  
|**in_row_data_page_count**|**bigint**|Número de páginas en uso para almacenar datos consecutivos en esta partición. Si la partición forma parte de un montón, el valor es el número de páginas de datos en el montón. Si la partición forma parte de un índice, el valor es el número de páginas en el nivel hoja. (Las páginas no hojas en B-tree no están incluidas en el recuento.) En cualquier caso, las páginas IAM (Mapa de asignación de índices) no están incluidas. Siempre es 0 para un índice de almacén de columnas optimizado de memoria xVelocity.|  
|**in_row_used_page_count**|**bigint**|Número total de páginas en uso para almacenar y administrar datos consecutivos en esta partición. Este recuento incluye páginas de árbol B no hoja, páginas IAM y todas las páginas incluidas en el **in_row_data_page_count** columna. Siempre es 0 para un índice de almacén de columnas.|  
|**in_row_reserved_page_count**|**bigint**|Número total de páginas reservadas para almacenar y administrar datos consecutivos en esta partición, independientemente de si las páginas están en uso o no. Siempre es 0 para un índice de almacén de columnas.|  
|**lob_used_page_count**|**bigint**|Número de páginas en uso para almacenar y administrar fuera de la fila **texto**, **ntext**, **imagen**, **varchar (max)**, **nvarchar (max)** , **varbinary (max)**, y **xml** columnas dentro de la partición. Las páginas IAM están incluidas.<br /><br /> Número total de LOBs utilizados para almacenar y administrar el índice de almacén de columnas en la partición.|  
|**lob_reserved_page_count**|**bigint**|Número total de páginas reservadas para almacenar y administrar fuera de la fila **texto**, **ntext**, **imagen**, **varchar (max)**,  **nvarchar (max)**, **varbinary (max)**, y **xml** columnas dentro de la partición, independientemente de si las páginas están en uso o no. Las páginas IAM están incluidas.<br /><br /> Número total de LOBs reservados para almacenar y administrar un índice de almacén de columnas en la partición.|  
|**row_overflow_used_page_count**|**bigint**|Número de páginas en uso para almacenar y administrar el desbordamiento de fila **varchar**, **nvarchar**, **varbinary**, y **sql_variant** columnas en la partición. Las páginas IAM están incluidas.<br /><br /> Siempre es 0 para un índice de almacén de columnas.|  
|**row_overflow_reserved_page_count**|**bigint**|Número total de páginas reservadas para almacenar y administrar el desbordamiento de fila **varchar**, **nvarchar**, **varbinary**, y **sql_variant** columnas en la partición, independientemente de si las páginas están en uso o no. Las páginas IAM están incluidas.<br /><br /> Siempre es 0 para un índice de almacén de columnas.|  
|**used_page_count**|**bigint**|Número total de páginas usadas para la partición. Se calcula como **in_row_used_page_count** + **lob_used_page_count** + **row_overflow_used_page_count**.|  
|**reserved_page_count**|**bigint**|Número total de páginas reservadas para la partición. Se calcula como **in_row_reserved_page_count** + **lob_reserved_page_count** + **row_overflow_reserved_page_count**.|  
|**row_count**|**bigint**|Número aproximado de filas de la partición.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
|**distribution_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador numérico único asociado con la distribución.|  
  
## <a name="remarks"></a>Comentarios  
 **Sys.dm_db_partition_stats** muestra información sobre el espacio utilizado para almacenar y administrar datos en la fila de datos LOB y datos de desbordamiento de fila de todas las particiones en una base de datos. Se muestra una fila por partición.  
  
 Los recuentos en los que se basa el resultado se almacenan en caché en memoria o se almacenan en disco en varias tablas del sistema.  
  
 Los datos consecutivos, datos LOB y datos de desbordamiento de fila representan las tres unidades de asignación que forman una partición. El [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) se puede consultar la vista de catálogo para metadatos acerca de cada unidad de asignación en la base de datos.  
  
 Si un montón o un índice no tiene particiones, entonces consta de una partición (con el número de partición = 1); por tanto, solo se devuelve una fila para ese montón o índice. El [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) se puede consultar la vista de catálogo para metadatos acerca de cada partición de todas las tablas e índices en una base de datos.  
  
 El recuento total de cada tabla o índice se puede obtener agregando los recuentos de todas las particiones relacionadas.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW DATABASE STATE para consultar el **sys.dm_db_partition_stats** vista de administración dinámica. Para obtener más información acerca de los permisos en las vistas de administración dinámica, consulte [funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>A. Devolver todos los recuentos de todas las particiones de todos los índices y montones en una base de datos  
 En el siguiente ejemplo se muestran todos los recuentos de todas las particiones de todos los índices y montones en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>B. Devolver todos los recuentos de todas las particiones de una tabla y sus índices  
 En el siguiente ejemplo se muestran todos los recuentos de todas las particiones de la tabla `HumanResources.Employee` y sus índices.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>C. Devolver el número total de páginas usadas y el número total de filas de un montón o índice clúster  
 En el siguiente ejemplo se devuelve el número total de páginas usadas y el número total de filas del montón o índice clúster de la tabla `HumanResources.Employee`. Puesto que la tabla `Employee` no tiene particiones de forma predeterminada, observe que la suma solo incluye una partición.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


