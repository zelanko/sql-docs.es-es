---
title: 'Guía del programador: temas de procedimientos (replicación) | Microsoft Docs'
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- replication
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1329e7b4da266ea6024ed8bbc760b5eed636a30a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198439"
---
# <a name="developer39s-guide-how-to-topics-replication"></a>Guía del programador: temas de procedimientos (replicación)
  Este tema proporciona vínculos a información acerca cómo realizar las tareas relacionadas con la replicación mediante programación.  
  
## <a name="securing-a-replication-topology"></a>Proteger una topología de replicación  
  
-   [Ver y modificar la configuración de seguridad de la replicación](security/view-and-modify-replication-security-settings.md)  
  
-   [Administrar inicios de sesión en la lista de acceso a la publicación](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>Configurar, modificar y deshabilitar la publicación y distribución (replicación)  
  
-   [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)  
  
-   [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)  
  
-   [Deshabilitar la publicación y la distribución](disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>Crear, modificar y eliminar publicaciones y artículos  
  
-   [Create a Publication](publish/create-a-publication.md)  
  
-   [Definir un artículo](publish/define-an-article.md)  
  
-   [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)  
  
-   [er y modificar las propiedades de un artículo](publish/view-and-modify-article-properties.md)  
  
-   [Eliminar una publicación](publish/delete-a-publication.md)  
  
-   [Eliminar un artículo](publish/delete-an-article.md)  
  
-   [Crear una publicación a partir de una base de datos de Oracle](publish/create-a-publication-from-an-oracle-database.md)  
  
-   [Establecer el período de expiración para las suscripciones](publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [Especificar opciones de esquema](publish/specify-schema-options.md)  
  
-   [Replicar cambios de esquema](publish/replicate-schema-changes.md)  
  
-   [Administrar columnas de identidad](publish/manage-identity-columns.md)  
  
-   [Establecer el nivel de compatibilidad para publicaciones de mezcla](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Opciones de instantánea  
  
-   [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [Entregar una instantánea mediante FTP](publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>Filtrado de datos  
  
-   [Definir y modificar un filtro de columna](publish/define-and-modify-a-column-filter.md)  
  
-   [Definir y modificar un filtro de fila estático](publish/define-and-modify-a-static-row-filter.md)  
  
-   [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [Optimizar los filtros de fila con parámetros](merge/parameterized-filters-parameterized-row-filters.md)  
  
-   [Definir y modificar un filtro de combinación entre artículos de mezcla](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Opciones de la replicación transaccional  
  
-   [Establecer el método de propagación para cambios de datos en artículos transaccionales](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [Habilitar suscripciones actualizables para publicaciones transaccionales](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Opciones de la replicación de mezcla  
  
-   [Definir una relación de registros lógicos entre artículos de tabla de mezcla](publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [Especificar el orden de procesamiento de la mezcla de artículos de tabla &#40;programación de la replicación con Transact-SQL&#41;](publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [Especificar que un artículo de tabla de mezcla es de solo descarga](publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [Especificar que no se debe realizar un seguimiento de las eliminaciones para los artículos de mezcla &#40;programación de la replicación con Transact-SQL&#41;](publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [Especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla](publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [Especificar un solucionador de artículos de mezcla](publish/specify-a-merge-article-resolver.md)  
  
-   [Especificar la resolución interactiva de conflictos para artículos de mezcla](publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>Crear, modificar y eliminar suscripciones  
  
-   [Crear una suscripción de extracción](create-a-pull-subscription.md)  
  
-   [Ver y modificar las propiedades de una suscripción de extracción](view-and-modify-pull-subscription-properties.md)  
  
-   [Eliminar una suscripción de extracción](delete-a-pull-subscription.md)  
  
-   [Crear una suscripción de inserción](create-a-push-subscription.md)  
  
-   [Ver y modificar las propiedades de una suscripción de inserción](view-and-modify-push-subscription-properties.md)  
  
-   [Eliminar una suscripción de inserción](delete-a-push-subscription.md)  
  
-   [Especificar programaciones de sincronización](specify-synchronization-schedules.md)  
  
-   [Crear una suscripción actualizable en una publicación transaccional](create-updatable-subscription-transactional-publication-transact-sql.md)  
  
-   [Crear una suscripción para un suscriptor que no sea de SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>Sincronizar suscripciones  
  
-   [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)  
  
-   [Crear una instantánea para una publicación de mezcla con filtros con parámetros](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inicializar una suscripción manualmente](initialize-a-subscription-manually.md)  
  
-   [Sincronizar una suscripción de extracción](synchronize-a-pull-subscription.md)  
  
-   [Sincronizar una suscripción de inserción](synchronize-a-push-subscription.md)  
  
-   [Reinicializar una suscripción](reinitialize-a-subscription.md)  
  
-   [Ejecutar scripts durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Implementar un controlador de lógica de negocios para un artículo de mezcla](implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Depurar un controlador de lógica de negocios &#40;programación de la replicación&#41;](debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controlar el comportamiento de desencadenadores y restricciones durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>Administrar una topología de replicación  
  
-   [Trabajar con perfiles del Agente de replicación](agents/replication-agent-profiles.md)  
  
-   [Validar datos en el suscriptor](validate-data-at-the-subscriber.md)  
  
-   [Administrar particiones para una publicación de mezcla mediante filtros con parámetros](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Realizar una carga masiva de datos en tablas de una publicación de mezcla &#40;programación de la replicación con Transact-SQL&#41;](bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [Limpiar metadatos de mezcla &#40;programación de la replicación con Transact-SQL&#41;](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [Realizar una actualización ficticia de un artículo de mezcla &#40;programación de la replicación con Transact-SQL&#41;](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [Ver comandos replicados y otra información en la base de datos de distribución &#40;programación de la replicación con Transact-SQL&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Habilitar copias de seguridad coordinadas para la replicación transaccional &#40;programación de la replicación con Transact-SQL&#41;](administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [Quiesce a Replication Topology &#40;Replication Transact-SQL Programming&#41;](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md) (Cómo detener una topología de replicación [programación de la replicación con Transact-SQL])  
  
-   [Configurar el trabajo del conjunto de transacciones para un publicador de Oracle &#40;programación de la replicación con Transact-SQL&#41;](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [Actualizar scripts de replicación &#40;programación de la replicación con Transact-SQL&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>Supervisar una topología de replicación  
  
-   [Permitir el uso del Monitor de replicación a los usuarios que no son administradores](monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [Supervisar la replicación mediante programación](monitor/monitoring-replication-overview.md)  
  
-   [Ver comandos replicados y otra información en la base de datos de distribución &#40;programación de la replicación con Transact-SQL&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](view-conflict-information-for-merge-publications.md)  
  
-   [Medir la latencia y validar las conexiones de la replicación transaccional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  