---
title: "Monitor de replicación | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.beta2.f1
helpviewer_keywords: Replication Monitor, help
ms.assetid: 39b92198-c3f6-4f25-8560-095848ad652d
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4875b39c775e1e62b81c325386833a3be7860b46
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="replication-monitor"></a>Monitor de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Esta sección de la documentación incluye información sobre el Monitor de replicación. Las páginas y cuadros de diálogo mostrados en el monitor son diferentes según el tipo de replicación y la versión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se supervise.  
  
-   [Monitor de replicación, página Principal](../../relational-databases/replication/replication-monitor-main-page.md)  
  
-   [Agregar publicador](../../relational-databases/replication/add-publisher.md)  
  
-   [Configuración del distribuidor](../../relational-databases/replication/distributor-settings.md)  
  
-   [Información de distribuidor, Publicaciones](../../relational-databases/replication/distributor-information-publications.md)  
  
-   [Información del distribuidor, Lista de supervisión de suscripciones &#40;Publicación transaccional, SQL Server 2005 y versiones posteriores&#41;](../../relational-databases/replication/distributor-info-subscription-watch-list-transaction-pub-sql-2005.md)  
  
-   [Información de distribuidor, Lista de supervisión de suscripciones &#40;Publicación de combinación, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/distributor-info-subscription-watch-list-merge-pub-sql-2005.md)  
  
-   [Información de distribuidor, Lista de supervisión de suscripciones &#40;Publicación de instantáneas, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/distributor-info-subscription-watch-list-snapshot-pub-sql-2005.md)  
  
-   [Información del distribuidor, Agentes](../../relational-databases/replication/distributor-information-agents.md)  
  
-   [Configuración del publicador](../../relational-databases/replication/publisher-settings.md)  
  
-   [Información del publicador, Publicaciones](../../relational-databases/replication/publisher-information-publications.md)  
  
-   [Información del publicador, Lista de supervisión de suscripciones &#40;Publicación transaccional, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-transactional.md)  
  
-   [Información de publicador, Lista de supervisión de suscripciones &#40;Publicación de combinación, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-merge-publication.md)  
  
-   [Información de publicador, Lista de supervisión de suscripciones &#40;Publicación de instantáneas, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-snapshot.md)  
  
-   [Información de publicador, Agentes](../../relational-databases/replication/publisher-information-agents.md)  
  
-   [Información de publicación, Todas las suscripciones &#40;Publicación transaccional&#41;](../../relational-databases/replication/publication-information-all-subscriptions-transactional-publication.md)  
  
-   [Información de publicación, Todas las suscripciones &#40;Publicación de combinación&#41;](../../relational-databases/replication/publication-information-all-subscriptions-merge-publication.md)  
  
-   [Información de publicación, Todas las suscripciones &#40;Publicación de instantáneas&#41;](../../relational-databases/replication/publication-information-all-subscriptions-snapshot-publication.md)  
  
-   [Información de publicación, Advertencias &#40;Publicación transaccional, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/publication-information-warnings-transactional-publication.md)  
  
-   [Información de publicación, Advertencias &#40;Publicación de combinación, SQL Server 2005 y posterior&#41;](../../relational-databases/replication/publication-information-warnings-merge-publication-sql-server-2005-and-later.md)  
  
-   [Información de publicación, Advertencias &#40;Publicación de instantáneas, SQL Server 2005 y posterior&#41;](../../relational-databases/replication/publication-information-warnings-snapshot-publication-sql-server-2005-and-later.md)  
  
-   [Información de publicación, Agentes &#40;Publicación transaccional&#41;](../../relational-databases/replication/publication-information-agents-transactional-publication.md)  
  
-   [Información de la Publicación, Agentes &#40;Publicación de combinación&#41;](../../relational-databases/replication/publication-information-agents-merge-publication.md)  
  
-   [Información de publicación, Agentes &#40;Publicación de instantáneas&#41;](../../relational-databases/replication/publication-information-agents-snapshot-publication.md)  
  
-   [Información de la publicación, Testigos de seguimiento &#40;Publicación transaccional, SQL Server 2005 y posterior&#41;](../../relational-databases/replication/publication-information-tracer-tokens-sql-server-2005-and-later.md)  
  
-   [Suscripción, comandos sin distribuir &#40;Suscripción transaccional, SQL Server 2005 y posteriores&#41;](../../relational-databases/replication/subscription-undistributed-commands-transactional-subscription.md)  
  
-   [Suscripción, Historial de Publicador a distribuidor &#40;Suscripción transaccional&#41;](../../relational-databases/replication/subscription-publisher-to-distributor-history-transactional-subscription.md)  
  
-   [Suscripción, Historial de Distribuidor a suscriptor &#40;Suscripción transaccional&#41;](../../relational-databases/replication/subscription-distributor-to-subscriber-history-transactional-subscription.md)  
  
-   [Suscripción, Historial de sincronizaciones &#40;Suscripción de mezcla, SQL Server 2005 y versiones posteriores&#41;](../../relational-databases/replication/subscription-synchronization-history.md)  
  
-   [Suscripción, Historial de sincronizaciones &#40;Suscripción de mezcla, SQL Server 2000&#41;](../../relational-databases/replication/subscription-synchronization-history-merge-subscription-sql-server-2000.md)  
  
-   [Suscripción, Historial de Distribuidor a suscriptor &#40;Suscripción de instantánea&#41;](../../relational-databases/replication/subscription-distributor-to-subscriber-history-snapshot-subscription.md)  
  
-   [Agente de lector del registro](../../relational-databases/replication/log-reader-agent.md)  
  
-   [Agente de lectura de cola](../../relational-databases/replication/queue-reader-agent.md)  
  
-   [Agente de instantáneas](../../relational-databases/replication/snapshot-agent.md)  
  
-   [Configuración del filtro](../../relational-databases/replication/filter-settings.md)  
  
-   [Ordenar columnas](../../relational-databases/replication/sort-columns.md)  
  
## <a name="see-also"></a>Ver también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  (Supervisar la replicación)  
 [Referencia de propiedades &#40;replicación&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
