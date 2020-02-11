---
title: Propiedades de la tabla de seguimiento (pestaña selección de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.tracetableproperties.eventsselection.f1
helpviewer_keywords:
- Trace Table Properties dialog box
ms.assetid: fa21df6a-b6b5-4b15-9104-957385821594
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 404b1d5d8467fe5840a6f53007bd55bc58cdf19f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089539"
---
# <a name="trace-table-properties-events-selection-tab"></a>Propiedades de la tabla de seguimiento (pestaña Selección de eventos)
  Utilice la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades de la tabla de seguimiento** para ver las propiedades de columna de datos y eventos del seguimiento o para quitar eventos o columnas del seguimiento.  
  
 Para ver esta ventana, use [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para abrir una tabla de seguimiento. A continuación, en el menú **archivo** , haga clic en **propiedades**y, a continuación, haga clic en la pestaña **selección de eventos** .  
  
## <a name="options"></a>Opciones  
 Columna **eventos**  
 Muestra los eventos de los que se hace el seguimiento y que están organizados por categoría de eventos. Para seleccionar un evento, debe activarse la casilla o la columna de datos de dicho evento. Si la casilla del evento está activada, se seleccionan todas las columnas de datos disponibles para dicho evento. Si la columna de datos de un evento está activada, se activa el evento, y cualquier otra columna requerida también se activa automáticamente. Si se está viendo un archivo o una tabla de seguimiento, al desactivar las casillas de las columnas de datos o eventos, se reduce la cantidad de datos visibles en la ventana de seguimiento para simplificar el análisis. Se pueden cambiar los filtros de las columnas para reducir la cantidad de datos visibles en la ventana de seguimiento. Para obtener más información sobre las clases de eventos, vea [Referencia de las clase de eventos de SQL Server](../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 Otras columnas de datos  
 Muestra las columnas de datos de las que se realiza un seguimiento. Todas las columnas de datos relevantes del seguimiento están activadas de forma predeterminada para cada uno de los eventos incluidos en el seguimiento.  
  
 Especifique los filtros haciendo clic en el encabezado de la columna de datos y especificando los criterios de filtro. Las columnas de datos filtradas se indican mediante un icono de filtro situado a la izquierda de la etiqueta de columna en el cuadro de diálogo **Editar filtro** .  
  
 **Mostrar todos los eventos**  
 Se muestran todos los eventos disponibles. De forma predeterminada, solo se muestran las filas de la cuadrícula **Selección de eventos** que están seleccionadas. Desactive esta casilla para ocultar todos los eventos que no estén seleccionados en la cuadrícula **Selección de eventos** . Si se activa **Mostrar todos los eventos** y se está viendo un archivo o una tabla de seguimiento, todos los eventos que se grabaron en el seguimiento se mostrarán en la ventana de seguimiento.  
  
 **Mostrar todas las columnas**  
 Muestra todas las columnas de datos disponibles. De forma predeterminada, solo se muestran las columnas de datos seleccionadas. Desactive esta casilla para ocultar todas las columnas de datos que no estén seleccionadas en la cuadrícula **Selección de eventos** .  
  
 **Filtros de columnas**  
 Inicia el cuadro de diálogo **Editar filtro**, en el que se muestra un icono de filtro a la izquierda de la etiqueta de la columna. Puede utilizar este cuadro de diálogo para editar los filtros de las columnas de datos.  
  
 **Organizar columnas**  
 Después de seleccionar la columna **Eventos** y la columna de datos de las que se va a realizar un seguimiento, haga clic en **Organizar columnas** para que la cuadrícula reordene la columna en la ventana de resultados del seguimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
