---
title: Wait Statistics (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 28e7ee81273d47e285b9903575bdc40ccededbb5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151020"
---
# <a name="sql-server-wait-statistics-object"></a>Wait Statistics (objeto de SQL Server)
  El objeto de rendimiento de **SQLServer:Wait Statistics** contiene contadores de rendimiento que ofrecen información sobre el estado de la espera.  
  
 La tabla incluida a continuación enumera los contadores que contiene el objeto de Wait Statistics.  
  
|Contadores de Wait Statistics de SQL Server|Descripción|  
|-----------------------------------------|-----------------|  
|**Esperas de bloqueo**|Estadísticas para procesos que esperan en un bloqueo.|  
|**Esperas de búfer de registro**|Estadísticas para procesos que esperan que el búfer de registro esté disponible.|  
|**Esperas de escritura en registro**|Estadísticas para procesos que esperan que se escriba el búfer de registro.|  
|**Esperas de cola de concesión de memoria**|Estadísticas para procesos que esperan que una concesión de memoria esté disponible.|  
|**Esperas de E/S de red**|Estadísticas relacionadas con la espera en E/S de red.|  
|**Esperas de bloqueos temporales distintos de páginas**|Estadísticas relacionadas con bloqueos temporales distintos de páginas.|  
|**Esperas de bloqueos temporales de E/S de páginas**|Estadísticas relacionadas con bloqueos temporales de E/S de páginas.|  
|**Esperas de bloqueos temporales de páginas**|Estadísticas relacionadas con bloqueos temporales de páginas, no incluidos los bloqueos temporales de E/S.|  
|**Esperas de objetos de memoria seguros para subprocesos**|Estadísticas para procesos que esperan en asignadores de memoria seguros para subprocesos.|  
|**Esperas de propiedad de transacción**|Estadísticas relacionadas con procesos que sincronizan el acceso a la transacción.|  
|**Espera del objeto de trabajo**|Estadísticas relacionadas con procesos que esperan que el objeto de trabajo esté disponible.|  
|**Esperas de sincronización de área de trabajo**|Estadísticas relacionadas con procesos que sincronizan el acceso al área de trabajo.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Elemento|Descripción|  
|----------|-----------------|  
|**Tiempo promedio de espera (ms)**|Tiempo promedio del tipo de espera seleccionado.|  
|**Tiempo de espera acumulado (ms) por segundo**|Tiempo de espera agregado por segundo para el tipo de espera seleccionado.|  
|**Espera en curso**|Número de procesos actualmente en espera en el tipo siguiente.|  
|**Esperas iniciadas por segundo**|Número de esperas iniciadas por segundo del tipo de espera seleccionado.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
