---
title: Configuración de SQL Server Profiler-reproducción (opciones avanzadas de reproducción) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 78ca3fc2d11b22d70c8a4e99d0961f793870bd53
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928521"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>SQL Server Profiler (Configuración de reproducción/página Opciones avanzadas de reproducción)
  En el cuadro de diálogo **Configuración de reproducción** , utilice la pestaña **Opciones avanzadas de reproducción** para especificar cómo reproducir un archivo de seguimiento.  
  
 Para ver esta ventana, utilice el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para abrir un seguimiento o un archivo de seguimiento que contenga los eventos adecuados para la reproducción. Para más información, consulte [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md). Cuando el archivo o tabla de seguimiento esté abierto, en el menú **Reproducir** , haga clic en **Iniciar**, establezca la conexión con la sesión de SQL Server donde desea reproducir el seguimiento y haga clic en la pestaña **Opciones avanzadas de reproducción** .  
  
## <a name="options"></a>Opciones  
 **Reproducir los SPID del sistema**  
 Especifica si el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] reproduce identificadores de proceso del sistema (SPID).  
  
 **Reproducir solo un SPID**  
 Solo reproduce la actividad del archivo de seguimiento de origen relacionada con el SPID seleccionado.  
  
 **SPID para reproducir**  
 Especifique el SPID que desea reproducir.  
  
 **Limitar reproducción por fecha y hora**  
 Active esta opción para reproducir solo una parte del archivo de seguimiento de origen.  
  
 **Hora de inicio**  
 Fecha y hora en que debe comenzar la reproducción del archivo de seguimiento de origen.  
  
 **Hora de finalización**  
 Fecha y hora en que debe detenerse la reproducción del archivo de seguimiento de origen.  
  
 **Intervalo de espera del monitor de estado (seg.)**  
 Especifique el intervalo de espera de la reproducción en segundos. El valor predeterminado es 3600 segundos (1 hora). Esta configuración afecta al tiempo que puede ejecutarse un proceso antes de que lo finalice el monitor de estado.  
  
 **Intervalo de sondeo del monitor de estado (seg.)**  
 Especifique el intervalo de sondeo del monitor de estado durante la reproducción en segundos. El valor predeterminado es 60 segundos. Este valor permite al usuario configurar la frecuencia con que el monitor de estado sondea los candidatos para terminar.  
  
 **Habilitar monitor de procesos bloqueados de SQL Server**  
 Habilita un proceso que busca procesos bloqueados o de bloqueo.  
  
 **Intervalo de espera del monitor de procesos bloqueados (seg.)**  
 Configura la frecuencia con que el monitor de procesos bloqueados busca procesos bloqueados o de bloqueo.  
  
## <a name="see-also"></a>Consulte también  
 [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproducir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Reproducir seguimientos](../tools/sql-server-profiler/replay-traces.md)  
  
  
