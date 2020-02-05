---
title: SQL Server, réplica de disponibilidad | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6dfb020026ba431669a0e551d5cb3aa85fbea637
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68095321"
---
# <a name="sql-server-availability-replica"></a>SQL Server, réplica de disponibilidad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto de rendimiento **SQLServer:Availability Replica** contiene contadores de rendimiento que proporcionan información acerca de las réplicas de disponibilidad en los grupos de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Todos los contadores de rendimiento de las réplicas de disponibilidad se aplican tanto a las réplicas principales como a las réplicas secundarias, y los contadores de envío/recepción reflejan la réplica local. En general, la réplica principal envía la mayor parte de los datos y las réplicas secundarias reciben los datos. Sin embargo, las réplicas secundarias envían mensajes de confirmación de reconocimiento y otro tráfico de fondo a las réplicas principales. Observe que en una réplica de disponibilidad dada, algunos contadores mostrarán el valor cero, dependiendo del rol actual (principal o secundario) de la réplica local.  
  
|Nombre del contador|Descripción|  
|------------------|-----------------|  
|**Bytes recibidos de la réplica/s**|Número de bytes recibidos de la réplica de disponibilidad por segundo. Las actualizaciones de estado y ping generará tráfico de red incluso en las bases de datos sin actualizaciones de usuario.|  
|**Bytes enviados a la réplica/s**|Número de bytes enviados a la réplica de disponibilidad remota por segundo. En la réplica principal, se trata del número de bytes enviados a la réplica secundaria. En la réplica secundaria, se trata del número de bytes enviados a la réplica principal.|  
|**Bytes enviados al transporte/s**|Número real de bytes enviados por segundo a través de la red a la réplica de disponibilidad remota. En la réplica principal, se trata del número de bytes enviados a la réplica secundaria. En la réplica secundaria, se trata del número de bytes enviados a la réplica principal.|  
|**Tiempo de control de flujo (ms/s)**|Tiempo en milisegundos que los mensajes de flujo de registro esperaron el control de flujo de envío en el último segundo.|  
|**Control de flujo/s**|Número de veces que se inició el control de flujo en el último segundo. **Tiempo de control de flujo (ms/s)** dividido entre **Control de flujo por segundo** es el tiempo medio por espera.|  
|**Recepciones de la réplica/s**|Número de mensajes de AlwaysOn recibidos de la réplica por segundo.|  
|**Mensajes reenviados/s**|Número de mensajes de AlwaysOn reenviados en el último segundo.|  
|**Envíos a la réplica/s**|Número de mensajes de AlwaysOn enviados a esta réplica de disponibilidad por segundo.|  
|**Envíos a transporte/s**|Número real de mensajes de AlwaysOn enviados por segundo a través de la red en la réplica de disponibilidad remota. En la réplica principal, se trata del número de mensajes enviados a la réplica secundaria. En la réplica secundaria, se trata del número de mensajes enviados a la réplica principal.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, réplica de base de datos](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Grupos de disponibilidad Always On (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
