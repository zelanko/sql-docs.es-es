---
title: Establecer opciones de resolución de conflictos de actualización en cola (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf77195076c4467babaa85c19202449b567367ef
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37262431"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>Establecer opciones de resolución de conflictos de actualización en cola (SQL Server Management Studio)
  Establezca las opciones de resolución de conflictos para las publicaciones que admiten suscripciones de actualización en cola en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación - \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>Para establecer las opciones de resolución de conflictos de actualización en cola  
  
1.  En la página **Opciones de suscripción**, del cuadro de diálogo **Propiedades de la publicación - \<Publicación>**, seleccione uno de los siguientes valores para la opción **Directiva de resolución de conflictos**:  
  
    -   **Mantener el cambio del publicador**  
  
    -   **Mantener el cambio del suscriptor**  
  
    -   **Reinicializar la suscripción**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Habilitar suscripciones actualizables para publicaciones transaccionales](enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
