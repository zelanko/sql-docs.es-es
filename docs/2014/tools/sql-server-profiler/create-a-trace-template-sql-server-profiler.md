---
title: Crear una plantilla de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f37369821585845d63bd4d416b1868364045680f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63255777"
---
# <a name="create-a-trace-template-sql-server-profiler"></a>Crear una plantilla de seguimiento (SQL Server Profiler)
  En este tema se describe cómo crear una plantilla de seguimiento nueva mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-create-a-trace-template"></a>Para crear una plantilla de seguimiento  
  
1.  En el menú **Archivo** , haga clic en **Plantillas**y, a continuación, en **Nueva plantilla**.  
  
2.  En el cuadro de diálogo **Propiedades de la plantilla de seguimiento** , seleccione un tipo de servidor en la lista **Seleccionar tipo de servidor**.  
  
3.  En el cuadro **Nuevo nombre de plantilla** , escriba un nombre para la plantilla.  
  
4.  También puede hacer clic en **Basar plantilla nueva en una existente**y, a continuación, seleccionar una plantilla de la lista.  
  
     Todos los eventos, las columnas de datos y los filtros se establecen inicialmente tal como se especifica en la plantilla seleccionada.  
  
5.  También puede hacer clic en **Usar como plantilla predeterminada para tipo de servidor seleccionado**.  
  
6.  En la pestaña **Selección de eventos** , podrá agregar, quitar o modificar eventos, columnas de datos o filtros.  
  
7.  En el menú **Selección de eventos**, utilice el control de cuadrículas para agregar o quitar eventos y columnas de datos del archivo de seguimiento tal como se indica a continuación:  
  
    -   Para agregar un evento, expanda la categoría de evento correspondiente en la columna **Eventos** y seleccione el nombre del evento.  
  
    -   Cuando se agrega un evento se incluyen de manera predeterminada todas las columnas de datos pertinentes. Para eliminar una columna de datos de un evento del seguimiento, desactive la casilla de la columna de datos del evento.  
  
    -   Para agregar filtros, haga clic en el nombre de la columna de datos y especifique los criterios del filtro en el cuadro de diálogo **Editar filtro** . También puede hacer clic con el botón derecho en el nombre de la columna de datos y hacer clic en **Editar filtro de columna** para abrir el cuadro de diálogo **Editar filtro** . Haga clic en **Aceptar** para agregar el filtro.  
  
8.  Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar eventos y columnas de datos para un archivo de seguimiento &#40;SQL Server Profiler&#41;](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un seguimiento en ejecución &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un archivo o tabla de seguimiento &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
