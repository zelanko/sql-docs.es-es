---
title: Especifique un tipo de suscripción de mezcla y la prioridad de resolución de conflictos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dbd6f31a08527b8a04201ffced9d03642da8a290
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188565"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>Especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos (SQL Server Management Studio)
  Especifique un tipo de suscripción de mezcla y la prioridad de resolución de conflictos en la página **Tipo de suscripción** del Asistente para nuevas suscripciones. Para obtener más información sobre cómo utilizar este asistente, vea [Create a Pull Subscription](create-a-pull-subscription.md) y [Create a Push Subscription](create-a-push-subscription.md).  
  
 El tipo de suscripción no se puede modificar después de crear la suscripción, pero se puede modificar la prioridad del tipo de suscripción de servidor en el cuadro de diálogo **Propiedades de suscripción - \<Publicador>: \<baseDeDatosDePublicación>**. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md).  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Para especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos  
  
1.  En la página **Tipo de suscripción** del Asistente para nuevas suscripciones, seleccione **Cliente** o **Servidor** en la opción **Tipo de suscripción** .  
  
2.  Si selecciona el tipo de suscripción **Servidor**, escriba también un valor (de 0,00 a 99,99) en la opción **Prioridad para la resolución de conflictos** .  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>Para modificar la prioridad de resolución de conflictos  
  
1.  En **Propiedades de suscripción - \<Publicador>: \<baseDeDatosDePublicación>**, en el publicador, escriba un valor (de 0,00 a 99,99) para la opción **Prioridad**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
