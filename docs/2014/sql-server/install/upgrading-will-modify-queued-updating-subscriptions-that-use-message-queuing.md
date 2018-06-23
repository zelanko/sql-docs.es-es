---
title: Actualización, se modificarán las suscripciones de actualización en cola que usa Message Queue Server | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: efb1b244385061bee985ec04b5f90d3fb349aef3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105749"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>Con la actualización, se modificarán las suscripciones de actualización en cola que utilicen Message Queue Server
  El Asesor de actualizaciones ha detectado que podría tener una o más suscripciones de actualización en cola que utilizan [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queue Server (también conocido como MSMQ). La replicación ya no admite Message Queue Server, por lo que las suscripciones se modificarán de forma que usen una cola de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Solo un valor de **sql** está permitido. Las publicaciones existentes que usan Message Queue Server se modifican durante la actualización para que usen una cola de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tiene aplicaciones que dependen de las actualizaciones en cola que utilizan Message Queue Server, estas aplicaciones deberán reescribirse para su inclusión en una cola de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre las suscripciones de actualización en cola, vea "Suscripciones actualizable para la replicación transaccional" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La actualización quitará las colas de suscripción de Message Queue Server existentes si el servicio Message Queue Server se ejecuta mientras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se actualiza.  
  
 Si el servicio Message Queue Server no está en ejecución, elimine manualmente las colas una vez completada la actualización. Para obtener más información acerca de cómo quitar colas, vea la documentación de Windows.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de replicación](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  