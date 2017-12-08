---
title: Suscripciones actualizables | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 139c6e956eb8f54df670f9c913988d80b05d14b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="updatable-subscriptions"></a>Suscripciones actualizables
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Con la replicación transaccional, los datos replicados deben tratarse como de solo lectura; sin embargo, puede modificarlos en un suscriptor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante suscripciones actualizables. Si necesita modificar datos en el suscriptor, elija una de las siguientes opciones en función de sus necesidades.  
  
|Tipo de suscripción actualizable|Requisitos|  
|---------------------------------|------------------|  
|Actualización inmediata|El publicador y el suscriptor deben conectarse para actualizar datos en el suscriptor.|  
|Actualización en cola|El publicador y el suscriptor no tienen que estar conectados para actualizar datos en el suscriptor. Las actualizaciones pueden realizarse sin conexión y sincronizarse después entre el publicador y el suscriptor.|  
  
## <a name="options"></a>Opciones  
 **Replicar cambios de suscriptor**  
 Active la casilla en la columna **Replicar** para cada suscriptor que deba realizar actualizaciones. Para los suscriptores que pueden realizar actualizaciones, seleccione la opción apropiada en el cuadro de lista desplegable de la columna **Confirmar en el publicador** :  
  
-   Seleccione **Confirmar cambios simultáneamente** para realizar una suscripción de actualización inmediata.  
  
-   Seleccione **Poner en cola cambios y confirmar cuando sea posible** para realizar una suscripción de actualización en cola.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
