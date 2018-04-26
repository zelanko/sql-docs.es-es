---
title: Establecer opciones de resolución de conflictos de actualización en cola (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5f471a69c3c0c7693cd7eac27d04692c65b6111
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>Establecer opciones de resolución de conflictos de actualización en cola (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Establezca las opciones de resolución de conflictos para las publicaciones que admiten suscripciones de actualización en cola en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación - \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>Para establecer las opciones de resolución de conflictos de actualización en cola  
  
1.  En la página **Opciones de suscripción**, del cuadro de diálogo **Propiedades de la publicación - \<Publicación>**, seleccione uno de los siguientes valores para la opción **Directiva de resolución de conflictos**:  
  
    -   **Mantener el cambio del publicador**  
  
    -   **Mantener el cambio del suscriptor**  
  
    -   **Reinicializar la suscripción**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Habilitar suscripciones actualizables para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
