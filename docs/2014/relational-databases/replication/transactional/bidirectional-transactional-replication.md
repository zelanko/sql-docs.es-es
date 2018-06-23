---
title: Replicación transaccional bidireccional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 59817a189d1e52f7d4e8532c35fc024aa1745e3f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201351"
---
# <a name="bidirectional-transactional-replication"></a>replicación transaccional bidireccional
  La replicación transaccional bidireccional es una topología de replicación transaccional específica que permite a dos servidores intercambiar cambios mutuamente: cada servidor publica datos y después se suscribe a una publicación con los mismos datos en el otro servidor. El parámetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) se establece en TRUE para garantizar que los cambios se envíen únicamente al suscriptor y no se envíen de vuelta al publicador.  
  
 En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, esta topología también es compatible con la replicación transaccional punto a punto, pero la replicación bidireccional puede proporcionar un mayor rendimiento.  
  
## <a name="see-also"></a>Vea también  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
