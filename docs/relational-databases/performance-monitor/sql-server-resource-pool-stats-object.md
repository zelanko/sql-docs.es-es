---
title: 'Objeto SQL Server: Estadísticas de grupo de recursos de servidor | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 86dcb119efd9c6bb179aae9208f8e8209a5f4671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649491"
---
# <a name="sql-server-resource-pool-stats-object"></a>Objeto SQL Server: Estadísticas de grupo de recursos de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto SQLServer:Estadísticas de grupo de recursos de servidor contiene contadores de rendimiento que notifican información sobre las estadísticas del grupo de recursos de servidor del regulador de recursos.  
  
 Cada grupo de recursos de servidor activo crea una instancia del objeto de rendimiento SQLServer:Estadísticas de grupo de recursos de servidor que tiene el mismo nombre que el grupo de recursos de servidor del regulador de recursos. En la tabla siguiente se describen los contadores admitidos en esta instancia.  
  
|Nombre de contador|Descripción|  
|------------------|-----------------|  
|**Cantidad de concesiones de memoria activas (KB)**|Cantidad total actual, en kilobytes (KB), de memoria concedida. Esta información también está disponible en [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md).| 
|**Número de concesiones de memoria activas**|Número total actual de concesiones de memoria. Esta información también está disponible en [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md).|  
|**Promedio de E/S de lectura de disco (ms)**|Tiempo promedio, en milisegundos, de una operación de lectura del disco.|  
|**Base de E/S de lectura de disco (ms) promedio**|Exclusivamente para uso interno.|
|**Promedio de escrituras en disco (ms)**|Tiempo promedio, en milisegundos, de una operación de escritura en el disco.|  
|**Base de E/S de escritura en disco (ms) promedio**|Exclusivamente para uso interno.|
|**Destino de memoria caché (KB)**|Destino del agente de memoria actual, en kilobytes (KB), para la memoria caché.|  
|**Destino de memoria de compilación (KB)**|Destino del agente de memoria actual, en kilobytes (KB), para la compilación de consultas.|  
|**% de efecto de control de CPU**|Efecto del regulador de recursos en el grupo de recursos de servidor. Se calcula como (% de uso de la CPU) / (% de uso de la CPU sin regulador de recursos).|  
|**% de CPU retrasada**|CPU del sistema retrasada para todas las solicitudes de la instancia especificada del objeto de rendimiento como porcentaje del tiempo total activo.|
|**Base de % de CPU retrasada**|Exclusivamente para uso interno.|
|**% efectivo de la CPU**|Uso de CPU del sistema por todas las solicitudes de la instancia especificada del objeto de rendimiento como porcentaje del tiempo total activo.|
|**Base de % efectivo de la CPU**|Exclusivamente para uso interno.|
|**% de uso de CPU**|El uso de ancho banda de CPU por parte de todas las solicitudes en todos los grupos de cargas de trabajo pertenecientes a este grupo. Este número se mide en relación al equipo y se normaliza respecto a todas las CPUs del sistema. Este valor cambiará a medida que la cantidad de CPU disponible para el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] varíe. No se normaliza respecto a lo que el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recibe.|  
|**Base de % de uso de la CPU**|Exclusivamente para uso interno.|
|**% objetivo de uso de CPU**|Valor de destino del porcentaje de uso de CPU para el grupo de recursos de servidor según la configuración del grupo de recursos de servidor y la carga del sistema.|  
|**% de CPU infringida**|Diferencia entre la reserva de CPU y el porcentaje de programación efectiva.|
|**Bytes de lectura de disco/s**|Número de bytes leídos del disco en el último segundo.|  
|**E/S de lectura de disco limitadas/s**|Número de operaciones de lectura limitadas en el último segundo.|  
|**E/S de lectura de disco/s**|Número de operaciones de lectura del disco en el último segundo.| 
|**Bytes de escritura en disco/s**|Número de bytes escritos en el disco en el último segundo.|  
|**E/S de escritura en disco limitadas/s**|Número de operaciones de escritura limitadas en el último segundo.| 
|**E/S de escrituras en disco/s**|Número de operaciones de escritura en el disco en el último segundo.|
|**Memoria máxima (KB)**|Cantidad máxima, en kilobytes (KB), de memoria que el grupo de recursos de servidor puede tener en función de la configuración del grupo de recursos de servidor y el estado del servidor.| 
|**Tiempos de espera agotados de concesiones de memoria/s**|Número de tiempos de espera agotados de concesiones de memoria por segundo.|
|**Concesiones de memoria/s**|Número de concesiones de memoria por segundo que han tenido lugar en este grupo de recursos de servidor.| 
|**Número de concesiones de memoria pendientes**|Número de solicitudes de concesiones de memoria pendientes en las colas. Esta información también está disponible en [sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md).|
|**Destino de memoria de ejecución de consultas (KB)**|Destino del agente de memoria actual, en kilobytes (KB), para la concesión de memoria de la ejecución de consultas. Esta información también está disponible en [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md).|  
|**Memoria de destino (KB)**|Cantidad de destino, en kilobytes (KB), de memoria que el grupo de recursos de servidor trata de obtener en función de la configuración del grupo de recursos de servidor y el estado del servidor.|   
|**Memoria usada (KB)**|Cantidad de memoria utilizada, en kilobytes (KB), para el grupo de recursos de servidor.|  

  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Objeto SQL Server: Estadísticas de grupo de cargas de trabajo](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)   
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)  
  
  
