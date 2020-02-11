---
title: Sys. dm_fts_semantic_similarity_population (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_semantic_similarity_population_TSQL
- sys.dm_fts_semantic_similarity_population
- dm_fts_semantic_similarity_population
- sys.dm_fts_semantic_similarity_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_semantic_similarity_population dynamic management view
ms.assetid: 33666f28-c370-47e2-a932-190316ed5f69
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 280ab197ef9347c6a209be7ef05e8f1ce2dfd23e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900872"
---
# <a name="sysdm_fts_semantic_similarity_population-transact-sql"></a>sys.dm_fts_semantic_similarity_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila de información de estado sobre el rellenado del índice de similitud de documentos para cada índice de similitud en cada tabla que tiene un índice semántico asociado.  
  
 El paso de rellenado sigue al paso de extracción. Para obtener información de estado sobre el paso de extracción de similitud, vea [Sys. dm_fts_index_population &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md).  
    
||||  
|-|-|-|  
|**Nombre de la columna**|**Tipo**|**Descripción**|  
|**database_id**|**int**|Identificador de la base de datos que contiene el índice de texto completo que se está rellenando.|  
|**catalog_id**|**int**|Id. del catálogo de texto completo que contiene este índice de texto completo.|  
|**table_id**|**int**|Id. de la tabla para la que se está llenando el índice de texto completo.|  
|**document_count**|**int**|Número de total de documentos del rellenado|  
|**document_processed_count**|**int**|Número de documentos procesados desde el inicio de este ciclo de llenado|  
|**completion_type**|**int**|Estado de finalización de este llenado.|  
|**completion_type_description**|**nvarchar (120)**|Descripción del tipo de finalización.|  
|**worker_count**|**int**|Número de subprocesos de trabajo asociados a la extracción de similitud|  
|**estatus**|**int**|Estado de este llenado. Nota: algunos de los estados son transitorios. Uno de los siguientes:<br /><br /> 3 = Iniciando<br /><br /> 5 = Procesamiento normal<br /><br /> 7 = Procesamiento detenido<br /><br /> 11 = Rellenado anulado|  
|**status_description**|**nvarchar (120)**|Descripción del estado de llenado.|  
|**start_time**|**datetime**|Hora en que se inició el rellenado.|  
|**incremental_timestamp**|**timestamp**|Representa la marca de tiempo de inicio de un llenado completo. Para los otros de tipos de llenado este valor es el último punto de comprobación confirmado que representa el progreso de los llenados.|  
  
## <a name="general-remarks"></a>Notas generales  
 Para obtener más información, vea [administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener más información sobre el estado de la indización semántica, consulte [Sys. dm_fts_index_population &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente se muestra cómo consultar el estado de los rellenados de índices de similitud de documentos para todas las tablas que tienen un índice semántico asociado:  
  
```  
SELECT * FROM sys.dm_fts_semantic_similarity_population;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
