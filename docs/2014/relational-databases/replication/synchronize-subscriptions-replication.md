---
title: Sincronizar suscripciones (replicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d82ef2a50da415504c2a7c461e652beb7547d501
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772024"
---
# <a name="synchronize-subscriptions-replication"></a>Sincronizar suscripciones (replicación)
  Los agentes de replicación sincronizan las suscripciones. El Agente de distribución sincroniza las suscripciones con las publicaciones transaccionales y de instantáneas, y el Agente de mezcla sincroniza las suscripciones con las publicaciones de combinación. Puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimientos almacenados de replicación y Replication Management Objects (RMO) para sincronizar las suscripciones y controlar el comportamiento de la sincronización. Los temas siguientes describen cómo sincronizar las suscripciones y especificar las opciones de sincronización.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)  
  
-   [Crear una instantánea para una publicación de mezcla con filtros con parámetros](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales &#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inicializar una suscripción manualmente](initialize-a-subscription-manually.md)  
  
-   [Sincronizar una suscripción de extracción](synchronize-a-pull-subscription.md)  
  
-   [Sincronizar una suscripción de inserción](synchronize-a-push-subscription.md)  
  
-   [Reinicializar una suscripción](reinitialize-a-subscription.md)  
  
-   [Ejecutar scripts antes y después de aplicar una instantánea &#40;SQL Server Management Studio&#41;](execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Ejecutar scripts durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [Ver conflictos de datos para publicaciones transaccionales &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Administrador de sincronización de Windows&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [Implementar un controlador de lógica de negocios para un artículo de mezcla](implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Depurar un controlador de lógica de negocios &#40;programación de la replicación&#41;](debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controlar el comportamiento de desencadenadores y restricciones durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>Vea también  
 [Sincronizar datos](synchronize-data.md)  
  
  
