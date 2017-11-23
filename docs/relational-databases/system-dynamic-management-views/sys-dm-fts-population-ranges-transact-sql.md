---
title: Sys.dm_fts_population_ranges (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/29/2017
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
- sys.dm_fts_population_ranges
- sys.dm_fts_population_ranges_TSQL
- dm_fts_population_ranges_TSQL
- dm_fts_population_ranges
dev_langs: TSQL
helpviewer_keywords: sys.dm_fts_population_ranges dynamic management view
ms.assetid: 58d8564b-9c43-4965-a31c-2893890334ef
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 06ca4f5bc4232621bcc027696f1f778633f1942c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftspopulationranges-transact-sql"></a>sys.dm_fts_population_ranges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los intervalos específicos relacionados con un rellenado de índices de texto completo actualmente en progreso.  
   
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**memory_address**|**varbinary (8)**|Dirección de búferes de memoria asignados para la actividad relacionada con este subintervalo de un rellenado de índices de texto completo.|  
|**parent_memory_address**|**varbinary (8)**|Dirección de búferes de memoria que representa el objeto primario de todos los intervalos de rellenado relacionados con un índice de texto completo.|  
|**is_retry**|**bit**|Si el valor es 1, este subintervalo es responsable de reintentar las filas con errores.|  
|**session_id**|**smallint**|Id. de la sesión que procesa actualmente esta tarea.|  
|**processed_row_count**|**int**|Número de filas que se han procesado en este intervalo. El progreso se conserva y se cuenta cada 5 minutos, en lugar de con cada confirmación del lote.|  
|**error_count**|**int**|Número de filas que han tenido errores en este intervalo. El progreso se conserva y se cuenta cada 5 minutos, en lugar de con cada confirmación del lote.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.  

## <a name="physical-joins"></a>Combinaciones físicas  
 ![Combinaciones significativas de esta vista de administración dinámica](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-population-ranges-1.gif "combinaciones significativas de esta vista de administración dinámica")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
  [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

