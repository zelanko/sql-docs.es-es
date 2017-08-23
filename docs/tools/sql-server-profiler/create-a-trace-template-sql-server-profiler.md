---
title: Crear una plantilla de seguimiento (SQL Server Profiler) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- saving trace template
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4834d9022ec4ea6f1b97220a38a9b84f4634dbe5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

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
  
## <a name="see-also"></a>Vea también  
 [Especificar eventos y columnas de datos para un archivo de seguimiento &#40; Analizador de SQL Server &#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Derivar una plantilla a partir de un seguimiento en ejecución &#40; Analizador de SQL Server &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivar una plantilla de un archivo de seguimiento o tabla de seguimiento &#40; Analizador de SQL Server &#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
