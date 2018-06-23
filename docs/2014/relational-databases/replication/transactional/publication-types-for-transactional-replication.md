---
title: Tipos de publicaciones para la replicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 11e9e6ffafe62c66684470b4b04e2e0b67cc868b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105339"
---
# <a name="publication-types-for-transactional-replication"></a>Tipos de publicaciones para la replicación transaccional
  La replicación transaccional ofrece tres tipos de publicaciones:  
  
|Tipo de publicación|Descripción|  
|----------------------|-----------------|  
|Publicación transaccional estándar|Apropiada para topologías en las que todos los datos del suscriptor son de solo lectura (la replicación transaccional no exige que esto se cumpla en el suscriptor).<br /><br /> Las publicaciones transaccionales estándar se crean de manera predeterminada cuando se usa Transact-SQL o Replication Management Objects (RMO). Cuando se utiliza el Asistente para nueva publicación, se crean seleccionando **Publicación transaccional** en la página **Tipo de publicación** .<br /><br /> Para obtener más información sobre la creación de publicaciones, vea [Publish Data and Database Objects (Publicar datos y objetos de base de datos)](../publish/publish-data-and-database-objects.md).|  
|Publicación transaccional en una topología punto a punto|Las características de este tipo de publicación son:<br /><br /> Cada ubicación tiene datos idénticos y funciona como publicador y como suscriptor.<br /><br /> Una misma fila solo se puede cambiar en una ubicación a la vez.<br /><br /> Esta topología es más apropiada para los entornos de servidor que necesitan una gran disponibilidad y escalabilidad de lectura.<br /><br /> <br /><br /> Para obtener más información, consulte [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md).|  
  
## <a name="see-also"></a>Vea también  
 [Transactional Replication](transactional-replication.md) (Replicación transaccional)  
  
  