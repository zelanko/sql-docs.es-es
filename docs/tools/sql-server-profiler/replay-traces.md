---
title: Reproducir seguimientos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Profiler, replaying traces
- Run to Cursor option
- Toggle Breakpoint option
- traces [SQL Server], replaying
- replaying traces
- playback engine [SQL Server Profiler]
- events [SQL Server], replaying traces
- Profiler [SQL Server Profiler], replaying traces
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
caps.latest.revision: "29"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eca1952d968ef9ca864f69f48b17ed20cfa45938
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="replay-traces"></a>Reproducir seguimientos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]La reproducción es la capacidad de reproducir la actividad capturada en un seguimiento. Al crear o modificar un seguimiento, puede guardarlo para reproducirlo posteriormente. Puede utilizar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para reproducir la actividad de seguimiento de un equipo único. Para las cargas de trabajo grandes, emplee la utilidad Distributed Replay para reproducir la información de seguimiento de varios equipos.  
  
 En esta sección se describe cómo utilizar las características de reproducción de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Para obtener más información sobre la utilidad Distributed Replay, vea [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
 El [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] incluye un motor de reproducción de varios subprocesos que puede simular conexiones de usuario y la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La reproducción es útil para solucionar problemas de aplicaciones o procesos. Cuando haya identificado el problema e implementado las acciones para corregirlo, ejecute el seguimiento que encontró el posible problema en la aplicación o proceso corregido. A continuación, reproduzca el seguimiento original y compare los resultados.  
  
 La reproducción de seguimientos admite la depuración por medio de las opciones **Alternar punto de interrupción** y **Ejecutar hasta el cursor** del menú [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **del** . Estas opciones ofrecen mejoras especialmente en el análisis de scripts largos, ya que pueden dividir la reproducción del seguimiento en segmentos más cortos para analizarlos de forma incremental.  
  
 Para obtener más información sobre los permisos necesarios para reproducir un seguimiento, vea [Permisos necesarios para ejecutar SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Requisitos de reproducción](../../tools/sql-server-profiler/replay-requirements.md)|Describe los eventos que se deben incluir en una definición de seguimiento para reproducirla con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Opciones de reproducción &#40; Analizador de SQL Server &#41;](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|Describe las opciones del cuadro de diálogo **Configuración de reproducción** del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Consideraciones para reproducir seguimientos &#40; Analizador de SQL Server &#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|Describe los eventos de seguimiento que no se pueden reproducir con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y los efectos de reproducir seguimientos en el rendimiento del servidor.|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
