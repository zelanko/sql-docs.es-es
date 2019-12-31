---
title: Sys. Indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d4d307ea18127586ac46b0f6afb973ef62cf6ba
ms.sourcegitcommit: ede04340adbf085e668a2536d4f7114abba14a0c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761484"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por índice o montón de un objeto tabular, como una tabla, una vista o una función con valores de tabla.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**Inter**|Id. del objeto al que pertenece este índice.|  
|**Name**|**sysname**|Nombre del índice. **Name** es único solo dentro del objeto.<br /><br /> NULL = Montón|  
|**index_id**|**Inter**|Id. del índice. **index_id** es único solo dentro del objeto.<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster<br /><br /> > 1 = Índice no clúster|  
|**automáticamente**|**tinyint**|Tipo de índice:<br /><br /> 0 = Montón<br /><br /> 1 = Clúster<br /><br /> 2 = No clúster<br /><br /> 3 = XML<br /><br /> 4 = Espacial<br /><br /> 5 = índice clúster de almacén de columnas. **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.<br /><br /> 6 = índice de almacén de columnas no agrupado. **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> 7 = Índice de hash no clúster. **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.|  
|**type_desc**|**nvarchar (60)**|Descripción del tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> Almacén de columnas en clúster: **se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.<br /><br /> Almacén de columnas no agrupado: **se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> HASH no AGRUPAdo: los índices de HASH no clúster solo se admiten en tablas optimizadas para memoria. La vista sys.hash_indexes muestra los índices hash actuales y las propiedades hash. Para obtener más información, vea [Sys. hash_indexes &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md). **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.|  
|**is_unique**|**poco**|1 = El índice es exclusivo.<br /><br /> 0 = El índice no es exclusivo.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**data_space_id**|**Inter**|Id. del espacio de datos para este índice. El espacio de datos es un grupo de archivos o un esquema de partición.<br /><br /> 0 = **object_id** es una función con valores de tabla o un índice en memoria.|  
|**ignore_dup_key**|**poco**|1 = IGNORE_DUP_KEY está ON.<br /><br /> 0 = IGNORE_DUP_KEY está OFF.|  
|**is_primary_key**|**poco**|1 = El índice forma parte de una restricción PRIMARY KEY.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**is_unique_constraint**|**poco**|1 = El índice forma parte de una restricción UNIQUE.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**fill_factor**|**tinyint**|> 0 = porcentaje de FILLFACTOR utilizado al crear o volver a generar el índice.<br /><br /> 0 = Valor predeterminado<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**is_padded**|**poco**|1 = PADINDEX está ON.<br /><br /> 0 = PADINDEX está OFF.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**is_disabled**|**poco**|1 = El índice está deshabilitado.<br /><br /> 0 = El índice no está deshabilitado.|  
|**is_hypothetical**|**poco**|1 = El índice es hipotético y no se puede utilizar directamente como ruta de acceso a datos. Los índices hipotéticos contienen estadísticas de nivel de columna.<br /><br /> 0 = El índice no es hipotético.|  
|**allow_row_locks**|**poco**|1 = El índice admite bloqueos de fila.<br /><br /> 0 = El índice no admite bloqueos de fila.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**allow_page_locks**|**poco**|1 = El índice admite bloqueos de página.<br /><br /> 0 = El índice no admite bloqueos de página.<br /><br /> Siempre es 0 para los índices clúster de almacén de columnas.|  
|**has_filter**|**poco**|1 = El índice tiene un filtro y solo contiene filas que cumplen con la definición del filtro.<br /><br /> 0 = El índice no tiene un filtro.|  
|**filter_definition**|**nvarchar (Max)**|Expresión para el subconjunto de filas incluido en el índice filtrado.<br /><br /> NULL para el montón o el índice no filtrado.|  
|**auto_created**|**poco**|1 = el ajuste automático creó el índice.<br /><br />0 = el usuario creó el índice.
|**optimize_for_sequential_key**|**poco**|1 = el índice tiene habilitada la optimización de la última página.<br><br>0 = valor predeterminado. El índice tiene deshabilitada la optimización de la última página.|

> [!NOTE]
> El bit de **optimize_for_sequential_key** solo se admite en las versiones SQL Server 2019 CTP 3,1 y versiones posteriores.
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Para obtener más información, vea [configuración de visibilidad de metadatos](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelven todos los `Production.Product` índices de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] la tabla en la base de datos.  
  
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
  
## <a name="see-also"></a>Véase también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys. index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Sys. xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [Sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [Sys. grupos de archivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys. partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Preguntas más frecuentes sobre el catálogo del sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [&#40;de optimización en memoria de OLTP en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
