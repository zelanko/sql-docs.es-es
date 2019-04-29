---
title: sys.indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f65371e31362524a5a909d1fdda4a047b2525966
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004243"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por índice o montón de un objeto tabular, como una tabla, una vista o una función con valores de tabla.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. del objeto al que pertenece este índice.|  
|**Nombre**|**sysname**|Nombre del índice. **nombre** es único solo dentro del objeto.<br /><br /> NULL = Montón|  
|**index_id**|**int**|Id. del índice. **index_id** es único solo dentro del objeto.<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster<br /><br /> > 1 = índice no clúster|  
|**Tipo**|**tinyint**|Tipo de índice:<br /><br /> 0 = Montón<br /><br /> 1 = Clúster<br /><br /> 2 = No clúster<br /><br /> 3 = XML<br /><br /> 4 = Espacial<br /><br /> 5 = índice clúster de almacén de columnas. **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 6 = índice no agrupado de almacén de columnas. **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 7 = índice hash no clúster. **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> Almacén de columnas agrupado - **se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Almacén de columnas no agrupado - **se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> HASH NO CLÚSTER: Los índices NONCLUSTERED HASH solo se admiten en tablas optimizadas para memoria. La vista sys.hash_indexes muestra los índices hash actuales y las propiedades hash. Para obtener más información, consulte [sys.hash_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md). **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_unique**|**bit**|1 = El índice es exclusivo.<br /><br /> 0 = El índice no es exclusivo.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**data_space_id**|**int**|Id. del espacio de datos para este índice. El espacio de datos es un grupo de archivos o un esquema de partición.<br /><br /> 0 = **object_id** es una función con valores de tabla o índice en memoria.|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY está ON.<br /><br /> 0 = IGNORE_DUP_KEY está OFF.|  
|**is_primary_key**|**bit**|1 = El índice forma parte de una restricción PRIMARY KEY.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**is_unique_constraint**|**bit**|1 = El índice forma parte de una restricción UNIQUE.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**fill_factor**|**tinyint**|> 0 = porcentaje de FILLFACTOR utilizado al crear o volver a generar el índice.<br /><br /> 0 = Valor predeterminado<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**is_padded**|**bit**|1 = PADINDEX está ON.<br /><br /> 0 = PADINDEX está OFF.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**is_disabled**|**bit**|1 = El índice está deshabilitado.<br /><br /> 0 = El índice no está deshabilitado.|  
|**is_hypothetical**|**bit**|1 = El índice es hipotético y no se puede utilizar directamente como ruta de acceso a datos. Los índices hipotéticos contienen estadísticas de nivel de columna.<br /><br /> 0 = El índice no es hipotético.|  
|**allow_row_locks**|**bit**|1 = El índice admite bloqueos de fila.<br /><br /> 0 = El índice no admite bloqueos de fila.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**allow_page_locks**|**bit**|1 = El índice admite bloqueos de página.<br /><br /> 0 = El índice no admite bloqueos de página.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**has_filter**|**bit**|1 = El índice tiene un filtro y solo contiene filas que cumplen con la definición del filtro.<br /><br /> 0 = El índice no tiene un filtro.|  
|**filter_definition**|**nvarchar(max)**|Expresión para el subconjunto de filas incluido en el índice filtrado.<br /><br /> NULL para el montón o el índice no filtrado.|  
|**auto_created**|**bit**|1 = índice se creó mediante el ajuste automático.<br /><br />0 = índice creado por el usuario.
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los índices para la tabla `Production.Product` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
