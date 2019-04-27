---
title: Seguimiento de propiedades de la plantilla (pestaña selección de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetemplateproperties.eventsselection.f1
helpviewer_keywords:
- Trace Template Properties dialog box
ms.assetid: 5b202457-ab42-4902-8012-7f3f40aa09f5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac74d361758cda8ec0b345b93e542d96c709e586
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773461"
---
# <a name="trace-template-properties-events-selection-tab"></a>Propiedades de la plantilla de seguimiento (pestaña Selección de eventos)
  Utilice la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades de la plantilla de seguimiento** para ver, editar o especificar las clases de eventos y las columnas de datos que se van a incluir en una plantilla de seguimiento del [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] .  
  
## <a name="options"></a>Opciones  
 Columna**Eventos**   
 Active o desactive la casilla de la columna de eventos para especificar los eventos de los que debe realizarse un seguimiento. Los eventos se organizan por categoría.  
  
 Si ha seleccionado **Basar plantilla nueva en una existente** en la pestaña **General** , los eventos se seleccionan automáticamente de acuerdo con la plantilla especificada. Para obtener más información sobre las clases de eventos, vea [Referencia de las clase de eventos de SQL Server](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Columnas de datos  
 Especifique las columnas de datos de las que debe realizarse un seguimiento activando el cuadro correspondiente al evento y la columna de datos que necesite. Si se activa la casilla correspondiente al evento, todas las columnas de eventos pertinentes se activan de forma predeterminada para cada evento incluido en el seguimiento. Si ha seleccionado **Basar plantilla nueva en una existente** en la pestaña **General** , las columnas de datos y los filtros se seleccionan automáticamente de acuerdo con la plantilla especificada.  
  
 Especifique los filtros haciendo clic en el encabezado de la columna de datos y especificando los criterios de filtro. Las columnas de datos filtradas se indican mediante un icono de filtro situado a la izquierda de la etiqueta de columna en el cuadro de diálogo **Editar filtro** .  
  
 **Mostrar todos los eventos**  
 Se muestran todos los eventos disponibles. Esta opción está activada de forma predeterminada si crea una nueva plantilla que no se base en una plantilla existente. Desactive esta opción para ocultar todos los eventos no seleccionados en la cuadrícula **Selección de eventos** .  
  
 **Mostrar todas las columnas**  
 Muestra todas las columnas de datos disponibles. Esta opción está activada de forma predeterminada si crea una nueva plantilla que no se base en una plantilla existente. Desactive esta opción para ocultar todas las columnas de datos no seleccionadas en la cuadrícula **Selección de eventos** .  
  
 **Filtros de columnas**  
 Inicia el cuadro de diálogo **Editar filtro**, que muestra un icono de filtro a la izquierda de la etiqueta de columna de datos. Utilice el cuadro de diálogo **Editar filtro** para editar los filtros de las columnas de datos.  
  
 **Organizar columnas**  
 Cambia el orden de las columnas del seguimiento y agrupa los resultados en una o más columnas.  
  
## <a name="see-also"></a>Vea también  
 [Especificar eventos y columnas de datos para un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Organizar las columnas mostradas en un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Filtrar eventos en un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Ver información de un filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificar un filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
