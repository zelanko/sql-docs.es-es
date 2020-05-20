---
title: Sys. trace_categories (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_categories
- trace_categories_TSQL
- sys.trace_categories
- sys.trace_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_categories catalog view
ms.assetid: f6a86766-e2a9-4d9f-a073-1b59e888ba7d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4898bdb8e05c2b2fce20ca30ef7f056107a4befa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821277"
---
# <a name="systrace_categories-transact-sql"></a>sys.trace_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las clases de eventos similares se agrupan por categoría. Cada fila de la vista de catálogo **Sys. trace_categories** identifica una categoría que es única en todo el servidor. Estas categorías no cambian para una versión concreta de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para obtener una lista completa de los eventos de seguimiento admitidos, vea [SQL Server referencia](../../relational-databases/event-classes/sql-server-event-class-reference.md)de la clase de eventos.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use vistas de catálogo de eventos extendidos en su lugar.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**category_id**|**smallint**|Id. único de esta categoría. Esta columna también está en la vista de catálogo **Sys. trace_events** .|  
|**name**|**nvarchar(128)**|Nombre único de esta categoría. Este parámetro no se traduce.|  
|**type**|**tinyint**|Tipo de categoría:<br /><br /> 0 = Normal<br /><br /> 1 = Conexión<br /><br /> 2 = Error|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Sys. Traces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [Sys. trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [Sys. trace_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [Sys. trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [Sys. trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
