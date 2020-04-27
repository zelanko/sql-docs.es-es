---
title: Modificar una plantilla de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- modifying traces
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64c13b9fed062b73de7ab35ef5048ae4b68e5618
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66090000"
---
# <a name="modify-a-trace-template-sql-server-profiler"></a>Modificar una plantilla de seguimiento (SQL Server Profiler)
  En este tema se explica cómo modificar una plantilla de seguimiento mediante [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
### <a name="to-modify-a-trace-template"></a>Para modificar una plantilla de seguimiento  
  
1.  En el menú **Archivo** , seleccione **Plantillas**y haga clic en **Editar plantilla**.  
  
2.  En el cuadro de diálogo **Propiedades de la plantilla de seguimiento** , en la pestaña **General** , modifique el tipo de servidor y el nombre de la plantilla si es necesario o elija una plantilla predeterminada para el tipo de servidor.  
  
3.  En la pestaña **selección de eventos**, utilice el control de cuadrícula para agregar o quitar eventos y columnas de datos del archivo de seguimiento como se indica a continuación.  
  
    -   Para agregar un evento, expanda la categoría de evento correspondiente en la columna **Eventos** y seleccione el nombre del evento.  
  
    -   Cuando se agrega un evento se incluyen de manera predeterminada todas las columnas de datos pertinentes. Para eliminar una columna de datos de un evento del seguimiento, desactive la casilla de la columna de datos del evento.  
  
    -   Para agregar filtros, haga clic en el nombre de la columna de datos y especifique los criterios del filtro en el cuadro de diálogo **Editar filtro** . También puede hacer clic con el botón derecho en el nombre de la columna de datos y hacer clic en **Editar filtro de columna** para abrir el cuadro de diálogo **Editar filtro** . Haga clic en **Aceptar** para agregar el filtro.  
  
4.  Haga clic en **Guardar**o bien en **Guardar As**si desea guardar la plantilla de seguimiento con otro nombre.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar eventos y columnas de datos para un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un seguimiento en ejecución &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un archivo de seguimiento o de una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler plantillas y permisos](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
