---
title: Replicación transaccional bidireccional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2cf5fbf215338b273be0924e6930906c8698aff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188595"
---
# <a name="bidirectional-transactional-replication"></a>replicación transaccional bidireccional
  La replicación transaccional bidireccional es una topología de replicación transaccional específica que permite a dos servidores intercambiar cambios mutuamente: cada servidor publica datos y después se suscribe a una publicación con los mismos datos en el otro servidor. El **@loopback_detection** parámetro de [sp_addsubscription &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) se establece en true para garantizar que los cambios se envíen únicamente al suscriptor y no tengan como resultado que el cambio se envíe de vuelta al publicador.  
  
 En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores, esta topología también es compatible con la replicación transaccional punto a punto, pero la replicación bidireccional puede proporcionar un mayor rendimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
