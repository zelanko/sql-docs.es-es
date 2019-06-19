---
title: sys.dm_fts_index_population (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
author: pmasl
ms.author: pelopes
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 223277050e7c758d2fcd5d46e62cf171fc2a1cca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947304"
---
# <a name="sysdmftsindexpopulation-transact-sql"></a>sys.dm_fts_index_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los rellenados de frases clave semánticas e índices de texto completo actualmente en curso en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Identificador de la base de datos que contiene el índice de texto completo que se está rellenando.|  
|**catalog_id**|**int**|Id. del catálogo de texto completo que contiene este índice de texto completo.|  
|**table_id**|**int**|Id. de la tabla para la que se está llenando el índice de texto completo.|  
|**memory_address**|**varbinary(8)**|Dirección de memoria de la estructura de datos interna utilizada para representar un rellenado activo.|  
|**population_type**|**int**|Tipo de llenado. Uno de los siguientes:<br /><br /> 1 = Llenado completo<br /><br /> 2 = Llenado basado en la marca de tiempo incremental<br /><br /> 3 = Actualización manual de los cambios de los que se ha realizado seguimiento<br /><br /> 4 = Actualización de fondo de los cambios de los que se ha realizado seguimiento.|  
|**population_type_description**|**nvarchar(120)**|Descripción del tipo de llenado.|  
|**is_clustered_index_scan**|**bit**|Indica si el llenado implica un recorrido en el índice clúster.|  
|**range_count**|**int**|Número de subintervalos en los que este llenado se ha hecho en paralelo.|  
|**completed_range_count**|**int**|Número de intervalos en los que se ha completado el proceso.|  
|**outstanding_batch_count**|**int**|Número actual de lotes pendientes para este rellenado. Para obtener más información, consulte [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md).|  
|**status**|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Estado de este llenado. Nota: algunos de los estados son transitorios. Uno de los siguientes:<br /><br /> 3 = Iniciando<br /><br /> 5 = Procesamiento normal<br /><br /> 7 = Procesamiento detenido<br /><br /> Por ejemplo, este estado se produce cuando hay una combinación automática en curso.<br /><br /> 11 = Rellenado anulado<br /><br /> 12 = Procesamiento de una extracción de similitud semántica|  
|**status_description**|**nvarchar(120)**|Descripción del estado de llenado.|  
|**completion_type**|**int**|Estado de finalización de este llenado.|  
|**completion_type_description**|**nvarchar(120)**|Descripción del tipo de finalización.|  
|**worker_count**|**int**|Este valor siempre es 0.|  
|**queued_population_type**|**int**|Tipo de llenado, basado en los cambios de seguimiento, que seguirán el llenado actual, si los hay.|  
|**queued_population_type_description**|**nvarchar(120)**|Descripción del rellenado que se va a seguir, si existe. Por ejemplo, cuando CHANGE TRACKING = AUTO y el rellenado completo inicial está en curso, esta columna indicaría "Rellenado automático".|  
|**start_time**|**datetime**|Hora en que se inició el rellenado.|  
|**incremental_timestamp**|**timestamp**|Representa la marca de tiempo de inicio de un llenado completo. Para los otros de tipos de llenado este valor es el último punto de comprobación confirmado que representa el progreso de los llenados.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando la indización semántica estadística está habilitada además de la indización de texto completo, la extracción y el rellenado de frases clave semánticas y la extracción de datos de similitud de documentos se producen simultáneamente con la indización de texto completo. El rellenado del índice de similitud de documentos se produce posteriormente en una segunda fase. Para obtener más información, consulte [administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="physical-joins"></a>Combinaciones físicas  
 ![Combinaciones significativas de esta vista de administración dinámica](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "combinaciones significativas de esta vista de administración dinámica")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|Uno a uno|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|Uno a uno|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

