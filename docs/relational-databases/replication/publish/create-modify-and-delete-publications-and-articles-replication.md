---
title: Creación, modificación y eliminación de publicaciones y artículos (replicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
ms.assetid: e66d06ec-a12b-444d-875b-77f958af2f21
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8680a77f6a7ac44c9e3b72636db79f325e4d5db8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="create-modify-and-delete-publications-and-articles-replication"></a>Crear, modificar y eliminar publicaciones y artículos (replicación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta sección de la documentación contiene información acerca de los procedimientos de las tareas relacionadas con la creación de publicaciones y la definición de artículos.  
  
## <a name="in-this-section"></a>En esta sección  
  
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
  
## <a name="snapshot-options"></a>Opciones de instantánea  
  
-   [Especificar el formato de instantánea &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-snapshot-format-sql-server-management-studio.md)  
  
-   [Especificar una ubicación de carpeta de instantáneas alternativa &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   [Comprimir archivos de instantáneas &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   [Configurar propiedades de instantáneas &#40;Replication Transact-SQL Programming&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [Ejecutar scripts antes y después de aplicar una instantánea &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Entregar una instantánea mediante FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
## <a name="filtering-data"></a>Filtrado de datos  
  
-   [Definir y modificar un filtro de columna](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [Definir y modificar un filtro de fila estático](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [Optimizar los filtros de fila con parámetros](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [Definir y modificar un filtro de combinación entre artículos de mezcla](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
-   [Generar automáticamente un conjunto de filtros de combinación entre artículos de mezcla &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)  
  
## <a name="transactional-replication-options"></a>Opciones de la replicación transaccional  
  
-   [Establecer el método de propagación para cambios de datos en artículos transaccionales](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [Habilitar suscripciones actualizables para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
-   [Establecer opciones de resolución de conflictos de actualización en cola &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   [Publicar la ejecución de un procedimiento almacenado en una publicación transaccional &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
## <a name="merge-replication-options"></a>Opciones de la replicación de mezcla  
  
-   [Definir una relación de registros lógicos entre artículos de tabla de mezcla](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [Especificar el orden de procesamiento de la mezcla de artículos de tabla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [Especificar que un artículo de tabla de mezcla es de solo descarga](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [Especificar que no se debe realizar un seguimiento de las eliminaciones para los artículos de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [Especificar el seguimiento de conflictos y el nivel de resolución para artículos de mezcla](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [Especificar un solucionador de artículos de mezcla](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [Especificar la resolución interactiva de conflictos para artículos de mezcla](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="see-also"></a>Ver también  
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
