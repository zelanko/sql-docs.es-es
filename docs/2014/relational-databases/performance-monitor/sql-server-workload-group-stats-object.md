---
title: 'Objeto SQL Server: Estadísticas de grupo de cargas de trabajo | Microsoft Docs'
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
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 47f6ec268f40ab409a2c4438e6faa029ae10fe2b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270781"
---
# <a name="sql-server-workload-group-stats-object"></a>Objeto SQL Server: Estadísticas de grupo de cargas de trabajo
  El objeto SQLServer:Estadísticas de grupo de cargas de trabajo contiene contadores de rendimiento que notifican información sobre las estadísticas de grupo de cargas de trabajo del regulador de recursos.  
  
 Cada grupo de cargas de trabajo activo crea una instancia del objeto de rendimiento SQLServer:Estadísticas de grupo de cargas de trabajo que tiene el mismo nombre de instancia que el grupo de cargas de trabajo del regulador de recursos. En la tabla siguiente se describen los contadores admitidos en esta instancia.  
  
|Nombre de contador|Descripción|  
|------------------|-----------------|  
|Solicitudes en cola|Número actual de solicitudes en cola que esperan ser recogidas. Este número puede ser distinto de cero si se produce una limitación una vez alcanzado el límite GROUP_MAX_REQUESTS.|  
|Solicitudes activas|El número de solicitudes que están ejecutándose actualmente en este grupo de cargas de trabajo. Este número debería ser equivalente al recuento de filas procedentes de sys.dm_exec_requests filtrado por identificador de grupo.|  
|Solicitudes completadas/s|Número de solicitudes que se han completado en este grupo de cargas de trabajo. Este número es acumulativo.|  
|% de uso de CPU|Uso del ancho banda de CPU por parte de todas las solicitudes en este grupo de cargas de trabajo medidas en relación al equipo y normalizadas con respecto a todas las CPU del sistema. Este valor cambiará a medida que la cantidad de CPU disponible para el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] varíe. No se normaliza respecto a lo que el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recibe.|  
|Tiempo máximo de CPU por solicitud (ms)|Tiempo de CPU máximo, en milisegundos, utilizado por una solicitud actualmente en ejecución en el grupo de cargas de trabajo.|  
|Solicitudes bloqueadas|Número actual de solicitudes bloqueadas en el grupo de cargas de trabajo. Este número se puede utilizar para determinar las características de la carga de trabajo.|  
|Concesiones con memoria reducida/s|Número de consultas que obtienen una cantidad de concesiones de memoria por debajo de la cantidad ideal por segundo.|  
|Concesión máxima de memoria de solicitud (KB)|Valor máximo de concesión de memoria, en kilobytes (KB), para una consulta.|  
|Optimizaciones de consultas/s|Número de optimizaciones de consultas por segundo que han tenido lugar en este grupo de cargas de trabajo. Este número se puede utilizar para determinar las características de la carga de trabajo.|  
|Planes poco óptimos/s|Número de planes poco óptimos que se generan en este grupo de cargas de trabajo por segundo.|  
|Subprocesos paralelos activos|Recuento actual de uso de subprocesos paralelos.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [Objeto SQL Server: Estadísticas de grupo de recursos de servidor](sql-server-resource-pool-stats-object.md)   
 [regulador de recursos](../resource-governor/resource-governor.md)  
  
  
