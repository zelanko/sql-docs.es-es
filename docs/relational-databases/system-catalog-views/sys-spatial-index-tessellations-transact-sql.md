---
title: Sys.spatial_index_tessellations (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- spatial_index_tessellations
- sys.spatial_index_tessellations_TSQL
- spatial_index_tessellations_TSQL
- sys.spatial_index_tessellations
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_index_tessellations catalog view
ms.assetid: 8b17a9a4-b57f-4220-8138-fc73581b1670
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cb3c73d1baf770004cb56cebaa6034ed5091090c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysspatialindextessellations-transact-sql"></a>sys.spatial_index_tessellations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

 Representa la información acerca del esquema de teselación y los parámetros de cada uno de los índices espaciales.  
  
> [!NOTE]  
>  Para más información sobre la teselación, vea [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md).  
  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Identificador del objeto en el que se define el índice. Cada (object_id, index_id) par tiene una entrada correspondiente [sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md).|  
|index_id|**int**|Identificador del índice espacial en el que se define la columna indizada.|  
|tessellation_scheme|**sysname**|Nombre del esquema de teselación, uno de: GEOMETRY_GRID, GEOGRAPHY_GRID|  
|bounding_box_xmin|**float(53)**|Coordenada X de la esquina inferior izquierda del delimitador en el cuadro, uno de: NULL = no aplicable con un esquema de teselación dado (como GEOGRAPHY_GRID) *n* = si tessellation_scheme es GEOMETRY_GRID, el valor de la coordenada x mínima.                     **Nota:** se interpretan las coordenadas definidas por los parámetros del cuadro de límite para cada objeto según su [identificador de referencia espacial (SRID)](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).|  
|bounding_box_ymin|**float(53)**|Coordenada Y de la esquina inferior izquierda del delimitador en el cuadro, uno de: NULL = no aplicable con un esquema de teselación dado (como GEOGRAPHY_GRID) *n* = si tessellation_scheme es GEOMETRY_GRID, el valor de la coordenada y mínima|  
|bounding_box_xmax|**float(53)**|Coordenada X de la esquina superior derecha del delimitador en el cuadro, uno de: NULL = no aplicable con un esquema de teselación dado (como GEOGRAPHY_GRID) *n* = si tessellation_scheme es GEOMETRY_GRID, el valor de la coordenada x máxima|  
|bounding_box_ymax|**float(53)**|Coordenada Y de la esquina superior derecha del delimitador en el cuadro, uno de: NULL = no aplicable con un esquema de teselación dado (como GEOGRAPHY_GRID) *n* = si tessellation_scheme es GEOMETRY_GRID, el valor de la coordenada y máxima|  
|level_1_grid|**smallint**|Densidad de la cuadrícula para la cuadrícula de nivel superior. Si tessellation_scheme es GEOMETRY_GRID o GEOGRAPHY_GRID, uno de: 16 = 4 por 4 cuadrícula (baja) 64 = 8 por 8 cuadrícula (intermedia) 256 = 16 por 16 cuadrícula (alta) NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_1_grid_desc|**nvarchar(60)**|Densidad de cuadrícula de la cuadrícula de nivel superior, uno de: bajo Mediana alta NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_2_grid|**smallint**|Densidad de la cuadrícula de segundo nivel. Si tessellation_scheme es GEOMETRY_GRID o GEOGRAPHY_GRID, uno de: 16 = 4 por 4 cuadrícula (baja) 64 = 8 por 8 cuadrícula (intermedia) 256 = 16 por 16 cuadrícula (alta) NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_2_grid_desc|**nvarchar(60)**|Densidad de cuadrícula de la cuadrícula de nivel 2 º, uno de: bajo Mediana alta NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_3_grid|**smallint**|Densidad de la cuadrícula de tercer nivel.   Si tessellation_scheme es GEOMETRY_GRID o GEOGRAPHY_GRID, uno de: 16 = 4 por 4 cuadrícula (baja) 64 = 8 por 8 cuadrícula (intermedia) 256 = 16 por 16 cuadrícula (alta) NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_3_grid_desc|**nvarchar(60)**|Densidad de cuadrícula de la cuadrícula de nivel 3, uno de: bajo Mediana alta NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_4_grid|**smallint**|Densidad de la cuadrícula de cuarto nivel. Si tessellation_scheme es GEOMETRY_GRID o GEOGRAPHY_GRID, uno de: 16 = 4 por 4 cuadrícula (baja) 64 = 8 por 8 cuadrícula (intermedia) 256 = 16 por 16 cuadrícula (alta) NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|level_4_grid_desc|**nvarchar(60)**|Densidad de cuadrícula de la cuadrícula de nivel 4, uno de: < bajo Mediana alta NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados.  Se devuelve NULL cuando se utiliza la nueva teselación de SQL Server 11.|  
|cells_per_object|**int**|Número de celdas por objeto espacial, uno de: si tessellation_scheme es GEOMETRY_GRID o GEOGRAPHY_GRID, *n* = número de celdas por objeto NULL = no aplicable con un esquema de teselación o un tipo de índice espacial dados|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
