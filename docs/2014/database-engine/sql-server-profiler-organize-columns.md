---
title: SQL Server Profiler - organizar columnas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.organize.columns.f1
ms.assetid: bf5674f4-da5e-43f9-aeb2-76ca37993790
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f0ad3d1204e8c27d91ecb3b586d56a27d45eeb4e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089755"
---
# <a name="sql-server-profiler---organize-columns"></a>SQL Server Profiler (Organizar columnas)
  Utilice el cuadro de diálogo **Organizar columnas** para seleccionar columnas de datos y agrupar o agregar eventos que se muestran en un seguimiento; esto facilita la lectura y el análisis de los archivos o tablas de seguimiento grandes.  
  
 La agregación mueve y contrae todos los eventos del seguimiento bajo su tipo de clase de evento correspondiente. A la izquierda del nombre de clase de eventos aparece un signo más (**+**). Si hace clic en el signo más, expande la clase de evento y puede ver todos sus eventos.  
  
 La agrupación organiza todas las clases de evento de un tipo específico en una ventana de seguimiento. Sin embargo, los eventos no se contraen bajo el tipo de clase de evento.  
  
 Cuando agrupa o agrega eventos en una ventana de seguimiento, las columnas seleccionadas para agrupar o agregar permanecen fijas en la ventana, pero puede desplazarse a la derecha o la izquierda para ver las demás columnas de datos.  
  
 Para tener acceso a este cuadro de diálogo, abra un archivo o una tabla de seguimiento existente y haga clic en **Propiedades** en el menú [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] **del** . En el cuadro de diálogo **Propiedades de seguimiento** , haga clic en la pestaña **Selección de eventos** y, a continuación, haga clic en **Organizar columnas**. También puede hacer clic en **Organizar columnas** en la pestaña **Selección de eventos** cuando crea un nuevo seguimiento.  
  
## <a name="options"></a>Opciones  
 **Grupos**  
 Desplaza los nombres de columnas de datos bajo **Grupos** para agrupar o agregar clases de eventos en la ventana de seguimiento.  
  
 Para agregar eventos, desplace una columna de datos a **Grupos**. De este modo, todos los eventos de un tipo específico se contraen bajo el nombre del tipo de clase de evento en la ventana de seguimiento. A la izquierda del nombre de clase de eventos aparece un signo más (**+**). Haga clic en el signo más para expandir el tipo de clase de evento y ver todos sus eventos. Puede activar y desactivar la agregación y la agrupación si hace clic en **Vista agregada** o **Vista agrupada** en el menú **Ver** .  
  
 Para agrupar eventos, desplace varias columnas de datos a **Grupos**. De este modo, todos los eventos de un tipo específico se agrupan en la ventana de seguimiento, pero no se contraen bajo el nombre del tipo de clase de evento. Puede cambiar entre una vista agrupada y una vista no agrupada si hace clic en **Vista agrupada** en el menú Ver. Cuando se desplaza más de una columna de datos a **Grupos**, la opción para cambiar a **Vista agregada** deja de estar disponible.  
  
 **Columnas**  
 Muestra las columnas de datos que se pueden desplazar a **Grupos**. Haga clic en el signo más (**+**) situado a la izquierda de **Columnas** para expandir la lista.  
  
 **Subir**  
 Después de seleccionar una columna de datos, haga clic en **Subir** para subir las columnas a **Grupos**. También puede hacer clic en **Subir** para volver a organizar la visualización de las columnas en la ventana de seguimiento.  
  
 **Bajar**  
 Después de seleccionar una columna de datos, haga clic en **Bajar** para quitar las columnas de **Grupos**. También puede hacer clic en **Bajar** para volver a organizar la visualización de las columnas en la ventana de seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Organizar las columnas mostradas en un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)   
 [Crear un seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Crear una plantilla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  
