---
title: Objeto de transporte SQL Server, Broker y DBM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0347c7f7e19ae5500f8c5be100ef2d0dc663784
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250730"
---
# <a name="sql-server-broker-and-dbm-transport-object"></a>Broker y DBM Transport (objeto de SQL Server)
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
|**Promedio de tamaño de envíos de fragmentos de mensajes**|Este contador informa del tamaño medio de los fragmentos de mensajes enviados a través de la red.|  
|**Envíos de fragmentos de mensajes/seg.**|Este contador informa del número de fragmentos de mensajes con todas las prioridades enviados a través de la red por segundo.|  
|**Recepciones de fragmentos de mensajes/seg.**|Este contador informa del número de fragmentos de mensajes recibidos a través de la red por segundo.|  
|**Promedio de tamaño de recepciones de fragmentos de mensajes**|Este contador informa del tamaño medio de los fragmentos de mensajes recibidos a través de la red.|  
|**Recuento de conexiones abiertas**|Este contador informa del número de conexiones de red que Service Broker tiene abiertas.|  
|**Bytes pendientes para E/S de recepción**|Este contador informa del número de bytes incluidos en fragmentos de mensajes que se han recibido a través de la red, pero que todavía no se han colocado en una cola ni se han descartado.|  
|**Bytes pendientes para E/S de envío**|Este contador informa del número total de bytes de fragmentos de mensajes que están listos para ser enviados a través de la red.|  
|**Fragmentos de mensajes pendientes para E/S de recepción**|Este contador informa del número de fragmentos de mensajes que se han recibido a través de la red, pero que todavía no se han colocado en una cola ni se han descartado.|  
|**Fragmentos de mensajes pendientes para E/S de envío**|Este contador informa del número total de fragmentos de mensajes que están listos para ser enviados a través de la red.|  
|**Total de bytes de E/S de recepción**|Este contador informa del número total de bytes recibidos a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|  
|**Bytes de E/S de recepción/seg.**|Este contador informa del número de bytes por segundo recibidos a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|  
|**Promedio de longitud de E/S de recepción**|Este contador informa del promedio de bytes para una operación de recepción de transporte.|  
|**E/S de recepción/seg.**|Este contador informa del número de operaciones de E/S de recepción de transporte por segundo que la capa de trasporte de Service Broker / DBM ha finalizado. Tenga en cuenta que una operación de recepción de transporte puede incluir varios fragmentos de mensajes.|  
|**Total de bytes de E/S de envío**|Este contador informa del número total de bytes enviados a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|  
|**Bytes de E/S de envío/seg.**|Este contador informa del número de bytes por segundo enviados a través de la red por extremos de Service Broker y extremos de creación de reflejo de base de datos.|  
|**Promedio de longitud de E/S de envío**|Este contador informa del tamaño medio de bytes de cada operación de envío de transporte. Tenga en cuenta que una operación de envío de transporte puede incluir varios fragmentos de mensajes.|  
|**E/S de envío/seg.**|Este contador informa del número de operaciones de E/S de envío de transporte por segundo que han finalizado. Tenga en cuenta que una operación de envío de transporte puede incluir varios fragmentos de mensajes.|  
  
## <a name="see-also"></a>Consulte también  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
