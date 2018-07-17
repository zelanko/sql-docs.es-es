---
title: Tipos de publicaciones para la replicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9bcd05056b4c9c0db1375813ee81ed0c5c03f25c
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37360057"
---
# <a name="publication-types-for-transactional-replication"></a>Tipos de publicaciones para la replicación transaccional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación transaccional ofrece tres tipos de publicaciones:  
  
|Tipo de publicación|Descripción|  
|----------------------|-----------------|  
|Publicación transaccional estándar|Apropiada para topologías en las que todos los datos del suscriptor son de solo lectura (la replicación transaccional no exige que esto se cumpla en el suscriptor).<br /><br /> Las publicaciones transaccionales estándar se crean de manera predeterminada cuando se usa Transact-SQL o Replication Management Objects (RMO). Cuando se utiliza el Asistente para nueva publicación, se crean seleccionando **Publicación transaccional** en la página **Tipo de publicación** .<br /><br /> Para obtener más información sobre la creación de publicaciones, vea [Publish Data and Database Objects (Publicar datos y objetos de base de datos)](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).|  
|Publicación transaccional en una topología punto a punto|Las características de este tipo de publicación son:<br /><br /> -Cada ubicación tiene datos idénticos y funciona como publicador y como suscriptor.<br /><br /> -Una misma fila solo se puede cambiar en una ubicación a la vez.<br /><br /> -Esta topología es más apropiada para los entornos de servidor que necesitan una gran disponibilidad y escalabilidad de lectura.<br /><br /> <br /><br /> Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
## <a name="see-also"></a>Ver también  
 [Transactional Replication](../../../relational-databases/replication/transactional/transactional-replication.md) (Replicación transaccional)  
  
  
