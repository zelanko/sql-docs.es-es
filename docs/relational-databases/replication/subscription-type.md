---
title: "Tipo de suscripción | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4618c40e494cd53f48b859a514976da3b29ea322
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="subscription-type"></a>Tipo de suscripción
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] La replicación de mezcla proporciona dos tipos de suscripción: servidor y cliente (denominadas en versiones anteriores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] global y local, respectivamente). Los suscriptores con una suscripción de servidor pueden:  
  
-   Volver a publicar datos en otros suscriptores.  
  
-   Servir como asociados de sincronización alternativos.  
  
-   Solucionador de conflictos en función de la prioridad establecida.  
  
 La mayoría de los suscriptores no necesitan esta funcionalidad y pueden usar la suscripción de cliente. Las suscripciones de cliente todavía permiten la detección y resolución de conflictos, pero los suscriptores no tienen asignada una prioridad: el primer suscriptor que envía un cambio al publicador gana cualquier conflicto que pueda surgir de ese cambio.  
  
> [!NOTE]  
>  El tipo de suscripción no se puede cambiar una vez creada la suscripción.  
  
## <a name="options"></a>.  
 **Propiedades de la suscripción**  
 Para cada suscriptor, seleccione **Cliente** o **Servidor** en el cuadro de lista desplegable de la columna **Tipo de suscripción** . Para los suscriptores con suscripciones de servidor, escriba un número entre 0 y 99,99 en la columna **Prioridad para la resolución de conflictos** (cuanto mayor sea el número, más alta será la prioridad del suscriptor).  
  
## <a name="see-also"></a>Ver también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
