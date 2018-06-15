---
title: Columnstore (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c9e2cb03070450920cae365f435ae871367ec704
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33696608"
---
# <a name="sql-server-columnstore-object"></a>Objeto Columnstore de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El objeto **SQLServer:Columnstore** proporciona contadores para supervisar la ejecución de índices de almacén de columnas en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En la siguiente tabla se describen los contadores de rendimiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore** counters.  
  
|Contadores de Columnstore|Description|  
|--------------------------|-----------------|  
|**Grupos de filas delta cerrados**|Número de grupos de filas delta cerrados.|  
|**Grupos de filas delta comprimidos**|Número de grupos de filas delta comprimidos.|  
|**Grupos de filas delta creados**|Número de grupos de filas delta creados.|  
|**Frecuencia de aciertos de caché de segmentos**|Porcentaje de segmentos de columna que se han encontrado en el grupo del almacén de columnas sin tener que incurrir en una lectura de disco.|  
|**Base de frecuencia de aciertos de caché de segmento**|Exclusivamente para uso interno.|
|**Lecturas de segmento por segundo**|Número de lecturas de segmento físico emitidas.|  
|**Total de búferes de eliminación migrados**|Número de veces que el motor de tupla ha limpiado el búfer de eliminación.|  
|**Total de evaluaciones de directiva de combinación**|Número de veces que se ha evaluado la directiva de combinación para el almacén de columnas.|  
|**Total de grupos de filas comprimidos**|Número total de grupos de filas comprimidos.|  
|**Grupos de filas totales aptas para Merge**|Número de grupos de filas de origen aptas para una operación MERGE desde el inicio de SQL Server.|  
|**Total de grupos de filas comprimidos de combinación**|Número de grupos de filas de destino comprimidos creados con MERGE desde el inicio de SQL Server.|  
|**Total de grupos de filas de origen combinados**|Número de grupos de filas de origen combinados desde el inicio de SQL Server.|  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
