---
title: "Suscripciones actualizables | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.updatablesubscriptions.f1"
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Suscripciones actualizables
  Con la duplicación transaccional, los datos replicados deben tratarse como de solo lectura; Sin embargo, puede modificar los datos duplicados en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptor mediante suscripciones actualizables. Si necesita modificar datos en el suscriptor, elija una de las siguientes opciones en función de sus necesidades.  
  
|Tipo de suscripción actualizable|Requisitos|  
|---------------------------------|------------------|  
|Actualización inmediata|El publicador y el suscriptor deben conectarse para actualizar datos en el suscriptor.|  
|Actualización en cola|El publicador y el suscriptor no tienen que estar conectados para actualizar datos en el suscriptor. Las actualizaciones pueden realizarse sin conexión y sincronizarse después entre el publicador y el suscriptor.|  
  
## Opciones  
 **Replicar cambios de suscriptor**  
 Active la casilla de verificación en la **replicar** columna para cada suscriptor que debe ser capaz de realizar actualizaciones. Para los suscriptores que se pueden realizar actualizaciones, seleccione la opción adecuada en el cuadro de lista desplegable de la **Confirmar en el publicador** columna:  
  
-   Seleccione **Confirmar cambios simultáneamente** para realizar una suscripción de actualización inmediata.  
  
-   Seleccione **Poner en cola cambios y confirmar cuando sea posible** para realizar una suscripción de actualización en cola.  
  
## Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  