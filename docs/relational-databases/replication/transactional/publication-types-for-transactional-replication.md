---
title: "Tipos de publicaciones para la replicación transaccional | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3bfa3cae7f71edbae561b3d2ab1eb7784a433df6
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="publication-types-for-transactional-replication"></a>Tipos de publicaciones para la replicación transaccional
  La replicación transaccional ofrece tres tipos de publicaciones:  
  
|Tipo de publicación|Descripción|  
|----------------------|-----------------|  
|Publicación transaccional estándar|Apropiada para topologías en las que todos los datos del suscriptor son de solo lectura (la replicación transaccional no exige que esto se cumpla en el suscriptor).<br /><br /> Las publicaciones transaccionales estándar se crean de manera predeterminada cuando se usa Transact-SQL o Replication Management Objects (RMO). Cuando se utiliza el Asistente para nueva publicación, se crean seleccionando **Publicación transaccional** en la página **Tipo de publicación** .<br /><br /> Para obtener más información sobre la creación de publicaciones, vea [Publish Data and Database Objects (Publicar datos y objetos de base de datos)](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).|  
|Publicación transaccional en una topología punto a punto|Las características de este tipo de publicación son:<br /><br /> -Cada ubicación tiene datos idénticos y funciona como publicador y como suscriptor.<br /><br /> -Una misma fila solo se puede cambiar en una ubicación a la vez.<br /><br /> -Esta topología es más apropiada para los entornos de servidor que necesitan una gran disponibilidad y escalabilidad de lectura.<br /><br /> <br /><br /> Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
## <a name="see-also"></a>Vea también  
 [Transactional Replication](../../../relational-databases/replication/transactional/transactional-replication.md) (Replicación transaccional)  
  
  
