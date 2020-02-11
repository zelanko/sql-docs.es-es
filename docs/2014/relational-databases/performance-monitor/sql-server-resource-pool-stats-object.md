---
title: 'Objeto SQL Server: Estadísticas de grupo de recursos de servidor | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fdf00d1291180197f66cd6cb23cf27f10659c68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183019"
---
# <a name="sql-server-resource-pool-stats-object"></a>Objeto SQL Server: Estadísticas de grupo de recursos de servidor
  El objeto SQLServer:Estadísticas de grupo de recursos de servidor contiene contadores de rendimiento que notifican información sobre las estadísticas del grupo de recursos de servidor del regulador de recursos.  
  
 Cada grupo de recursos de servidor activo crea una instancia del objeto de rendimiento SQLServer:Estadísticas de grupo de recursos de servidor que tiene el mismo nombre que el grupo de recursos de servidor del regulador de recursos. En la tabla siguiente se describen los contadores admitidos en esta instancia.  
  
|Nombre del contador|Descripción|  
|------------------|-----------------|  
|% de uso de CPU|El uso de ancho banda de CPU por parte de todas las solicitudes en todos los grupos de cargas de trabajo pertenecientes a este grupo. Este número se mide en relación al equipo y se normaliza respecto a todas las CPUs del sistema. Este valor cambiará a medida que la cantidad de CPU disponible para el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] varíe. No se normaliza respecto a lo que el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recibe.|  
|% objetivo de uso de CPU|Valor de destino del porcentaje de uso de CPU para el grupo de recursos de servidor según la configuración del grupo de recursos de servidor y la carga del sistema.|  
|% de efecto de control de CPU|Efecto del regulador de recursos en el grupo de recursos de servidor. Se calcula como (% de uso de la CPU) / (% de uso de la CPU sin regulador de recursos).|  
|Destino de memoria de compilación (KB)|Destino del agente de memoria actual, en kilobytes (KB), para la compilación de consultas.|  
|Destino de memoria caché (KB)|Destino del agente de memoria actual, en kilobytes (KB), para la memoria caché.|  
|Destino de memoria de ejecución de consultas (KB)|Destino del agente de memoria actual, en kilobytes (KB), para la concesión de memoria de la ejecución de consultas. Esta información también está disponible en [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql).|  
|Concesiones de memoria/s|Número de concesiones de memoria por segundo que han tenido lugar en este grupo de recursos de servidor.|  
|Número de concesiones de memoria activas|Número total actual de concesiones de memoria. Esta información también está disponible en [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql).|  
|Tiempos de espera agotados de concesiones de memoria/s|Número de tiempos de espera agotados de concesiones de memoria por segundo.|  
|Cantidad de concesiones de memoria activas (KB)|Cantidad total actual, en kilobytes (KB), de memoria concedida. Esta información también está disponible en [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
|Número de concesiones de memoria pendientes|Número de solicitudes de concesiones de memoria pendientes en las colas. Esta información también está disponible en [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
|Memoria máxima (KB)|Cantidad máxima, en kilobytes (KB), de memoria que el grupo de recursos de servidor puede tener en función de la configuración del grupo de recursos de servidor y el estado del servidor.|  
|Memoria usada (KB)|Cantidad de memoria utilizada, en kilobytes (KB), para el grupo de recursos de servidor.|  
|Memoria de destino (KB)|Cantidad de destino, en kilobytes (KB), de memoria que el grupo de recursos de servidor trata de obtener en función de la configuración del grupo de recursos de servidor y el estado del servidor.|  
|E/S de lectura de disco/s|Número de operaciones de lectura del disco en el último segundo.|  
|E/S de lectura de disco limitadas/s|Número de operaciones de lectura limitadas en el último segundo.|  
|Bytes de lectura de disco/s |Número de bytes leídos del disco en el último segundo.|  
|Promedio de E/S de lectura de disco (ms)|Tiempo promedio, en milisegundos, de una operación de lectura del disco.|  
|E/S de escrituras en disco/s|Número de operaciones de escritura en el disco en el último segundo.|  
|E/S de escritura en disco limitadas/s|Número de operaciones de escritura limitadas en el último segundo.|  
|  Bytes de escritura en disco/s|Número de bytes escritos en el disco en el último segundo.|  
|Promedio de escrituras en disco (ms)|Tiempo promedio, en milisegundos, de una operación de escritura en el disco.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [Objeto SQL Server: Estadísticas de grupo de cargas de trabajo](sql-server-workload-group-stats-object.md)   
 [Regulador de recursos](../resource-governor/resource-governor.md)  
  
  
