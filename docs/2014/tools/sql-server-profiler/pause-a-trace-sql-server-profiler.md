---
title: Pausar un seguimiento (SQL Server Profiler) | Microsoft Docs
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
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a549cc7193adb9708719a0675397baa2ff5d4d3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178997"
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar un seguimiento (SQL Server Profiler)
  La pausa de un seguimiento impide la captura de más datos de eventos hasta que se vuelva a iniciar.  
  
 La pausa de un seguimiento impide la captura de datos de eventos hasta que se vuelve a iniciar. Al iniciarlo de nuevo se reanudan las operaciones de seguimiento. Tras reiniciar una traza, no se pierden los datos capturados previamente. Cuando se vuelve a iniciar el seguimiento, se reanuda la captura de datos a partir de ese punto. Cuando un seguimiento está pausado, puede cambiar el nombre, los eventos, las columnas y los filtros. Sin embargo, no puede cambiar los destinos a los que envía los datos del seguimiento ni la conexión del servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar un seguimiento  
  
1.  Seleccione una ventana que contenga un seguimiento que se esté ejecutando.  
  
2.  En el menú **Archivo** , haga clic en **Pausar seguimiento**.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
