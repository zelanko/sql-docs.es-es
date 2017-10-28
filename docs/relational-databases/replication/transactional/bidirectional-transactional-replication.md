---
title: "Replicación transaccional bidireccional | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5357fa35dcc99b260049788238a446dbaac38808
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="bidirectional-transactional-replication"></a>replicación transaccional bidireccional
  La replicación transaccional bidireccional es una topología de replicación transaccional específica que permite a dos servidores intercambiar cambios mutuamente: cada servidor publica datos y después se suscribe a una publicación con los mismos datos en el otro servidor. El parámetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) se establece en TRUE para garantizar que los cambios se envíen únicamente al suscriptor y no se envíen de vuelta al publicador.  
  
 En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, esta topología también es compatible con la replicación transaccional punto a punto, pero la replicación bidireccional puede proporcionar un mayor rendimiento.  
  
## <a name="see-also"></a>Vea también  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  

