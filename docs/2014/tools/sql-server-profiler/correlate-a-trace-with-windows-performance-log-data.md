---
title: Correlacionar un seguimiento con los datos del registro de rendimiento de Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
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
ms.openlocfilehash: 3c8a3d7a9888423d312d578784e1f7e1ff75434d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63316309"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Correlacionar un seguimiento con los datos del registro de rendimiento de Windows
  El [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]permite abrir un registro de rendimiento de Microsoft Windows, elegir los contadores que desea correlacionar con un seguimiento y ver los contadores de rendimiento seleccionados junto con el seguimiento en la interfaz gráfica de usuario del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Al seleccionar un evento en la ventana de seguimiento, una barra vertical roja en el panel de la ventana de datos del Monitor de sistema del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica los datos del registro de rendimiento que se correlacionan con el evento de seguimiento seleccionado.  
  
 Para correlacionar un seguimiento con contadores de rendimiento, abra un archivo o una tabla de seguimiento que contenga las columnas de datos **StartTime** y **EndTime** y luego haga clic en **Importar datos de rendimiento** del menú [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]Archivo**de**. Puede abrir un registro de rendimiento y seleccionar los objetos y contadores del Monitor de sistema que desea correlacionar con el seguimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Establecer correlaciones de un seguimiento con datos del registro de rendimiento de Windows &#40;SQL Server Profiler&#41;](correlate-a-trace-with-windows-performance-log-data.md)  
  
  
