---
title: Reproducir un único evento cada vez (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab6d5c64ab1f154e0b31cabfe89ba9aa095bf376
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800014"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>Reproducir un único evento cada vez (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo reproducir un solo evento cada vez en un archivo o tabla de reproducción de seguimientos mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-replay-a-single-event-at-a-time"></a>Para reproducir un solo evento cada vez  
  
1.  Abra el archivo o la tabla de seguimiento que desea reproducir. Para obtener más información, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) o el Asistente para la optimización del [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Asegúrese de que el archivo o la tabla de seguimiento que abre contiene las clases de evento necesarias para la reproducción. Para más información, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  En el menú **Reproducir** , haga clic en **Paso**y conéctese a la instancia de servidor en el que desea reproducir el seguimiento.  
  
3.  Compruebe la configuración en el cuadro de diálogo **Configuración de reproducción** y haga clic en **Aceptar**. Para obtener más información sobre cómo especificar la configuración en el cuadro de diálogo **Configuración de reproducción**, vea [Reproducir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md) o [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md).  
  
4.  Para reproducir el primer evento, haga clic en **Aceptar** en el cuadro de diálogo **Configuración de reproducción** .  
  
5.  Para reproducir eventos posteriores, en el menú **Reproducir** , haga clic en **Paso**o pulse F10. Vuelva a hacer clic en **Paso** o pulse F10 para cada evento.  
  
## <a name="see-also"></a>Ver también  
 [Reproducir seguimientos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
