---
title: "Crear seguimientos del generador de perfiles para su reproducción (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/23/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4fa41a17d09371375ea9b5193542a8df2fc216a4
ms.sourcegitcommit: 3206a31870f8febab7d1718fa59fe0590d4d45db
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>Crear seguimientos del generador de perfiles para su reproducción (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Para responder a consultas, detecciones y comandos enviados por los usuarios a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe recopilar los eventos necesarios. Para iniciar la recopilación de estos eventos, deben estar seleccionadas las clases de evento adecuadas en la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades de seguimiento** . Por ejemplo, si la clase de evento Query Begin está seleccionada, los eventos que contienen consultas se recopilan y utilizan para su reproducción. Igualmente, el archivo de seguimiento contiene información suficiente para admitir la reproducción de transacciones de servidor en un entorno distribuido de la secuencia original de transacciones.  
  
## <a name="replay-for-queries"></a>Reproducir consultas  
 Para reproducir consultas, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Audit Login con todas sus columnas de datos. Esta clase de evento proporciona información sobre qué usuario ha iniciado la sesión y sobre la configuración de la misma. El Id. de proceso del servidor (SPID) proporciona la referencia a la sesión de usuario. Para más información, consulte [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
-   La clase de evento Query Begin con todas sus columnas de datos. Esta clase de evento proporciona información sobre la consulta que fue enviada a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La columna Event Subclass proporciona información sobre el tipo de consulta. La columna TextData proporciona el texto real de la consulta. La columna RequestParameters proporciona los parámetros para las consultas parametrizadas, y la columna RequestProperties proporciona las propiedades de una solicitud de XML for Analysis (XMLA). Para más información, consulte [Queries Events Data Columns](../../analysis-services/trace-events/queries-events-data-columns.md).  
  
-   La clase de evento Query End con todas sus columnas de datos. Esta clase de evento comprueba el estado de la ejecución de la consulta. Para más información, consulte [Queries Events Data Columns](../../analysis-services/trace-events/queries-events-data-columns.md).  
  
## <a name="replay-for-discovers"></a>Reproducir descubrimientos  
 Para reproducir descubrimientos, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Audit Login con todas sus columnas de datos. Esta clase de evento proporciona información sobre qué usuario ha iniciado la sesión y sobre la configuración de la misma. El SPID proporciona la referencia a la sesión de usuario. Para más información, consulte [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
-   La clase de evento Discover Begin con todas sus columnas de datos. La columna TextData proporciona el \<RequestType > parte de la solicitud de detección y la columna de RequestProperties proporciona el \<Propiedades > parte de la solicitud de descubrimiento. La columna EventSubclass proporciona el tipo de descubrimiento. Para más información, consulte [Discover Events Data Columns](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
-   La clase de evento Discover End con todas sus columnas de datos. Esta clase de evento comprueba el estado de la solicitud de descubrimiento. Para más información, consulte [Discover Events Data Columns](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
## <a name="replay-for-commands"></a>Reproducir comandos  
 Para reproducir comandos, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Command Begin con todas sus columnas de datos. La columna TextData proporciona los detalles del comando, como el tipo de proceso, el identificador de la base de datos y el identificador del cubo. La columna RequestParameters proporciona los parámetros para el comando parametrizado, y la columna RequestProperties proporciona las propiedades de una solicitud de XMLA. Para más información, consulte [Command Events Data Columns](../../analysis-services/trace-events/command-events-data-columns.md).  
  
-   La clase de evento Command End con todas sus columnas de datos. Esta clase de evento comprueba el estado del comando. Para más información, consulte [Command Events Data Columns](../../analysis-services/trace-events/command-events-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [Introducción a la supervisión de Analysis Services con SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
