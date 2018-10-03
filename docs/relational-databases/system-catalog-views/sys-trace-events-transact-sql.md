---
title: Sys.trace_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_events_TSQL
- trace_events
- sys.trace_events
- sys.trace_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_events catalog view
ms.assetid: e7d2c5df-0e17-4e94-9d41-d36c7ee60662
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 302a0ea8c058eb3e69d89c2fc1e742af1965c4ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628303"
---
# <a name="systraceevents-transact-sql"></a>sys.trace_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sys.trace_events** vista de catálogo contiene una lista de todos los eventos de seguimiento SQL. Estos eventos de seguimiento no cambian para una versión concreta de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use vistas de catálogo de eventos extendidos en su lugar.  
  
 Para obtener más información acerca de estos eventos de seguimiento, vea [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|Id. único del evento. Esta columna también está disponible en el **sys.trace_event_bindings** y **sys.trace_subclass_values** vistas de catálogo.|  
|**category_id**|**smallint**|Id. de categoría del evento. Esta columna también está disponible en el **sys.trace_categories** vista de catálogo.|  
|**Nombre**|**nvarchar(128)**|Nombre único de este evento. Este parámetro no se traduce.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Sys.Traces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [Sys.trace_categories &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [Sys.trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [Sys.trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
