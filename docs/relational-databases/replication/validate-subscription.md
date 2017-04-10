---
title: "Validar suscripci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.validate.validateandresynch.f1"
helpviewer_keywords: 
  - "Validar suscripción, cuadro de diálogo"
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Validar suscripci&#243;n
  Use el cuadro de diálogo **Validar suscripción** para especificar que es necesario validar una suscripción a una publicación de combinación la próxima vez que se ejecute el Agente de mezcla para la suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
 También es posible validar todas las suscripciones a una publicación de mezcla con el botón secundario en una publicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y haga clic en **Validar todas las suscripciones**.  
  
## Opciones  
 **Fecha del último intento de validación**  
 Muestra la fecha de la última sesión del Agente de mezcla en la que se validó la suscripción, independientemente de si la validación se realizó correctamente.  
  
 **Fecha de la última validación correcta**  
 Muestra la fecha de la sesión del Agente de mezcla en la que se realizó correctamente la validación de la suscripción.  
  
 **Validar esta suscripción**  
 Seleccione esta opción para validar la suscripción.  
  
 **Opciones**  
 Haga clic en para tener acceso a la **Opciones de validación de suscripción** cuadro de diálogo que le permite especificar si desea utilizar la validación de recuento de filas o la validación de suma de comprobación binaria.  
  
## Vea también  
 [Validar datos replicados](../../relational-databases/replication/validate-replicated-data.md)  
  
  