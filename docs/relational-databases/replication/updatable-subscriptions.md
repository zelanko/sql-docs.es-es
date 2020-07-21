---
title: Suscripciones actualizables | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3cf65d8667e0fcedcb148e926a80969ec7a05642
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720662"
---
# <a name="updatable-subscriptions"></a>Suscripciones actualizables
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Con la replicación transaccional, los datos replicados deben tratarse como de solo lectura, aunque puede modificarlos en un suscriptor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante suscripciones actualizables. Si necesita modificar datos en el suscriptor, elija una de las siguientes opciones en función de sus necesidades.  
  
|Tipo de suscripción actualizable|Requisitos|  
|---------------------------------|------------------|  
|Actualización inmediata|El publicador y el suscriptor deben conectarse para actualizar datos en el suscriptor.|  
|Actualización en cola|El publicador y el suscriptor no tienen que estar conectados para actualizar datos en el suscriptor. Las actualizaciones pueden realizarse sin conexión y sincronizarse después entre el publicador y el suscriptor.|  
  
## <a name="options"></a>Opciones  
 **Replicar cambios de suscriptor**  
 Active la casilla en la columna **Replicar** para cada suscriptor que deba realizar actualizaciones. Para los suscriptores que pueden realizar actualizaciones, seleccione la opción apropiada en el cuadro de lista desplegable de la columna **Confirmar en el publicador** :  
  
-   Seleccione **Confirmar cambios simultáneamente** para realizar una suscripción de actualización inmediata.  
  
-   Seleccione **Poner en cola cambios y confirmar cuando sea posible** para realizar una suscripción de actualización en cola.  
  
## <a name="see-also"></a>Consulte también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
