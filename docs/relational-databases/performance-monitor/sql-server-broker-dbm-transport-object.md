---
title: Broker - DBM Transport (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2b4e92440afdc0bb57f696f2d0c2e601025442e8
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158993"
---
# <a name="sql-server-broker---dbm-transport-object"></a>Broker - DBM Transport (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto de rendimiento **Broker / DBM Transport** contiene contadores de rendimiento que proporcionan información de red sobre Service Broker y sobre la creación de reflejo de la base de datos. En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
|Contador de Broker / DBM Transport de SQL Server|Descripción|  
|------------------------------------------------|-----------------|  
|**Bytes actuales para E/S de recepción**|Este contador informa del número de bytes que deben leer las operaciones de recepción de transporte que están en ejecución.|  
|**Bytes actuales para E/S de envío**|Este contador informa del número de bytes en fragmentos de mensaje que están en proceso de ser enviados a través de la red.|  
|**Fragmentos de mensajes actuales para E/S de envío**|Este contador informa del número total de fragmentos de mensajes que están en proceso de ser enviados a través de la red.|  
|**Envíos de fragmentos de mensajes P1/seg.**|Este contador informa del número de fragmentos de mensajes con prioridad 1 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes P2/seg.**|Este contador informa del número de fragmentos de mensajes con prioridad 2 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 3/s**|Este contador informa del número de fragmentos de mensajes con prioridad 3 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 4/s**|Este contador informa del número de fragmentos de mensajes con prioridad 4 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 5/s**|Este contador informa del número de fragmentos de mensajes con prioridad 5 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 6/s**|Este contador informa del número de fragmentos de mensajes con prioridad 6 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 7/s**|Este contador informa del número de fragmentos de mensajes con prioridad 7 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 8/s**|Este contador informa del número de fragmentos de mensajes con prioridad 8 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 9/s**|Este contador informa del número de fragmentos de mensajes con prioridad 9 enviados a través de la red por segundo.|  
|**Envíos de fragmentos de mensajes de prioridad 10/s**|Este contador informa del número de fragmentos de mensajes con prioridad 10 enviados a través de la red por segundo.|  
|**Recepciones de fragmentos de mensajes/s**|Este contador informa del número de fragmentos de mensajes recibidos a través de la red por segundo.|   
|**Envíos de fragmentos de mensajes/seg.**|Este contador informa del número de fragmentos de mensajes con todas las prioridades enviados a través de la red por segundo.|  
|**Promedio de tamaño de recepciones de fragmentos de mensajes**|Este contador informa del tamaño medio de los fragmentos de mensajes recibidos a través de la red.|  
|**Base promedio de tamaño de fragmentos de mensaje recibidos**|Exclusivamente para uso interno.| 
|**Promedio de tamaño de fragmentos de mensaje enviados**|Este contador informa del tamaño medio de los fragmentos de mensajes enviados a través de la red.|  
|**Base promedio de tamaño de fragmentos de mensaje enviados**|Exclusivamente para uso interno.|
|**Recuento de conexiones abiertas**|Este contador informa del número de conexiones de red que Service Broker tiene abiertas.|  
|**Bytes pendientes para E/S de recepción**|Este contador informa del número de bytes incluidos en fragmentos de mensajes que se han recibido a través de la red, pero que todavía no se han colocado en una cola ni se han descartado.|  
|**Bytes pendientes para E/S de envío**|Este contador informa del número total de bytes de fragmentos de mensajes que están listos para ser enviados a través de la red.|  
|**Fragmentos de mensajes pendientes para E/S de recepción**|Este contador informa del número de fragmentos de mensajes que se han recibido a través de la red, pero que todavía no se han colocado en una cola ni se han descartado.|  
|**Fragmentos de mensajes pendientes para E/S de envío**|Este contador informa del número total de fragmentos de mensajes que están listos para ser enviados a través de la red.|  
|**Bytes de E/S de recepción/seg.**|Este contador informa del número de bytes por segundo recibidos a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|  
|**Total de bytes de E/S de recepción**|Este contador informa del número total de bytes recibidos a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|  
|**Promedio de longitud de E/S de recepción**|Este contador informa del promedio de bytes para una operación de recepción de transporte.|  
|**Base promedio de longitud de E/de recepción**|Exclusivamente para uso interno.|
|**E/S de recepción/s**|Este contador informa del número de operaciones de E/S de recepción de transporte por segundo que la capa de trasporte de Service Broker / DBM ha finalizado. Tenga en cuenta que una operación de recepción de transporte puede incluir varios fragmentos de mensajes.|  
|**Bytes de copias de búfer de E/S de recepción/s**|Velocidad a la que las operaciones de E/S de recepción de transporte han tenido que mover fragmentos de búfer en la memoria.|
|**Recuento de copias de búfer de E/S de recepción**|Número de veces que las operaciones de E/S de recepción de transporte han tenido que mover fragmentos de búfer en la memoria.| 
|**Bytes de E/S de envío/seg.**|Este contador informa del número de bytes por segundo enviados a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|   
|**Total de bytes de E/S de envío**|Este contador informa del número total de bytes enviados a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.| 
|**Promedio de longitud de E/S de envío**|Este contador informa del tamaño medio de bytes de cada operación de envío de transporte. Tenga en cuenta que una operación de envío de transporte puede incluir varios fragmentos de mensajes.|  
|**Base de longitud promedio de E/S de envío**|Exclusivamente para uso interno.|
|**E/S de envío/seg.**|Este contador informa del número de operaciones de E/S de envío de transporte por segundo que han finalizado. Tenga en cuenta que una operación de envío de transporte puede incluir varios fragmentos de mensajes.|  
  
## <a name="see-also"></a>Ver también  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
