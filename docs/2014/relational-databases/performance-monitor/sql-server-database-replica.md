---
title: SQL Server, réplica de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c8830ae30ad3514e107b718f9a02fef873e20295
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038781"
---
# <a name="sql-server-database-replica"></a>SQL Server, réplica de base de datos
  El objeto de rendimiento **SQLServer:Database Replica** contiene contadores de rendimiento que ofrecen información acerca de las bases de datos secundarias de un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este objeto solamente es válido en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda una réplica secundaria.  
  
|Nombre del contador|Descripción|Vista en...|  
|------------------|-----------------|--------------|  
|**Bytes de archivo recibidos/s**|Cantidad de datos de FILESTREAM recibidos por la réplica secundaria para la base de datos secundaria en el último segundo.|Réplica secundaria|  
|**Bytes de registro recibidos/s**|Cantidad de entradas de registro recibidas por la réplica secundaria para la base de datos en el último segundo.|Réplica secundaria|  
|**Registro restante para deshacer**|Cantidad del registro en kilobytes que queda para completar la fase de deshacer.|Réplica secundaria|  
|**Cola de envío de registro**|Cantidad de entradas de registro de los archivos de registro de la base de datos principal, en kilobytes, que no se han enviado todavía a la réplica secundaria. Este valor se envía a la réplica secundaria desde la réplica principal. El tamaño de la cola no incluye los archivos FILESTREAM que se envían a un secundario.|Réplica secundaria|  
|**Transacciones de escritura reflejadas/s**|Número de transacciones que se escribieron en la base de datos principal y, después, esperaron a confirmarse hasta que el registro se enviara a la base de datos secundaria, en el último segundo.|Réplica principal|  
|**Cola de recuperación**|Cantidad de entradas de registro en los archivos de registro de la réplica secundaria que no se han rehecho todavía.|Réplica secundaria|  
|**Rehacer bloqueadas por segundo**|Número de veces que el subproceso de puesta al día está bloqueado en los bloqueos mantenidos por los lectores de la base de datos.|Réplica secundaria|  
|**Rehacer bytes restantes**|Cantidad restante de registro en kilobytes que se debe rehacer para finalizar la fase de reversión.|Réplica secundaria|  
|**Bytes puestos al día/s**|Cantidad de entradas de registro rehechas en la base de datos secundaria en el último segundo.|Réplica secundaria|  
|**Registro total que requiere la operación de deshacer**|Kilobytes totales del registro que se deben deshacer.|Réplica secundaria|  
|**Retraso de transacción**|Retraso en la espera de reconocimiento de confirmación no terminada, en milisegundos.|Réplica principal|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;el monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, réplica de disponibilidad](sql-server-availability-replica.md)   
 [SQL Server, objeto Databases](sql-server-databases-object.md)   
 [Grupos de disponibilidad AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
