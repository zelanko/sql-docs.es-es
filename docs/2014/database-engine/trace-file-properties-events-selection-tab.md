---
title: Seguimiento de propiedades de archivo (pestaña selección de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracefileproperties.eventsselection.f1
helpviewer_keywords:
- Trace File Properties dialog box
ms.assetid: 158d442f-2225-4173-8545-fb1cf611b4d0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 956316eb83291f71932c0ee70460274090b7069d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193375"
---
# <a name="trace-file-properties-events-selection-tab"></a>Propiedades del archivo de seguimiento (pestaña Selección de eventos)
  Utilice la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades del archivo de seguimiento** para ver las propiedades de columna del seguimiento o quitar columnas de datos del seguimiento.  
  
 Para ver esta ventana, abra un archivo de seguimiento. Después, en el menú **Archivo** , haga clic en **Propiedades**y, a continuación, haga clic en la pestaña **Selección de eventos** .  
  
## <a name="options"></a>Opciones  
 Columna **Eventos**  
 Muestra los eventos de los que se hace el seguimiento y que están organizados por categoría de eventos. Inicialmente, se seleccionan todos los eventos del seguimiento. Para seleccionar un evento, debe activarse la casilla o la columna de datos de dicho evento. Si la casilla del evento está activada, se seleccionan todas las columnas de datos disponibles para dicho evento. Si la columna de datos de un evento está activada, se activa el evento, y cualquier otra columna requerida también se activa automáticamente. Si se está viendo un archivo o una tabla de seguimiento, al desactivar las casillas de las columnas de datos o eventos, se reduce la cantidad de datos visibles en la ventana de seguimiento para simplificar el análisis. Se pueden cambiar los filtros de las columnas para reducir la cantidad de datos visibles en la ventana de seguimiento. Para obtener más información sobre las clases de eventos, vea [SQL Server Event Class Reference](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Columnas de datos  
 Muestra las columnas de datos de las que se realiza un seguimiento. Todas las columnas de datos relevantes del seguimiento están activadas de forma predeterminada para cada uno de los eventos incluidos en el seguimiento.  
  
 Especifique los filtros haciendo clic en el encabezado de la columna de datos y especificando los criterios de filtro. Las columnas de datos filtradas se indican mediante un icono de filtro situado a la izquierda de la etiqueta de columna en el cuadro de diálogo **Editar filtro** .  
  
 **Mostrar todos los eventos**  
 Se muestran todos los eventos disponibles. De forma predeterminada, solo se muestran las filas de la cuadrícula **Selección de eventos** que están seleccionadas. Desactive esta casilla para ocultar todos los eventos que no estén seleccionados en la cuadrícula **Selección de eventos** . Si se activa **Mostrar todos los eventos** y se está viendo un archivo o una tabla de seguimiento, todos los eventos que se grabaron en el seguimiento se mostrarán en la ventana de seguimiento.  
  
 **Mostrar todas las columnas**  
 Muestra todas las columnas de datos disponibles. De forma predeterminada, solo se muestran las columnas de datos seleccionadas. Desactive esta casilla para ocultar todas las columnas de datos que no estén seleccionadas en la cuadrícula **Selección de eventos** .  
  
 **Filtros de columnas**  
 Inicia el cuadro de diálogo **Editar filtro** , que muestra un icono de filtro a la izquierda de la etiqueta de columna para las columnas de datos filtradas. Utilice el cuadro de diálogo **Editar filtro** para editar los filtros de las columnas de datos.  
  
 **Organizar columnas**  
 Después de seleccionar la columna **Eventos** y la columna de datos de las que se va a realizar un seguimiento, haga clic en **Organizar columnas** para que la cuadrícula reordene la columna en la ventana de resultados del seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Especificar eventos y columnas de datos para un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Filtrar eventos en un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)   
 [Ver información de un filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [Modificar un filtro &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
  
  
