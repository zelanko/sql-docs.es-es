---
title: Crear seguimientos del generador de perfiles para su reproducción (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- replaying queries
- replaying discovers
- events [Analysis Services]
- replaying commands
- Profiler [SQL Server Profiler], Analysis Services
- performance [Analysis Services], replays
- traces [Analysis Services]
ms.assetid: 93b2fc46-7cfb-4ab5-abeb-1475a7d6f0f2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 994fa58d9def8048f7fb88e09721055d2b184bb0
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544007"
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>Crear seguimientos del generador de perfiles para su reproducción (Analysis Services)
  Para reproducir consultas, detecciones y comandos enviados por los usuarios a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe recopilar los eventos necesarios. Para iniciar la recopilación de estos eventos, deben estar seleccionadas las clases de evento adecuadas en la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades de seguimiento** . Por ejemplo, si la clase de evento Query Begin está seleccionada, los eventos que contienen consultas se recopilan y utilizan para su reproducción. Igualmente, el archivo de seguimiento contiene información suficiente para admitir la reproducción de transacciones de servidor en un entorno distribuido de la secuencia original de transacciones.  
  
## <a name="replay-for-queries"></a>Reproducir consultas  
 Para reproducir consultas, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Audit Login con todas sus columnas de datos. Esta clase de evento proporciona información sobre qué usuario ha iniciado la sesión y sobre la configuración de la misma. El Id. de proceso del servidor (SPID) proporciona la referencia a la sesión de usuario. Para más información, consulte [Security Audit Data Columns](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns).  
  
-   La clase de evento Query Begin con todas sus columnas de datos. Esta clase de evento proporciona información sobre la consulta que fue enviada a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La columna Event Subclass proporciona información sobre el tipo de consulta. La columna TextData proporciona el texto real de la consulta. La columna RequestParameters proporciona los parámetros para las consultas parametrizadas, y la columna RequestProperties proporciona las propiedades de una solicitud de XML for Analysis (XMLA). Para más información, consulte [Queries Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns).  
  
-   La clase de evento Query End con todas sus columnas de datos. Esta clase de evento comprueba el estado de la ejecución de la consulta. Para más información, consulte [Queries Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/queries-events-data-columns).  
  
## <a name="replay-for-discovers"></a>Reproducir descubrimientos  
 Para reproducir descubrimientos, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Audit Login con todas sus columnas de datos. Esta clase de evento proporciona información sobre qué usuario ha iniciado la sesión y sobre la configuración de la misma. El SPID proporciona la referencia a la sesión de usuario. Para más información, consulte [Security Audit Data Columns](https://docs.microsoft.com/bi-reference/trace-events/security-audit-data-columns).  
  
-   La clase de evento Discover Begin con todas sus columnas de datos. La columna TextData proporciona la \<RequestType> parte de la solicitud de detección y la columna RequestProperties proporciona la \<Properties> parte de la solicitud de detección. La columna EventSubclass proporciona el tipo de descubrimiento. Para más información, consulte [Discover Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns).  
  
-   La clase de evento Discover End con todas sus columnas de datos. Esta clase de evento comprueba el estado de la solicitud de descubrimiento. Para más información, consulte [Discover Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/discover-events-data-columns).  
  
## <a name="replay-for-commands"></a>Reproducir comandos  
 Para reproducir comandos, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Command Begin con todas sus columnas de datos. La columna TextData proporciona los detalles del comando, como el tipo de proceso, el identificador de la base de datos y el identificador del cubo. La columna RequestParameters proporciona los parámetros para el comando parametrizado, y la columna RequestProperties proporciona las propiedades de una solicitud de XMLA. Para más información, consulte [Command Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns).  
  
-   La clase de evento Command End con todas sus columnas de datos. Esta clase de evento comprueba el estado del comando. Para más información, consulte [Command Events Data Columns](https://docs.microsoft.com/bi-reference/trace-events/command-events-data-columns).  
  
## <a name="see-also"></a>Consulte también  
 [Eventos de seguimiento de Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [Introducción a Supervisar Analysis Services con SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
