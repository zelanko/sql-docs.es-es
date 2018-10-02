---
title: ExecStatistics (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 258aaee37e6e0c6bbbb0a43326a21c80712e9749
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773113"
---
# <a name="sql-server-execstatistics-object"></a>ExecStatistics (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto **SQLServer:ExecStatistics** de Microsoft SQL Server proporciona contadores para supervisar diversas ejecuciones.  
  
 En esta tabla se describen los contadores de **Exec Statistics** de SQL Server.  
  
|Contadores de Exec Statistics de SQL Server|Descripción|  
|-----------------------------------------|-----------------|  
|**Consulta distribuida**|Estadísticas relacionadas con la ejecución de consultas distribuidas.|  
|**Llamadas DTC**|Estadísticas relacionadas con la ejecución de llamadas DTC.|  
|**Procedimientos extendidos**|Estadísticas relacionadas con la ejecución de procedimientos extendidos.|  
|**Llamadas OLEDB**|Estadísticas relacionadas con la ejecución de llamadas OLEDB.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Elemento|Descripción|  
|----------|-----------------|  
|**Tiempo medio de ejecución (ms)**|Tiempo medio de ejecución del tipo de ejecución seleccionado.|  
|**Tiempo de ejecución acumulado (ms) por segundo**|Tiempo de ejecución acumulado por segundo del tipo de ejecución seleccionado.|  
|**Ejecuciones en curso**|Número de ejecuciones en curso del tipo de ejecución seleccionado.|  
|**Ejecuciones iniciadas por segundo**|Número de ejecuciones iniciadas por segundo del tipo de ejecución seleccionado.|  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
