---
title: Tipos de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db941e69711c51a6799c1b94723ce90c64c96e6a
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350957"
---
# <a name="types-of-replication"></a>Tipos de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona los siguientes tipos de replicación para usarlos en las aplicaciones distribuidas:  
  
-   Replicación transaccional. Para obtener más información, consulte [Replicación transaccional](../../relational-databases/replication/transactional/transactional-replication.md).  
  
-   Replicación de mezcla. Para obtener más información, consulte [Replicación de mezcla](../../relational-databases/replication/merge/merge-replication.md).  
  
-   Replicación de instantáneas. Para obtener más información, consulte [Replicación de instantáneas](../../relational-databases/replication/snapshot-replication.md).  
  
 El tipo de replicación que se elige para una aplicación depende de muchos factores, como el entorno físico de la replicación, el tipo y la cantidad de datos que se desean replicar y si los datos se actualizan en el suscriptor. El entorno físico incluye el número y la ubicación de los equipos que participan en la replicación, y si estos equipos son clientes (estaciones de trabajo, equipos portátiles o dispositivos de mano) o servidores.  
  
 Por lo general, cada tipo de replicación comienza con una sincronización inicial de los objetos publicados entre el publicador y los suscriptores. Esta sincronización inicial puede llevarse a cabo mediante la replicación con una *instantánea*, que es una copia de todos los objetos y datos especificados por una publicación. Una vez creada la instantánea, se envía a los suscriptores. Para algunas aplicaciones, la replicación de instantáneas es lo único que se necesita. Para otros tipos de aplicaciones, es importante que los cambios de datos posteriores fluyan al suscriptor de forma incremental a lo largo del tiempo. Algunas aplicaciones también requieren que los cambios vuelvan del suscriptor al publicador. La replicación transaccional y la replicación de mezcla proporcionan opciones para estos tipos de aplicaciones.  
  
 En la replicación de instantáneas, no se realiza un seguimiento de los cambios de datos; cada vez que se aplica una instantánea, ésta sobrescribe completamente los datos existentes. La replicación transaccional realiza un seguimiento de los cambios a través del registro de transacciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la replicación de mezcla realiza un seguimiento de los cambios a través de desencadenadores y tablas de metadatos.  
  
## <a name="see-also"></a>Ver también  
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
