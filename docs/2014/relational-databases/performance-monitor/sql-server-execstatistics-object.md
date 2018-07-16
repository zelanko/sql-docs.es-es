---
title: ExecStatistics (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1424f6044e384f7d5c279908ac28129f9426281b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302405"
---
# <a name="sql-server-execstatistics-object"></a>ExecStatistics (objeto de SQL Server)
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
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
