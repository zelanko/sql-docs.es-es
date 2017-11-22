---
title: "Reproducir hasta un punto de interrupción (SQL Server Profiler) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a727831b7231e07378f5eba9436ea5e48f4167c1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>Reproducir hasta un punto de interrupción (SQL Server Profiler)
  En este tema se describe cómo establecer puntos de interrupción en una tabla o archivo de seguimiento que desee reproducir mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. El establecimiento de puntos de interrupción en un seguimiento o archivo de seguimiento antes de comenzar la reproducción del seguimiento permite poner en pausa la reproducción del seguimiento en determinados eventos. El uso de puntos de interrupción durante la reproducción de un seguimiento permite usar la depuración, ya que la reproducción de scripts de seguimiento largos se puede dividir en segmentos cortos que se pueden analizar de forma incremental.  
  
### <a name="to-replay-to-a-breakpoint"></a>Para reproducir hasta un punto de interrupción  
  
1.  Abra el archivo o la tabla de seguimiento que desea reproducir. Para obtener más información, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) o [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Asegúrese de que el archivo o la tabla de seguimiento que abre contiene las clases de evento necesarias para la reproducción. Para más información, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  En la ventana de seguimiento, haga clic en el evento que desee utilizar como punto de interrupción. Para establecer un punto de interrupción, utilice uno de estos tres métodos:  
  
    -   Presione F9.  
  
    -   En el menú **Reproducir** , haga clic en **Alternar punto de interrupción**.  
  
    -   Haga clic con el botón derecho en el evento y luego haga clic en **Alternar puntos de interrupción**.  
  
     Un punto rojo aparece junto al evento de seguimiento seleccionado para indicar que se trata del punto de interrupción del seguimiento.  
  
     Repita este paso para establecer varios puntos de interrupción.  
  
3.  En el menú **Reproducir** , haga clic en **Iniciar**y conéctese al servidor en el que desee reproducir el seguimiento.  
  
4.  Compruebe la configuración en el cuadro de diálogo **Configuración de reproducción** y haga clic en **Aceptar**.  
  
     Se inicia la reproducción, que se pone en pausa al alcanzar el punto de interrupción.  
  
5.  Presione F5 para reanudar la reproducción y continuar hasta el siguiente punto de interrupción.  
  
6.  Repita el paso 5 hasta el final del seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Reproducir hasta un cursor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)   
 [Reproducir seguimientos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
