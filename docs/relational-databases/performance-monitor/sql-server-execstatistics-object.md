---
title: ExecStatistics (objeto de SQL Server) | Microsoft Docs
description: Obtenga información sobre el objeto SQLServer:ExecStatistics, que proporciona contadores para supervisar diversas ejecuciones.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 67ef3667057a2cb5e2507d89a515814d2ea427e6
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505743"
---
# <a name="sql-server-execstatistics-object"></a>ExecStatistics (objeto de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
