---
title: Optimización del rendimiento de los artículos de solo descarga (combinación)
description: Describe cómo optimizar el rendimiento de los artículos de solo descarga usados por la replicación de combinación.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1d773da4bf6159727e928fa6a735366b706c1a5b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882259"
---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  La replicación de mezcla ofrece dos tipos de artículos diferentes para satisfacer las necesidades de distintas aplicaciones. Las publicaciones pueden contener uno o varios de cada uno de estos tipos de artículos, según sea necesario para la aplicación:  
  
-   Artículos estándar  
  
-   artículos de solo descarga  
  
 Los artículos de solo descarga proporcionan ventajas de rendimiento sobre los artículos estándar y deben utilizarse cuando sea necesario.  
  
> [!NOTE]  
>  Para utilizar artículos de solo descarga, el nivel de compatibilidad de la publicación debe ser como mínimo de 90RTM.  
  
## <a name="standard-articles"></a>Artículos estándar  
 Los artículos estándar son la opción predeterminada y ofrecen toda la gama de características de replicación de mezcla, incluida la detección y resolución de conflictos. Los artículos estándar son adecuados para tablas que son actualizadas por varios suscriptores; los objetos que no son tablas, como vistas y procedimientos almacenados, siempre se publican como artículos estándar.  
  
## <a name="download-only-articles"></a>artículos de solo descarga  
 Los artículos de solo descarga están diseñados para aplicaciones con datos que no se actualizan en los suscriptores, como un conjunto de artículos contenidos en un catálogo de productos. Un catálogo de productos se actualiza normalmente en el publicador, pero no en los suscriptores. Los artículos de solo descarga no se pueden actualizar en el suscriptor, y por ello los metadatos de seguimiento no se envían a los suscriptores. Esto puede reducir la capacidad de almacenamiento en los suscriptores y aumentar el rendimiento, sobre todo si la conexión de red es lenta.  
  
 Los artículos de solo descarga funcionan junto con las suscripciones de cliente: si un artículo se designa como de solo descarga, las filas de dicho artículo no se pueden insertar, actualizar ni eliminar en los suscriptores que utilizan suscripciones de cliente. Los publicadores y suscriptores que utilizan el tipo de suscripción de servidor (normalmente, suscriptores que republican datos en otros suscriptores) pueden insertar, actualizar y eliminar datos. Para obtener más información sobre las suscripciones de cliente, vea [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md).  
  
 Para especificar que un artículo es de solo descarga, vea [ Especificación de las propiedades de replicación de mezcla](../../../relational-databases/replication/merge/specify-merge-replication-properties.md).  
  
## <a name="using-different-article-types-in-your-applications"></a>Usar diferentes tipos de artículos en las aplicaciones  
 Entendiendo los requisitos de la aplicación puede lograr un equilibrio entre la flexibilidad máxima y el rendimiento óptimo. Por ejemplo, las aplicaciones con numerosos conflictos y cambios tanto en el publicador como en los suscriptores utilizarán una publicación compuesta por artículos estándar. Algunas aplicaciones, como una aplicación de automatización del personal de ventas, pueden tener artículos con un potencial de conflictos, y otros artículos que funcionan como tablas de búsqueda, que se pueden especificar como de solo descarga. Las aplicaciones de entrada de datos, como los sistemas de punto de venta y las aplicaciones de automatización del personal de campo, a menudo particionan los datos de manera que se eliminen los conflictos, y los datos de un suscriptor nunca llegan a otro. En estas situaciones, una combinación de particiones no superpuestas, artículos de solo descarga y particiones precalculadas proporciona el máximo rendimiento y escalabilidad. Para obtener más información acerca de las particiones no superpuestas y las particiones precalculadas, vea [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de artículos para replicación de mezcla](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Optimizar el rendimiento de la replicación de mezcla con seguimiento condicional de eliminaciones](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
