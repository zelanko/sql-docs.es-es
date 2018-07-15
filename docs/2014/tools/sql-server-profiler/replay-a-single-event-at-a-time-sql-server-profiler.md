---
title: Reproducir un único evento cada vez (SQL Server Profiler) | Microsoft Docs
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
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5424a91d2672710a593555c937157a4501469e4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299355"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>Reproducir un único evento cada vez (SQL Server Profiler)
  En este tema se describe cómo reproducir un solo evento cada vez en un archivo o tabla de reproducción de seguimientos mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-replay-a-single-event-at-a-time"></a>Para reproducir un solo evento cada vez  
  
1.  Abra el archivo o la tabla de seguimiento que desea reproducir. Para obtener más información, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) o [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Asegúrese de que el archivo o la tabla de seguimiento que abre contiene las clases de evento necesarias para la reproducción. Para más información, consulte [Replay Requirements](replay-requirements.md).  
  
2.  En el menú **Reproducir** , haga clic en **Paso**y conéctese a la instancia de servidor en el que desea reproducir el seguimiento.  
  
3.  Compruebe la configuración en el cuadro de diálogo **Configuración de reproducción** y haga clic en **Aceptar**. Para obtener más información sobre cómo especificar la configuración en el cuadro de diálogo **Configuración de reproducción**, vea [Reproducir un archivo de seguimiento &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md) o [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md).  
  
4.  Para reproducir el primer evento, haga clic en **Aceptar** en el cuadro de diálogo **Configuración de reproducción** .  
  
5.  Para reproducir eventos posteriores, en el menú **Reproducir** , haga clic en **Paso**o pulse F10. Vuelva a hacer clic en **Paso** o pulse F10 para cada evento.  
  
## <a name="see-also"></a>Vea también  
 [Reproducir seguimientos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
