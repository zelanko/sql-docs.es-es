---
title: Pausar un seguimiento (SQL Server Profiler) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07c66a2907d0e0d6b75e413959256133156b67a6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar un seguimiento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Pausar un seguimiento impide la aún más los datos de evento captura de hasta que se reinicie el seguimiento.  
  
 La pausa de un seguimiento impide la captura de datos de eventos hasta que se vuelve a iniciar. Al iniciarlo de nuevo se reanudan las operaciones de seguimiento. Tras reiniciar una traza, no se pierden los datos capturados previamente. Cuando se vuelve a iniciar el seguimiento, se reanuda la captura de datos a partir de ese punto. Cuando un seguimiento está pausado, puede cambiar el nombre, los eventos, las columnas y los filtros. Sin embargo, no puede cambiar los destinos a los que envía los datos del seguimiento ni la conexión del servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar un seguimiento  
  
1.  Seleccione una ventana que contenga un seguimiento que se esté ejecutando.  
  
2.  En el menú **Archivo** , haga clic en **Pausar seguimiento**.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
