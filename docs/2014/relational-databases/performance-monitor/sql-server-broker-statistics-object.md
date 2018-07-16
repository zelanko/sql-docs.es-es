---
title: Broker Statistics (objeto de SQL Server) | Microsoft Docs
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
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6ea599a631955067e168cd704fae9e8ae8965c26
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198955"
---
# <a name="sql-server-broker-statistics-object"></a>Broker Statistics (objeto de SQL Server)
  El objeto de rendimiento SQLServer:Broker Statistics contiene contadores de rendimiento que notifican información general de [!INCLUDE[ssSB](../../includes/sssb-md.md)] para una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. En la tabla siguiente se muestran los contadores incluidos en este objeto:  
  
|Contadores de Broker Statistics de SQL Server|Descripción|  
|-------------------------------------------|-----------------|  
|**Total de errores de activación**|Número de veces que un procedimiento almacenado de activación de [!INCLUDE[ssSB](../../includes/sssb-md.md)] terminó con un error.|  
|**Reversiones de transacciones de Broker**|Número de transacciones revertidas que contenían instrucciones DML relacionadas con [!INCLUDE[ssSB](../../includes/sssb-md.md)], como SEND y RECEIVE.|  
|**Total de mensajes dañados**|Número de mensajes dañados que recibió la instancia.|  
|**Mensajes quitados de la cola de transmisión/s**|Número de mensajes que se han quitado de la cola de transmisión de [!INCLUDE[ssSB](../../includes/sssb-md.md)] por segundo.|  
|**Recuento de eventos de temporizador de diálogos**|Número de temporizadores activos en la capa del protocolo de diálogo. Este número corresponde al número de diálogos activos.|  
|**Total de mensajes quitados**|Número de mensajes recibidos por la instancia pero que no se pudieron entregar a una cola.|  
|**Total de mensajes locales puestos en cola**|Número de mensajes que se han colocado en las colas de la instancia, contando solo los que no han llegado a través de la red.|  
|**Mensajes locales puestos en cola/seg.**|Número de mensajes por segundo que se han colocado en las colas de la instancia, contando solo los que no han llegado a través de la red.|  
|**Total de mensajes en cola**|Número total de mensajes que se han colocado en las colas de la instancia.|  
|**Mensajes puestos en cola/seg.**|Número de mensajes por segundo que se han colocado en las colas de la instancia. Esto incluye mensajes de todos los niveles de prioridad.|  
|**Mensajes P1 en cola/seg.**|Número de mensajes con prioridad 1 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P2 en cola/seg.**|Número de mensajes con prioridad 2 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P3 en cola/seg.**|Número de mensajes con prioridad 3 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P4 en cola/seg.**|Número de mensajes con prioridad 4 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P5 en cola/seg.**|Número de mensajes con prioridad 5 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P6 en cola/seg.**|Número de mensajes con prioridad 6 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P7 en cola/seg.**|Número de mensajes con prioridad 7 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P8 en cola/seg.**|Número de mensajes con prioridad 8 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P9 en cola/seg.**|Número de mensajes con prioridad 9 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes P10 en cola/seg.**|Número de mensajes con prioridad 10 por segundo que se han colocado en las colas de la instancia.|  
|**Mensajes de transmisión en cola/seg**|Número de mensajes que se han colocado en la cola de transmisión de [!INCLUDE[ssSB](../../includes/sssb-md.md)] por segundo.|  
|**Total de fragmentos de mensajes de transporte puestos en cola**|Número de fragmentos de mensajes que se han colocado en las colas de la instancia, contando solo los que han llegado a través de la red.|  
|**Fragmentos de mensajes de transporte puestos en cola/seg.**|Número de fragmentos de mensajes por segundo que se han colocado en las colas de la instancia.|  
|**Total de mensajes de transporte puestos en cola**|Número de mensajes que se han colocado en las colas de la instancia, contando solo los que han llegado a través de la red.|  
|**Mensajes de transporte en cola/seg.**|Número de mensajes por segundo que se han colocado en las colas de la instancia, contando solo los que han llegado a través de la red.|  
|**Total de mensajes reenviados**|Número total de mensajes de [!INCLUDE[ssSB](../../includes/sssb-md.md)] reenviados por este equipo.|  
|**Mensajes reenviados/seg.**|Número de mensajes por segundo reenviados por este equipo.|  
|**Total de bytes de mensajes reenviados**|Tamaño total, en bytes, de los mensajes reenviados por este equipo.|  
|**Bytes de mensajes reenviados/seg.**|Tamaño, en bytes, de los mensajes por segundo reenviados por este equipo.|  
|**Total de mensajes reenviados descartados**|Número de mensajes que este equipo recibió para reenviar, pero no se reenviaron correctamente.|  
|**Mensajes reenviados descartados/seg.**|Número de mensajes por segundo que este equipo recibió para reenviar, pero no se reenviaron correctamente.|  
|**Bytes de mensajes reenviados pendientes**|Tamaño total de los mensajes pendientes de reenviar.|  
|**Recuento de mensajes reenviados pendientes**|Número total de mensajes pendientes de reenviar.|  
|**Total de SQL RECEIVE**|Número total de instrucciones RECEIVE [!INCLUDE[tsql](../../includes/tsql-md.md)] procesadas.|  
|**SQL RECEIVE/seg.**|Número de instrucciones RECEIVE [!INCLUDE[tsql](../../includes/tsql-md.md)] procesadas por segundo.|  
|**Total de SQL SEND**|Número total de instrucciones SEND [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecutadas.|  
|**SQL SEND/seg.**|Número de instrucciones SEND [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecutadas por segundo.|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
