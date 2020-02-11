---
title: Usar SQL Server Profiler para supervisar Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 8b77dafc-4584-4e93-8ad7-299304391bfd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2a042d49dc8222c0357c6fde6077153c40b11b53
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079528"
---
# <a name="use-sql-server-profiler-to-monitor-analysis-services"></a>Usar SQL Server Profiler para supervisar Analysis Services
  
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] realiza un seguimiento de los eventos de procesos del motor, como el inicio de un lote o una transacción, y captura datos sobre estos eventos, lo que permite supervisar la actividad del servidor y de la base de datos (por ejemplo, consultas del usuario o actividad de inicio de sesión). Puede capturar datos del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] en un archivo o una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para su análisis posterior y también reproducir los eventos capturados en la misma instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o en otra, para ver qué sucedió exactamente. Puede reproducir eventos en tiempo real o paso a paso. También resulta útil ejecutar los eventos de seguimiento junto con los contadores de Rendimiento en el mismo equipo. El analizador puede correlacionar los dos basándose en el tiempo y mostrarlos juntos en una misma línea temporal. Los eventos de seguimiento proporcionan más detalles, mientras que los contadores de Rendimiento ofrecen una vista agregada. Para obtener información sobre cómo crear y ejecutar seguimientos, vea [Crear seguimientos del generador de perfiles para su reproducción &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md).  
  
 En la tabla siguiente se describen los temas de esta sección.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Introducción a Supervisar Analysis Services con SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|Describe cómo utilizar el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para supervisar una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Crear seguimientos del generador de perfiles para la reproducción &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md)|Describe los requisitos para crear un seguimiento para la reproducción mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Eventos de seguimiento de Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)|Describe las clases de evento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Estas clases de evento se asignan a las acciones generadas por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y se utilizan para las reproducciones de seguimientos.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar una instancia de Analysis Services](monitor-an-analysis-services-instance.md)  
  
  
