---
title: Tipos de replicación | Microsoft Docs
description: Obtenga información sobre los diferentes tipos de replicación que SQL Server proporciona para su uso en aplicaciones distribuidas.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c7483eca0f573e901908d3fb5b2eb72f8317ef7c
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111163"
---
# <a name="types-of-replication"></a>Tipos de replicación
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona los siguientes tipos de replicación para usarlos en las aplicaciones distribuidas:  

| **Tipo** | **Descripción** |
|:-------- | :-------------- |
| [Replicación transaccional](transactional/transactional-replication.md)| Los cambios en el publicador se entregan al suscriptor cuando se producen (casi en tiempo real). Los cambios de datos se aplican al suscriptor en el mismo orden y dentro de los mismos límites de transacción que se establecieron en el publicador. | 
| [Replicación de mezcla](merge/merge-replication.md) | Los datos se pueden cambiar en el publicador y en el suscriptor; asimismo, se realiza un seguimiento con los desencadenadores. El suscriptor se sincroniza con el publicador cuando están conectados a la red e intercambian todas las filas que han cambiado entre el publicador y el suscriptor desde la última vez que se produjo la sincronización. | 
| [Replicación de instantáneas](snapshot-replication.md) | Aplica una instantánea del publicador al suscriptor, que distribuye los datos exactamente como aparecen en un momento específico y no supervisa las actualizaciones de los datos. Cuando se produce la sincronización, se genera la instantánea completa y se envía a los suscriptores.| 
| [Punto a punto](transactional/peer-to-peer-transactional-replication.md) | Generada en la base de replicación transaccional, la replicación punto a punto propaga transaccionalmente los cambios coherentes en tiempo casi real entre varias instancias del servidor. | 
| [Bidireccional](transactional/bidirectional-transactional-replication.md)| La replicación transaccional bidireccional es una topología de replicación transaccional específica que permite a dos servidores intercambiar cambios mutuamente: cada servidor publica datos y después se suscribe a una publicación con los mismos datos en el otro servidor. | 
| [Suscripciones actualizables](transactional/updatable-subscriptions-for-transactional-replication.md) | Creado sobre la base de la replicación transaccional, cuando los datos se actualizan en el suscriptor de una suscripción actualizable, primero se propaga al publicador y luego se propaga a otros suscriptores. | 
  
 
El tipo de replicación que se elige para una aplicación depende de muchos factores, como el entorno físico de la replicación, el tipo y la cantidad de datos que se desean replicar y si los datos se actualizan en el suscriptor. El entorno físico incluye el número y la ubicación de los equipos que participan en la replicación, y si estos equipos son clientes (estaciones de trabajo, equipos portátiles o dispositivos de mano) o servidores.  
  
Por lo general, cada tipo de replicación comienza con una sincronización inicial de los objetos publicados entre el publicador y los suscriptores. Esta sincronización inicial puede llevarse a cabo mediante la replicación con una *instantánea*, que es una copia de todos los objetos y datos especificados por una publicación. Una vez creada la instantánea, se envía a los suscriptores. Para algunas aplicaciones, la replicación de instantáneas es lo único que se necesita. Para otros tipos de aplicaciones, es importante que los cambios de datos posteriores fluyan al suscriptor de forma incremental a lo largo del tiempo. Algunas aplicaciones también requieren que los cambios vuelvan del suscriptor al publicador. La replicación transaccional y la replicación de mezcla proporcionan opciones para estos tipos de aplicaciones.  
  
 
## <a name="see-also"></a>Consulte también  
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)
  
  
