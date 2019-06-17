---
title: sys.dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1460ef53098a9cdd7cf8bb1672c45cfd27adff57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822737"
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Proporciona información de nivel de grupo de filas actual acerca de todos los índices de almacén de columnas de la base de datos actual.  
  
 Este comando extiende la vista de catálogo [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla subyacente.|  
|**index_id**|**int**|Id. de este índice de almacén de columnas en *object_id* tabla.|  
|**partition_number**|**int**|Identificador de la partición de tabla que contiene *row_group_id*. Puede utilizar partition_number para unir esta DMV a sys.partitions.|  
|**row_group_id**|**int**|Id. de este grupo de filas. Para las tablas con particiones, es único dentro de la partición.<br /><br /> -1 para una cola en memoria.|  
|**delta_store_hobt_id**|**bigint**|El hobt_id para un grupo de filas en el almacén delta.<br /><br /> Es NULL si el grupo de filas no está en el almacén delta.<br /><br /> NULL para el final de una tabla en memoria.|  
|**state**|**tinyint**|Número de identificación asociado *state_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = OBJETO DE DESECHO<br /><br /> COMPRESSED es el único estado que se aplica a tablas en memoria.|  
|**state_desc**|**nvarchar(60)**|Descripción del estado del grupo de fila:<br /><br /> INVISIBLE: un grupo de filas que se está compilando. Por ejemplo: <br />Un grupo de filas del almacén de columnas es INVISIBLE, mientras que los datos se comprimen. Cuando finaliza la compresión de los cambios de un conmutador de metadatos el estado de la fila del almacén de columnas de grupo de INVISIBLE comprimida y el estado del grupo de filas almacén delta de cerrado a objetos de DESECHO.<br /><br /> Abra - un grupo de filas de almacén delta que se acepta filas nuevas. Un grupo de filas abierto está todavía en formato de almacén de filas y no se ha comprimido al formato de almacén de columnas.<br /><br /> CERRADO: un grupo de filas en el almacén delta que contiene el número máximo de filas y está esperando el proceso de tupla motriz comprimirlo en el almacén de columnas.<br /><br /> COMPRIMIR - un grupo de filas que se comprimió con compresión de almacén de columnas y se almacenan en el almacén de columnas.<br /><br /> Marcador de exclusión - un grupo de filas que se encontraba anteriormente en el almacén delta y ya no utiliza.|  
|**total_rows**|**bigint**|Número de filas físicas almacenado en el grupo de filas. Para los grupos de filas comprimido, esto incluye las filas que se marcan eliminadas.|  
|**deleted_rows**|**bigint**|Número de filas almacenadas físicamente en un grupo de filas comprimidos que están marcadas para eliminación.<br /><br /> 0 para los grupos de filas que se encuentran en el almacén delta.|  
|**size_in_bytes**|**bigint**|Tamaño total, en bytes, de todas las páginas de este grupo de filas. Este tamaño no incluye el tamaño necesario para almacenar los metadatos o diccionarios compartidos.|  
|**trim_reason**|**tinyint**|Motivo por el que se desencadena el grupo de filas COMPRESSED tener menor que el número máximo de filas.<br /><br /> 0 - UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1 - NO_TRIM<br /><br /> 2 - CARGA MASIVA<br /><br /> 3 - REORG<br /><br /> 4 - DICTIONARY_SIZE<br /><br /> 5 - MEMORY_LIMITATION<br /><br /> 6 - RESIDUAL_ROW_GROUP<br /><br /> 7 - STATS_MISMATCH<br /><br /> 8 - EXCEDENTES|  
|**trim_reason_desc**|**nvarchar(60)**|Descripción de *trim_reason*.<br /><br /> 0 - UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: Se produjo al actualizar desde la versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 - NO_TRIM: El grupo de filas no se recorta. El grupo de filas se comprimió con el número máximo de 1,048,476 filas.  El número de filas puede ser menor si se ha eliminado un subsset de filas después de que se cerró el grupo de filas delta<br /><br /> 2 - CARGA MASIVA: El tamaño del lote de carga masiva limita el número de filas.<br /><br /> 3 - REORG:  Fuerza la compresión como parte del comando REORG.<br /><br /> 4 - DICTIONARY_SIZE: Tamaño del diccionario ha crecido demasiado grande para comprimir todas las filas entre sí.<br /><br /> 5 - MEMORY_LIMITATION: No hay suficiente memoria disponible para comprimir todas las filas entre sí.<br /><br /> 6 - RESIDUAL_ROW_GROUP:  Cerrado como parte del último grupo de filas con millones de filas < 1 durante la operación de generación de índice<br /><br /> STATS_MISMATCH: Solo para el almacén de columnas en la tabla en memoria. Si las estadísticas indican incorrectamente > = 1 millón de filas completo en la cola, pero se encontró menos, el grupo de filas comprimido tendrá < 1 millones de filas<br /><br /> EXCEDENTES: Solo para el almacén de columnas en la tabla en memoria. Si la cola tiene > 1 millones de filas completo, se comprimen las últimas filas restantes por lotes si el número está comprendido entre 100 KB y 1 millón|  
|**transition_to_compressed_state**|TINYINT|Muestra cómo se ha movido este grupo de filas del almacén delta en estado comprimido en el almacén de columnas.<br /><br /> 1 - NOT_APPLICABLE<br /><br /> 2 - INDEX_BUILD<br /><br /> 3 - TUPLE_MOVER<br /><br /> 4 - REORG_NORMAL<br /><br /> 5 - REORG_FORCED<br /><br /> 6 - CARGA MASIVA<br /><br /> 7 - MERGE|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE: la operación no se aplica al almacén delta. O bien, el grupo de filas se comprime antes de actualizar a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] en cuyo caso no se conserva el historial.<br /><br /> Crear un índice INDEX_BUILD - o regeneración de índice comprime el grupo de filas.<br /><br /> TUPLE_MOVER: el motor de tupla que se ejecuta en segundo plano comprime el grupo de filas. Esto sucede después de que el grupo de filas cambia el estado de abierto a cerrado.<br /><br /> REORG_NORMAL: la operación de reorganización, ALTER INDEX... REORG, mueve el grupo de filas cerrado desde el almacén delta al almacén de columnas. Esto ocurrió antes de que el motor de tupla tenido tiempo para mover el grupo de filas.<br /><br /> REORG_FORCED: este grupo de filas estaba abierto en el almacén delta y ha tenido en el almacén de columnas antes de que tenía un número total de filas.<br /><br /> Carga masiva: una operación de carga masiva comprime el grupo de filas directamente sin usar el almacén delta.<br /><br /> COMBINACIÓN - consolidado de uno o varios grupos de filas en este grupo de filas de una operación de combinación y, a continuación, realiza la compresión de almacén de columnas.|  
|**has_vertipaq_optimization**|bit|Optimización de Vertipaq mejora la compresión columnstore reorganizar el orden de las filas en el grupo de filas para lograr una compresión mayor. Esta optimización se produce automáticamente en la mayoría de los casos. Hay dos casos no se utiliza la optimización de Vertipaq:<br/>  a. Cuando mueve un grupo de filas delta al almacén de columnas y hay uno o varios índices no agrupados en el índice de almacén de columnas - en este caso se omite la optimización de Vertipaq a minimiza los cambios realizados en el índice de asignación;<br/> b. para los índices de almacén de columnas en tablas optimizadas para memoria. <br /><br /> 0 = No<br /><br /> 1 = Sí|  
|**generation**|BIGINT|Generación de grupo de filas asociada a este grupo de filas.|  
|**created_time**|datetime2|Hora del reloj para cuando se creó este grupo de filas.<br /><br /> NULL - para un índice de almacén de columnas en una tabla en memoria.|  
|**closed_time**|datetime2|Hora del reloj para cuando se ha cerrado este grupo de filas.<br /><br /> NULL - para un índice de almacén de columnas en una tabla en memoria.|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="results"></a>Resultado  
 Devuelve una fila por cada grupo de filas en la base de datos actual.  
  
## <a name="permissions"></a>Permisos  
 Se requieren estos permisos:  
  
-   Permiso CONTROL en la tabla.  
  
-   Permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. Calcular fragmentaton para decidir cuándo se debe reorganizar o volver a generar un índice de almacén de columnas.  
 Para los índices de almacén de columnas, el porcentaje de filas eliminadas es una buena medida para la fragmentación en un grupo de filas. Cuando la fragmentación es 20% o más, se recomienda quitar las filas eliminadas.  Para obtener ejemplos, vea [desfragmentación de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-defragmentation.md).  
  
 En este ejemplo une **sys.dm_db_column_store_row_group_physical_stats** con otro sistema de las tablas y, a continuación, calcula la `Fragmentation` columna como una estimación de la eficacia de cada grupo de filas de la base de datos actual.     Para buscar información en un única tabla, quite el comentario guiones delante de la **donde** cláusula y proporcione un nombre de tabla.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0) AS 'Fragmentation'
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
