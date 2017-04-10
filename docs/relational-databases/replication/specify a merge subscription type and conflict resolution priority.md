---
title: "Especificar un tipo de suscripci&#243;n de mezcla y la prioridad de resoluci&#243;n de conflictos (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "02/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], solucionador de suscripción de mezcla"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Especificar un tipo de suscripci&#243;n de mezcla y la prioridad de resoluci&#243;n de conflictos (SQL Server Management Studio)
  Especifique un tipo de suscripción de mezcla y la prioridad de resolución de conflictos en la página **Tipo de suscripción** del Asistente para nuevas suscripciones. Para obtener más información sobre cómo utilizar este asistente, vea [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) y [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
 Tipo de suscripción no puede modificarse una vez que se crea una suscripción, pero se puede modificar la prioridad para el tipo de suscripción de servidor en la **Propiedades de suscripción - \< publicador>: \< Basededatosdepublicaciones>** cuadro de diálogo. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
### Para especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos  
  
1.  En la página **Tipo de suscripción** del Asistente para nuevas suscripciones, seleccione **Cliente** o **Servidor** en la opción **Tipo de suscripción** .  
  
2.  Si selecciona un tipo de suscripción de **Server**, escribir un valor (de 0,00 a 99,99) para el **prioridad para la resolución de conflictos** opción.  
  
### Para modificar la prioridad de resolución de conflictos  
  
1.  En la **Propiedades de suscripción - \< publicador>: \< Basededatosdepublicaciones>** en el publicador, escriba un valor (de 0,00 a 99,99) para el **prioridad** opción.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  