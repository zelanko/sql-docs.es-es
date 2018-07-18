---
title: Creación de seguimientos de Profiler para reproducción (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d5928325ffe5b0b98da2058529b1cbb036a445be
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031643"
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
  
-   La clase de evento Discover Begin con todas sus columnas de datos. La columna TextData proporciona el \<RequestType > parte de la solicitud de descubrimiento y la columna RequestProperties proporciona las \<Propiedades > parte de la solicitud de descubrimiento. La columna EventSubclass proporciona el tipo de descubrimiento. Para más información, consulte [Discover Events Data Columns](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
-   La clase de evento Discover End con todas sus columnas de datos. Esta clase de evento comprueba el estado de la solicitud de descubrimiento. Para más información, consulte [Discover Events Data Columns](../../analysis-services/trace-events/discover-events-data-columns.md).  
  
## <a name="replay-for-commands"></a>Reproducir comandos  
 Para reproducir comandos, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe capturar los siguientes eventos:  
  
-   La clase de evento Command Begin con todas sus columnas de datos. La columna TextData proporciona los detalles del comando, como el tipo de proceso, el identificador de la base de datos y el identificador del cubo. La columna RequestParameters proporciona los parámetros para el comando parametrizado, y la columna RequestProperties proporciona las propiedades de una solicitud de XMLA. Para más información, consulte [Command Events Data Columns](../../analysis-services/trace-events/command-events-data-columns.md).  
  
-   La clase de evento Command End con todas sus columnas de datos. Esta clase de evento comprueba el estado del comando. Para más información, consulte [Command Events Data Columns](../../analysis-services/trace-events/command-events-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [Introducción a la supervisión de Analysis Services con SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  
