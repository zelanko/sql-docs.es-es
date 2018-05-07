---
title: Sys.dm_db_column_store_row_group_physical_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f2ed303fcfeef2d2f47504f3b2b4234f32067d0f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>sys.dm_db_column_store_row_group_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Proporciona información de nivel de grupo de filas actual acerca de todos los índices de almacén de columnas en la base de datos actual.  
  
 Este comando extiende la vista de catálogo [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla subyacente.|  
|**index_id**|**int**|Id. de este índice de almacén de columnas en *object_id* tabla.|  
|**partition_number**|**int**|Identificador de la partición de tabla que contiene *row_group_id*. Puede utilizar partition_number para unir esta DMV a sys.partitions.|  
|**Row_group_id**|**int**|Id. de este grupo de filas. Para las tablas con particiones, es único dentro de la partición.<br /><br /> -1 para una cola en memoria.|  
|**delta_store_hobt_id**|**bigint**|El hobt_id para un grupo de filas en el almacén delta.<br /><br /> Es NULL si el grupo de filas no está en el almacén delta.<br /><br /> NULL para el final de una tabla en memoria.|  
|**state**|**tinyint**|Número de identificación asociado *state_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = MARCADOR DE EXCLUSIÓN<br /><br /> COMPRESSED es el único estado que se aplica a tablas en memoria.|  
|**state_desc**|**nvarchar(60)**|Descripción del estado del grupo de fila:<br /><br /> INVISIBLE: un grupo de filas que se va a compilar. Por ejemplo: <br />Un grupo de filas del almacén de columnas es INVISIBLE mientras se comprime los datos. Cuando finaliza la compresión cambia de un conmutador de metadatos el estado de la fila del almacén de columnas grupo desde INVISIBLE a COMPRESSED y el estado del grupo de filas almacén delta de cerrado a objetos de DESECHO.<br /><br /> Abra: un grupo de filas de almacén delta que se acepta filas nuevas. Un grupo de filas abierto está todavía en formato de almacén de filas y no se ha comprimido al formato de almacén de columnas.<br /><br /> CERRADO: un grupo de filas en el almacén delta que contiene el número máximo de filas y está esperando que el proceso de tupla motriz para la compresión en el almacén de columnas.<br /><br /> COMPRESSED: grupo de filas que se comprimió con compresión de almacén de columnas y se almacenan en el almacén de columnas.<br /><br /> TOMBSTONE: que utiliza un grupo de filas que se encontraba anteriormente en el almacén delta y ya no lo está.|  
|**total_rows**|**bigint**|Número de filas físicos almacenado en el grupo de filas. Para grupos de filas comprimido, esto incluye las filas que están marcadas eliminadas.|  
|**deleted_rows**|**bigint**|Número de filas almacenadas físicamente en un grupo de filas comprimidos que están marcadas para eliminación.<br /><br /> 0 para los grupos de filas que se encuentran en el almacén delta.|  
|**size_in_bytes**|**bigint**|Tamaño total, en bytes, de todas las páginas de este grupo de filas. Este tamaño no incluye el tamaño necesario para almacenar metadatos o diccionarios compartidos.|  
|**trim_reason**|**tinyint**|Motivo por el que desencadenó el grupo de filas COMPRESSED tener menor que el número máximo de filas.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1 - NO_TRIM<br /><br /> 2 - CARGA MASIVA<br /><br /> 3 – REORG<br /><br /> 4-DICTIONARY_SIZE<br /><br /> 5: MEMORY_LIMITATION<br /><br /> 6: RESIDUAL_ROW_GROUP<br /><br /> 7 - STATS_MISMATCH<br /><br /> 8 - SOBRANTE|  
|**trim_reason_desc**|**nvarchar(60)**|Descripción de *trim_reason*.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: se produjo al actualizar desde la versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 - NO_TRIM: El grupo de filas no se recorta. El grupo de filas se comprimió con el valor máximo de 1,048,476 filas.  El número de filas puede ser menor si se ha eliminado un subsset de filas después de cerrar grupo de filas delta<br /><br /> 2: carga masiva: El tamaño del lote de carga masiva limita el número de filas.<br /><br /> 3 – REORG: Fuerza la compresión como parte del comando REORG.<br /><br /> 4-DICTIONARY_SIZE: El tamaño del diccionario ha crecido demasiado grande para comprimir todas las filas entre sí.<br /><br /> 5: MEMORY_LIMITATION: No hay suficiente memoria disponible para comprimir todas las filas entre sí.<br /><br /> 6: RESIDUAL_ROW_GROUP: Cierra como parte del último grupo de filas con millones de filas < 1 durante la operación de generación de índice<br /><br /> STATS_MISMATCH: solo para el almacén de columnas en la tabla en memoria. Si estadísticas incorrectamente indican > = 1 millón de filas completo en la cola, pero se encontró menos, el grupo de filas comprimido tendrá < 1 millones de filas<br /><br /> SOBRANTE: solo para el almacén de columnas en la tabla en memoria. Si la cola tiene 1 > millones de filas completo, se comprimen las últimas filas restantes de lote si el número está comprendido entre 100 KB y 1 millón|  
|**transition_to_compressed_state**|tinyint|Muestra cómo se ha movido este grupo de filas del almacén delta en estado comprimido en el almacén de columnas.<br /><br /> 1 - NOT_APPLICABLE<br /><br /> 2 – INDEX_BUILD<br /><br /> 3-TUPLE_MOVER<br /><br /> 4-REORG_NORMAL<br /><br /> 5: REORG_FORCED<br /><br /> 6 - CARGA MASIVA<br /><br /> 7 - MEZCLA|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE: la operación no se aplica al almacén delta. O bien, el grupo de filas se comprimió antes de actualizar a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] en cuyo caso no se conserva el historial.<br /><br /> Crear un índice INDEX_BUILD – o regeneración de índice comprimido el grupo de filas.<br /><br /> TUPLE_MOVER: el motor de tupla que se ejecuta en segundo plano comprime el grupo de filas. Esto sucede después de que el grupo de filas cambia el estado de abierto a cerrado.<br /><br /> REORG_NORMAL: la operación de reorganización, ALTER INDEX... REORG, mueve el grupo de filas cerrado desde el almacén delta al almacén de columnas. Esto ha ocurrido antes de que el motor de tupla tenido tiempo para mover el grupo de filas.<br /><br /> REORG_FORCED – este grupo de filas estaba abierto en el almacén delta y se ha forzado a almacenar en el almacén de columnas antes de que tenía un número total de filas.<br /><br /> Carga masiva: una operación de carga masiva comprime el grupo de filas directamente sin usar el almacén delta.<br /><br /> MERGE: una operación de combinación consolidados uno o varios grupos de filas en este grupo de filas y, a continuación, realiza la compresión de almacén de columnas.|  
|**has_vertipaq_optimization**|bit|Optimización de Vertipaq mejora la compresión columnstore reorganizando el orden de las filas en el grupo de filas para lograr una mayor compresión. Esta optimización se produce automáticamente en la mayoría de los casos. Hay dos casos no se utiliza la optimización de Vertipaq:<br/>  A. Cuando se mueve un grupo de filas delta al almacén de columnas y hay uno o varios índices no clúster en el índice de almacén de columnas - en este caso se omite Vertipaq optimización a minimiza los cambios en el índice de asignación;<br/> B. para los índices de almacén de columnas en tablas optimizadas en memoria. <br /><br /> 0 = No<br /><br /> 1 = Sí|  
|**generación**|bigint|Generación de grupo de fila asociada a este grupo de filas.|  
|**created_time**|datetime2|Hora del reloj para cuando se creó este grupo de filas.<br /><br /> NULL: para un índice de almacén de columnas en una tabla en memoria.|  
|**closed_time**|datetime2|Hora del reloj para cuando se ha cerrado este grupo de filas.<br /><br /> NULL: para un índice de almacén de columnas en una tabla en memoria.|  
  
## <a name="results"></a>Resultado  
 Devuelve una fila por cada grupo de filas de la base de datos actual.  
  
## <a name="permissions"></a>Permissions  
 Se requieren estos permisos:  
  
-   Permiso CONTROL en la tabla.  
  
-   Permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. Calcular fragmentaton para decidir cuándo se debe reorganizar o volver a generar un índice de almacén de columnas.  
 Para los índices de almacén de columnas, el porcentaje de filas eliminadas es una buena medida para la fragmentación en un grupo de filas. Cuando la fragmentación es del 20% o más, se recomienda quitar las filas eliminadas.  Para obtener ejemplos, vea [desfragmentación de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-defragmentation.md).  
  
 Este ejemplo combina **sys.dm_db_column_store_row_group_physical_stats** con otro sistema de tablas y, a continuación, calcula la `Fragmentation` columna como una estimación de la eficacia de cada grupo de filas de la base de datos actual.     Para buscar información en una única tabla, quite el comentario guiones delante de la **donde** cláusula y proporcione un nombre de tabla.  
  
```sql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/total_rows AS 'Fragmentation'  
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.ALL_COLUMNS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
