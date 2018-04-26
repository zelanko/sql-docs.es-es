---
title: Replicación transaccional bidireccional | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0493e6a1e66000b7f1a6106b9aac6b8a6f750900
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="bidirectional-transactional-replication"></a>replicación transaccional bidireccional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación transaccional bidireccional es una topología de replicación transaccional específica que permite a dos servidores intercambiar cambios mutuamente: cada servidor publica datos y después se suscribe a una publicación con los mismos datos en el otro servidor. El parámetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) se establece en TRUE para garantizar que los cambios se envíen únicamente al suscriptor y no se envíen de vuelta al publicador.  
  
 En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, esta topología también es compatible con la replicación transaccional punto a punto, pero la replicación bidireccional puede proporcionar un mayor rendimiento.  
  
## <a name="see-also"></a>Ver también  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
