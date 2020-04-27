---
title: Reproducir hasta un cursor (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c4c4b9d2e2e07c53f850fe545d803fa411dbbc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63267486"
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>Reproducir hasta un cursor (SQL Server Profiler)
  En este tema se describe cómo reproducir archivos o tablas de seguimiento que se ponen en pausa al alcanzar un cursor mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. La pausa de seguimientos en cursores es compatible con la depuración porque la reproducción de scripts de seguimiento largos se puede dividir en segmentos cortos que se pueden analizar de forma incremental.  
  
### <a name="to-replay-to-the-cursor"></a>Para reproducir hasta el cursor  
  
1.  Abra el archivo o la tabla de seguimiento que desea reproducir. Para obtener más información, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) o el Asistente para la optimización del [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Asegúrese de que el archivo o la tabla de seguimiento que abre contiene las clases de evento necesarias para la reproducción. Para más información, consulte [Replay Requirements](replay-requirements.md).  
  
2.  En la ventana de seguimiento, haga clic en un evento.  
  
3.  En el menú **Reproducir** , haga clic en **Ejecutar hasta el cursor**y, a continuación, conéctese al servidor en el que desea reproducir el seguimiento.  
  
4.  Compruebe la configuración en el cuadro de diálogo **Configuración de reproducción** y haga clic en **Aceptar**.  
  
     Se inicia la reproducción, que se pone en pausa al alcanzar el primer cursor.  
  
5.  Presione F5 para reanudar el seguimiento.  
  
6.  Repita el paso 5 hasta el final del seguimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Reproducir hasta un punto de interrupción &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)   
 [Reproducir seguimientos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
