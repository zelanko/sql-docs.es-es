---
title: Correlacionar un seguimiento con los datos del registro de rendimiento de Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d8806911251c15a8de0e7f71f032038c8686df4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217845"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Correlacionar un seguimiento con los datos del registro de rendimiento de Windows
  El [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]permite abrir un registro de rendimiento de Microsoft Windows, elegir los contadores que desea correlacionar con un seguimiento y ver los contadores de rendimiento seleccionados junto con el seguimiento en la interfaz gráfica de usuario del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Al seleccionar un evento en la ventana de seguimiento, una barra vertical roja en el panel de la ventana de datos del Monitor de sistema del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica los datos del registro de rendimiento que se correlacionan con el evento de seguimiento seleccionado.  
  
 Para correlacionar un seguimiento con contadores de rendimiento, abra un archivo o una tabla de seguimiento que contenga las columnas de datos **StartTime** y **EndTime** data columns, y then click **Importar datos de rendimiento** del menú [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **del** . Puede abrir un registro de rendimiento y seleccionar los objetos y contadores del Monitor de sistema que desea correlacionar con el seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Establecer correlaciones de un seguimiento con datos del registro de rendimiento de Windows &#40;SQL Server Profiler&#41;](correlate-a-trace-with-windows-performance-log-data.md)  
  
  
