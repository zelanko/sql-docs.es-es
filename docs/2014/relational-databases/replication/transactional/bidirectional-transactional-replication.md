---
title: Replicación transaccional bidireccional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86cdfaa9e7bf61b76acb953e3f2c6a1feb7d1dad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126833"
---
# <a name="bidirectional-transactional-replication"></a>replicación transaccional bidireccional
  La replicación transaccional bidireccional es una topología de replicación transaccional específica que permite a dos servidores intercambiar cambios mutuamente: cada servidor publica datos y después se suscribe a una publicación con los mismos datos en el otro servidor. El parámetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) se establece en TRUE para garantizar que los cambios se envíen únicamente al suscriptor y no se envíen de vuelta al publicador.  
  
 En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, esta topología también es compatible con la replicación transaccional punto a punto, pero la replicación bidireccional puede proporcionar un mayor rendimiento.  
  
## <a name="see-also"></a>Vea también  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
