---
title: "Categoría de eventos de procesamiento de consultas | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: a94b3198-be85-4935-845d-1cd4e121fc94
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 462d9a67cf2a56aaf46fb4106ec786c1d003d8a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="query-processing-events-category"></a>Procesamiento de consultas (categoría de eventos)
  La categoría de eventos Procesamiento de consultas contiene las clases de eventos que se describen en la siguiente tabla.  
  
|**Clase de eventos**|**Identificador del evento**|**Description**|  
|---------------------|------------------|---------------------|  
|Query Subcube|11|Consulta de subcubo para optimización basada en el uso.|  
|Query Subcube Verbose|12|Consulta de subcubo con información detallada. Este evento puede tener un impacto negativo en el rendimiento cuando está activado.|  
|Get Data From Aggregation|60|Responde a la consulta obteniendo datos de agregación. Este evento puede tener un impacto negativo en el rendimiento cuando está activado.|  
|Get Data From Cache|61|Responde a la consulta obteniendo datos de una de las memorias caché. Este evento puede tener un impacto negativo en el rendimiento cuando está activado.|  
|Query Cube Begin|70|Recopila todos los eventos Inicio de consulta de cubo desde que comenzó el seguimiento.|  
|Query Cube End|71|Recopila todos los eventos Final de consulta de cubo desde que comenzó el seguimiento.|  
|Calculate Non Empty Begin|72|Inicio de calcular no vacío.|  
|Calculate Non Empty Current|73|Calcular no vacío en curso.|  
|Calculate Non Empty End|74|Final de calcular no vacío.|  
|Serialize Results Begin|75|Inicio de serializar resultados.|  
|Serialize Results Current|76|Serializar resultados en curso.|  
|Serialize Results End|77|Final de serializar resultados.|  
|Execute MDX Script Begin|78|Inicio de ejecutar script MDX.|  
|Execute MDX Script Current|79|Ejecutar script MDX en curso.|  
|Execute MDX Script End|80|Final de ejecutar script MDX.|  
|Query Dimension|81|Consultar dimensión.|  
|VertiPaq SE Query Begin|82|Consulta de VertiPaq SE.|  
|VertiPaq SE Query End|83|Consulta de VertiPaq SE.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de evento de Procesamiento de consultas, vea [Query Processing Events Data Columns](../../analysis-services/trace-events/query-processing-events-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
