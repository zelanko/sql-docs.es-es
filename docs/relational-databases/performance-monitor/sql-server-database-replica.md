---
title: SQL Server, réplica de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 89d2da02b841edd85d58798ca4c7c1745332d536
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68093638"
---
# <a name="sql-server-database-replica"></a>SQL Server, réplica de base de datos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto de rendimiento **SQLServer:Database Replica** contiene contadores de rendimiento que ofrecen información sobre las bases de datos secundarias de un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este objeto solamente es válido en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda una réplica secundaria.  
  
|Nombre del contador|Descripción|Vista en...|  
|------------------|-----------------|--------------|  
|**Bytes de archivo recibidos/s**|Cantidad de datos de FILESTREAM recibidos por la réplica secundaria para la base de datos secundaria en el último segundo.|Réplica secundaria|  
|**Cola de aplicación de registro pendiente**|Número de bloques de registros en espera de aplicarse a la réplica de base de datos.|Réplica secundaria|
|**Cola de aplicación de registro lista**|Número de bloques de registros que están esperando y listos para aplicarse a la réplica de base de datos.|Réplica secundaria|
|**Bytes de registro recibidos/s**|Cantidad de entradas de registro recibidas por la réplica secundaria para la base de datos en el último segundo.|Réplica secundaria|  
|**Registro restante para deshacer**|Cantidad del registro en kilobytes que queda para completar la fase de deshacer.|Réplica secundaria|  
|**Cola de envío de registro**|Cantidad de entradas de registro de los archivos de registro de la base de datos principal, en kilobytes, que no se han enviado todavía a la réplica secundaria. Este valor se envía a la réplica secundaria desde la réplica principal. El tamaño de la cola no incluye los archivos FILESTREAM que se envían a una réplica secundaria.|Réplica secundaria|  
|**Transacciones de escritura reflejadas/s**|Número de transacciones que se escribieron en la base de datos principal y, después, esperaron a confirmarse hasta que el registro se enviara a la base de datos secundaria, en el último segundo.|Réplica principal|  
|**Cola de recuperación**|Cantidad de entradas de registro en los archivos de registro de la réplica secundaria que no se han rehecho todavía.|Réplica secundaria|  
|**Rehacer bloqueadas por segundo**|Número de veces que el subproceso de puesta al día se ha bloqueado en los bloqueos mantenidos por los lectores de la base de datos.|Réplica secundaria|  
|**Rehacer bytes restantes**|Cantidad restante de registro en kilobytes que se debe rehacer para finalizar la fase de reversión.|Réplica secundaria|  
|**Bytes puestos al día/s**|Cantidad de entradas de registro rehechas en la base de datos secundaria en el último segundo.|Réplica secundaria|  
|**Registro total que requiere la operación de deshacer**|Kilobytes totales del registro que se deben deshacer.|Réplica secundaria|  
|**Retraso de transacción**|Retraso en la espera de reconocimiento de confirmación no terminada de todas las transacciones actuales, en milisegundos. Divida entre las *transacciones de escritura reflejadas por segundo* para obtener el *promedio de retraso de transacción*. Para obtener más información, vea [SQL Server 2012 AlwaysOn – Part 12 – Performance Aspects and Performance Monitoring II](https://blogs.msdn.microsoft.com/saponsqlserver/2013/04/24/sql-server-2012-alwayson-part-12-performance-aspects-and-performance-monitoring-ii/) (SQL Server 2012 AlwaysOn – Parte 12: Cuestiones de rendimiento y supervisión del rendimiento II).|Réplica principal|  
  
## <a name="see-also"></a>Consulte también
  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, réplica de disponibilidad](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [Databases (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  