---
title: "Diseño de los índices de almacén de columnas | Microsoft Docs"
ms.custom: 
ms.date: 01/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96b8e884-8244-425f-b856-72a8ff6895a6
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 86700a7247c7a712e03a5b34c6b68e9364d870b9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="columnstore-indexes---architecture"></a>Diseño de los índices de almacén de columnas
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Obtenga información sobre cómo está diseñado un índice de almacén de columnas. Si conoce estos conceptos básicos, le resultará más fácil entender otros artículos sobre almacenes de columnas que explican cómo utilizarlos de forma eficaz.

## <a name="data-storage-uses-columnstore-and-rowstore-compression"></a>El almacén de datos emplea la compresión de almacén de columnas y de filas
Al tratar los índices de almacén de columnas, usamos los términos *almacén de filas* y *almacén de columnas* para hacer hincapié en el formato del almacenamiento de datos.  Los índices de almacén de columnas utilizan estos dos tipos de almacenamiento.

 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")

- Un **almacén de columnas** son datos organizados lógicamente como una tabla con filas y columnas, y almacenados físicamente en un formato de columnas.
  
Un índice de almacén almacena físicamente la mayoría de los datos en formato de almacén de columnas. Con este formato, los datos se comprimen y descomprimen como columnas. No hace falta descomprimir otros valores que no haya solicitado la consulta en cada una de las filas. De este modo, se puede examinar rápida una columna entera de una tabla grande. 

- Un **almacén de filas** son datos organizados lógicamente como una tabla con filas y columnas, y almacenados físicamente después en un formato de filas. Esta ha sido la forma tradicional de almacenar datos de tablas relacionales, como un montón o un índice agrupado de árbol b.

Un índice de almacén de columnas también guarda físicamente algunas filas en un formato de almacén de filas denominado "almacén delta" (también llamado "grupos de filas delta"). Se trata de un lugar donde se colocan las filas que son insuficientes para poder comprimirse en el almacén de columnas. Cada grupo de filas delta se implementa como un índice agrupado de árbol b. 

- Un **almacén delta** es un lugar donde se colocan las filas que son insuficientes para poder comprimirse en el almacén de columnas. El almacén delta es un almacén de filas. 
  
## <a name="operations-are-performed-on-rowgroups-and-column-segments"></a>Las operaciones se realizan en segmentos de columna y grupos de filas

El índice de almacén de columnas agrupa las filas en unidades administrables. Cada una de estas unidades se denomina "grupo de filas". Para obtener el mejor rendimiento, el número de filas del grupo de filas debe ser suficientemente grande como para mejorar las tasas de compresión, y suficientemente pequeño como para beneficiarse de las operaciones en memoria.

* Un **grupo de filas** es un elemento en el que el índice de almacén de columnas realiza operaciones de administración y compresión. 

Por ejemplo, el índice de almacén de columnas realiza estas operaciones en grupos de filas:

* Comprime los grupos de filas en el almacén de columnas. La compresión se realiza en cada segmento de columna de un grupo de filas.
* Combina grupos de filas durante una operación ALTER INDEX REORGANIZE.
* Crea nuevos grupos de filas durante una operación ALTER INDEX REBUILD.
* Informa de la fragmentación y el estado de los grupos de filas en las vistas de administración dinámica (DMV).

El almacén delta se compone de uno o varios grupos de filas denominados "grupos de filas delta". Cada grupo de filas delta es un índice agrupado de árbol b que almacena filas cuando son insuficientes para poder comprimirse en el almacén de columnas.  

* Un **grupo de filas delta** es un índice agrupado de árbol b que almacena cargas masivas pequeñas y las inserta hasta que el grupo de filas contenga 1 048 576 filas o hasta que se vuelve a generar el índice.  Cuando un grupo de filas delta tenga 1 048 576 filas, se marca como cerrado y espera a que un proceso llamado "motor de tupla" lo comprima en el almacén de columnas. 


Cada columna tiene algunos de sus valores en cada grupo de filas. Estos valores se denominan "segmentos de columna". Cuando el índice de almacén de columnas comprime un grupo de filas, lo hace con cada segmento de columna de manera independiente. Para descomprimir una columna entera, el índice de almacén de columnas solo debe descomprimir un segmento de columna de cada grupo de filas.

* Un **segmento de columna** es la parte de los valores de columna de un grupo de filas. Cada grupo de filas contiene un segmento de cada columna de la tabla. Cada columna tiene un segmento de columna en cada grupo de filas.| 
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
 
## <a name="small-loads-and-inserts-go-to-the-deltastore"></a>Las inserciones y las cargas pequeñas pasan al almacén delta
Un índice de almacén de columnas mejora el rendimiento y la compresión del almacén de columnas comprimiendo, al menos, 102 400 filas a la vez en el índice de almacén de columnas. Para comprimir las filas de forma masiva, el índice de almacén de columnas acumula inserciones y cargas pequeñas en el almacén delta. Las operaciones del almacén delta se administran en segundo plano. Para devolver los resultados correctos de la consulta, el índice clúster de almacén de columnas combina los resultados de la consulta tanto del almacén de columnas como del almacén delta. 

Las filas pasan al almacén delta cuando se dan estas circunstancias:
* Se insertan con la instrucción INSERT INTO VALUES.
* Al final de una carga masiva y cuando tienen menos de 102 400 filas.
* Actualizado. Cada actualización se implementa como una eliminación y una inserción.

El almacén delta también guarda una lista de identificadores de las filas eliminadas que se han marcado como eliminadas, pero que aún no se han suprimido físicamente del almacén de columnas. 

## <a name="when-delta-rowgroups-are-full-they-get-compressed-into-the-columnstore"></a>Cuando se llenan los grupos de filas delta se comprimen en el almacén de columnas

Los índices agrupados de almacén de columnas recopilan hasta 1 048 576 filas en cada grupo de filas delta antes de comprimir dicho grupo de filas en el almacén de columnas. De este modo, se mejora la compresión del índice de almacén de columnas. Cuando un grupo de filas de almacén delta contiene 1 048 576 filas, el índice de almacén de columnas lo marca como cerrado. Un proceso en segundo plano denominado" *motor de tupla*" identifica cada grupo de filas marcado como cerrado y lo comprime en el almacén de columnas. 

Puede forzar grupos de filas delta del almacén de columnas mediante [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) para generar o reorganizar el índice.  Tenga en cuenta que si hay presión de memoria durante la compresión, el índice de almacén de columnas podría reducir el número de filas de filas en el grupo de filas comprimido.

## <a name="each-table-partition-has-its-own-rowgroups-and-delta-rowgroups"></a>Cada partición de tabla tiene sus propios grupos de filas y grupos de filas delta

El concepto de partición es el mismo en un índice agrupado, un montón y un índice de almacén de columnas. Al crear particiones de una tabla, esta se divide en grupos de filas más pequeños según un rango de valores de columna. A menudo, se utiliza para administrar los datos. Por ejemplo, podría crear una partición de cada año de datos y, más adelante, usar la opción de modificación de particiones para archivar los datos en un almacenamiento menos costoso. Esta característica funciona en los índices de almacén de columnas y facilita la tarea de mover una partición de datos a otra ubicación.

Los grupos de filas siempre se definen dentro de una partición de tabla. Cuando un índice de almacén de columnas tiene particiones, cada una de ellas tiene sus propios grupos de filas y grupos de filas delta comprimidos.

### <a name="each-partition-can-have-multiple-delta-rowgroups"></a>Cada partición puede contener varios grupos de filas delta
Cada partición puede tener más de un grupos de filas delta. Cuando el índice de almacén de columnas necesita agregar datos a un grupo de filas delta y este se ha bloqueado, el índice de almacén de columnas tratará de obtener un bloqueo en otro grupo de filas delta. Si no hay ningún grupo de filas delta disponible, el índice de almacén columnas creará un grupo de filas delta.  Por ejemplo, una tabla con 10 particiones podría tener fácilmente 20 o más grupos de filas delta. 

  
## <a name="you-can-combine-columnstore-and-rowstore-indexes-on-the-same-table"></a>Puede combinar los índices de almacén de filas y de columnas en la misma tabla
Un índice no agrupado contiene una copia de parte o la totalidad de las filas y columnas de la tabla subyacente. El índice se define como una o varias columnas de la tabla y tiene una condición opcional que filtra las filas. 

Desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede crear un índice de almacén de columnas no agrupado actualizable en una tabla de almacén de filas. El índice de columnas almacena una copia de los datos, por lo que necesita más almacenamiento. Sin embargo, los datos del índice de almacén de columnas se comprimen en un tamaño inferior al que requiere la tabla de almacén de filas.  Gracias a esto, se pueden ejecutar análisis en el índice de almacén de columnas y realizar transacciones en el índice de almacén de filas al mismo tiempo. El almacén de columnas se actualiza cuando cambian los datos de la tabla de almacén de filas, de modo que ambos índices trabajan con los mismos datos.  
  
 Desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], puede tener uno o varios índices de almacén de filas no agrupados en un índice de almacén de columnas. Gracias a ello, podrá realizar búsquedas de tabla eficaces en el almacén de columnas subyacente. También habrá disponibles otras opciones. Por ejemplo, podrá aplicar una restricción de clave principal mediante una restricción UNIQUE en la tabla de almacén de filas. Puesto que un valor que no es único no se insertará en la tabla de almacén de filas, SQL Server no podrá insertar ese valor en el almacén de columnas.  
 

## <a name="metadata"></a>Metadatos  
Utilice estas vistas de metadatos para ver los atributos de los índices de almacén de columnas. Puede obtener más información sobre la arquitectura en algunas de estas vistas.

Tenga en cuenta que todas las columnas de un índice de almacén de columnas se guardan en los metadatos como columnas incluidas. El índice de almacén de columnas no tiene columnas de clave.  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
  
-   [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
|  


## <a name="next-steps"></a>Pasos siguientes
 Para obtener instrucciones sobre cómo diseñar los índices de almacén de columnas, consulte [Guía de diseño de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-design-guidance.md).
