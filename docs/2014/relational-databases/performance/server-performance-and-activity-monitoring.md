---
title: Supervisión de la actividad y rendimiento del servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e60d85e4c80d550ed281856c7cc22d8255a253ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221405"
---
# <a name="server-performance-and-activity-monitoring"></a>Supervisión de la actividad y rendimiento del servidor
  El objetivo de supervisar bases de datos es evaluar el rendimiento de un servidor. Una supervisión eficaz implica tomar instantáneas periódicas del rendimiento actual para aislar procesos que causan problemas y recopilar datos de forma continua a lo largo del tiempo para realizar el seguimiento de las tendencias de rendimiento. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows proporcionan utilidades que permiten ver la condición actual de la base de datos y realizar un seguimiento del rendimiento a medida que las condiciones cambian.  
  
 La sección siguiente contiene temas que describen cómo utilizar las herramientas de supervisión de la actividad y el rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Windows. Incluye los temas siguientes:  
  
## <a name="in-this-section"></a>En esta sección  
 **Para realizar tareas de supervisión con herramientas de Windows**  
  
-   [Iniciar el Monitor de sistema &#40;Windows&#41;](start-system-monitor-windows.md)  
  
-   [Ver el registro de aplicación de Windows &#40;Windows&#41;](view-the-windows-application-log-windows-10.md)  
  
 **Para crear alertas de bases de datos de SQL Server con herramientas de Windows**  
  
-   [Configurar una alerta de base de datos de SQL Server &#40;Windows&#41;](set-up-a-sql-server-database-alert-windows.md)  
  
 **Para realizar tareas de supervisión con SQL Server Management Studio**  
  
-   [Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
-   [Abrir el Monitor de actividad &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **Para realizar tareas de supervisión con Seguimiento de SQL mediante procedimientos almacenados de Transact-SQL**  
  
-   [Crear un seguimiento &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)  
  
-   [Establecer un filtro de seguimiento &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
-   [Modificar un seguimiento existente &#40;Transact-SQL&#41;](../sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [Ver un seguimiento guardado &#40;Transact-SQL&#41;](../sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [Ver la información del filtro &#40;Transact-SQL&#41;](../sql-trace/view-filter-information-transact-sql.md)  
  
-   [Eliminar un seguimiento &#40;Transact-SQL&#41;](../sql-trace/delete-a-trace-transact-sql.md)  
  
 **Para crear y modificar seguimientos mediante SQL Server Profiler**  
  
-   [Crear un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [Establecer opciones globales de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [Especificar eventos y columnas de datos para un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [Crear un script de Transact-SQL para ejecutar un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [Guardar los resultados de un seguimiento en un archivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [Establecer un tamaño máximo de archivo para un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [Guardar los resultados de un seguimiento en una tabla &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [Establecer un tamaño máximo de tabla para una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [Filtrar eventos en un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [Ver información de un filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [Modificar un filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [Filtrar eventos basándose en la hora de inicio del evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [Filtrar eventos basándose en la hora de finalización del evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [Filtrar los Id. de proceso de servidor &#40;SPID&#41; en un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [Organizar las columnas mostradas en un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **Para iniciar, pausar y detener seguimientos mediante SQL Server Profiler**  
  
-   [Iniciar un seguimiento automáticamente después de conectarse a un servidor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [Pausar un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [Detener un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [Ejecutar un seguimiento después de haberlo pausado o detenido &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **Para abrir seguimientos y configurar cómo se visualizan los seguimientos mediante SQL Server Profiler**  
  
-   [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [Borrar el contenido de una ventana de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [Cerrar una ventana de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [Configurar los valores predeterminados de definición de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [Establecer los valores predeterminados de presentación de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **Para reproducir seguimientos mediante SQL Server Profiler**  
  
-   [Reproducir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [Reproducir un único evento cada vez &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [Reproducir hasta un punto de interrupción &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [Reproducir hasta un cursor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Reproducir un script Transact-SQL &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **Para crear, modificar y utilizar plantillas de seguimientos mediante SQL Server Profiler**  
  
-   [Crear una plantilla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [Modificar una plantilla de seguimiento &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
-   [Derivar una plantilla a partir de un seguimiento en ejecución &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [Derivar una plantilla a partir de un archivo o tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [Exportar una plantilla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [Importar una plantilla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **Para utilizar seguimientos de SQL Server Profiler para recopilar y supervisar el rendimiento del servidor**  
  
-   [Buscar un valor o una columna de datos durante la ejecución de un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Guardar gráficos de interbloqueo &#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Guardar eventos Showplan XML por separado &#40;SQL Server Profiler&#41;](save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Guardar de forma separada eventos Showplan XML Statistics Profile &#40;SQL Server Profiler&#41;](save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [Extraer un script de un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [Establecer correlaciones de un seguimiento con datos del registro de rendimiento de Windows &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
