---
title: Pausar un seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d213e6b680bfe0d020a7c95b4e3924ef5679d7e2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077105"
---
# <a name="pause-a-trace-sql-server-profiler"></a>Pausar un seguimiento (SQL Server Profiler)
  La pausa de un seguimiento impide la captura de más datos de eventos hasta que se vuelva a iniciar.  
  
 La pausa de un seguimiento impide la captura de datos de eventos hasta que se vuelve a iniciar. Al iniciarlo de nuevo se reanudan las operaciones de seguimiento. Tras reiniciar una traza, no se pierden los datos capturados previamente. Cuando se vuelve a iniciar el seguimiento, se reanuda la captura de datos a partir de ese punto. Cuando un seguimiento está pausado, puede cambiar el nombre, los eventos, las columnas y los filtros. Sin embargo, no puede cambiar los destinos a los que envía los datos del seguimiento ni la conexión del servidor.  
  
### <a name="to-pause-a-trace"></a>Para pausar un seguimiento  
  
1.  Seleccione una ventana que contenga un seguimiento que se esté ejecutando.  
  
2.  En el menú **Archivo** , haga clic en **Pausar seguimiento**.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
