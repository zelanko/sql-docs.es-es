---
title: 'Guía del programador: temas de procedimientos (replicación) | Microsoft Docs'
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ea57ad6fed81479ee7191b683f9c79ef35fd67c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="developer39s-guide-how-to-topics-replication"></a>Guía del programador: temas de procedimientos (replicación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema proporciona vínculos a información acerca cómo realizar las tareas relacionadas con la replicación mediante programación.  
  
## <a name="securing-a-replication-topology"></a>Proteger una topología de replicación  
  
-   [Ver y modificar la configuración de seguridad de la replicación](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [Administrar inicios de sesión en la lista de acceso a la publicación](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>Configurar, modificar y deshabilitar la publicación y distribución (replicación)  
  
-   [Configurar la publicación y la distribución](../../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Deshabilitar la publicación y la distribución](../../../relational-databases/replication/disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>Crear, modificar y eliminar publicaciones y artículos  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [er y modificar las propiedades de un artículo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Eliminar una publicación](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Eliminar un artículo](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [Crear una publicación a partir de una base de datos de Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [Establecer el período de expiración para las suscripciones](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [Especificar opciones de esquema](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [Replicar cambios de esquema](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [Administrar columnas de identidad](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [Establecer el nivel de compatibilidad para publicaciones de mezcla](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Opciones de instantánea  
  
-   [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [Entregar una instantánea mediante FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>Filtrado de datos  
  
-   [Definir y modificar un filtro de columna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [Definir y modificar un filtro de fila estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [Optimizar los filtros de fila con parámetros](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [Definir y modificar un filtro de combinación entre artículos de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Opciones de la replicación transaccional  
  
-   [Establecer el método de propagación para cambios de datos en artículos transaccionales](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [Habilitar suscripciones actualizables para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Opciones de la replicación de mezcla  
  
-   [Definir una relación de registros lógicos entre artículos de tabla de mezcla](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [Especificar el orden de procesamiento de la mezcla de artículos de tabla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [Especificar que un artículo de tabla de mezcla es de solo descarga](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [Especificar que no se debe realizar un seguimiento de las eliminaciones para los artículos de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [Especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [Especificar un solucionador de artículos de mezcla](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [Especificar la resolución interactiva de conflictos para artículos de mezcla](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>Crear, modificar y eliminar suscripciones  
  
-   [Crear una suscripción de extracción](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
-   [Ver y modificar las propiedades de una suscripción de extracción](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
-   [Eliminar una suscripción de extracción](../../../relational-databases/replication/delete-a-pull-subscription.md)  
  
-   [Crear una suscripción de inserción](../../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Ver y modificar las propiedades de una suscripción de inserción](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
-   [Eliminar una suscripción de inserción](../../../relational-databases/replication/delete-a-push-subscription.md)  
  
-   [Especificar programaciones de sincronización](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
-   [Crear una suscripción actualizable en una publicación transaccional](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)
  
-   [Crear una suscripción para un suscriptor que no sea de SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>Sincronizar suscripciones  
  
-   [Crear y aplicar la instantánea inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inicializar una suscripción manualmente](../../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [Sincronizar una suscripción de extracción](../../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizar una suscripción de inserción](../../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [Reinicializar una suscripción](../../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [Ejecutar scripts durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Implementar un controlador de lógica de negocios para un artículo de mezcla](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Depurar un controlador de lógica de negocios &#40;programación de la replicación&#41;](../../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controlar el comportamiento de desencadenadores y restricciones durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>Administrar una topología de replicación  
  
-   [Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Validar datos en el suscriptor](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
-   [Administrar particiones para una publicación de mezcla mediante filtros con parámetros](../../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Realizar una carga masiva de datos en tablas de una publicación de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [Limpiar metadatos de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [Realizar una actualización ficticia de un artículo de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [Ver comandos replicados y otra información en la base de datos de distribución &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Habilitar copias de seguridad coordinadas para la replicación transaccional &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [Quiesce a Replication Topology &#40;Replication Transact-SQL Programming&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md) (Cómo detener una topología de replicación [programación de la replicación con Transact-SQL])  
  
-   [Configurar el trabajo del conjunto de transacciones para un publicador de Oracle &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [Actualizar scripts de replicación &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>Supervisar una topología de replicación  
  
-   [Permitir el uso del Monitor de replicación a los usuarios que no son administradores](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [Supervisar la replicación mediante programación](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
-   [Ver comandos replicados y otra información en la base de datos de distribución &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
-   [Medir la latencia y validar las conexiones de la replicación transaccional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
