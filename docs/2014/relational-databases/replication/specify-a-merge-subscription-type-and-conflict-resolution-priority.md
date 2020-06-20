---
title: Especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a19ae6246fe59308283fbaf2f35e2c49f96b140c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055557"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>Especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos (SQL Server Management Studio)
   Especifique un tipo de suscripción de mezcla y la prioridad de resolución de conflictos en la página **Tipo de suscripción** del Asistente para nuevas suscripciones. Para obtener más información sobre cómo utilizar este asistente, vea [Create a Pull Subscription](create-a-pull-subscription.md) y [Create a Push Subscription](create-a-push-subscription.md).  
  
 El tipo de suscripción no se puede modificar después de crear una suscripción, pero se puede modificar la prioridad del tipo de suscripción de servidor en el cuadro de diálogo **propiedades de \<Publisher> \<PublicationDatabase> suscripción** :. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md).  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>Para especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos  
  
1.  En la página **Tipo de suscripción** del Asistente para nuevas suscripciones, seleccione **Cliente** o **Servidor** en la opción **Tipo de suscripción** .  
  
2.  Si selecciona el tipo de suscripción **Servidor**, escriba también un valor (de 0,00 a 99,99) en la opción **Prioridad para la resolución de conflictos** .  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>Para modificar la prioridad de resolución de conflictos  
  
1.  En las **propiedades \<Publisher> \<PublicationDatabase> de la suscripción** : en el publicador, escriba un valor (de 0,00 a 99,99) para la opción **prioridad** .  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
