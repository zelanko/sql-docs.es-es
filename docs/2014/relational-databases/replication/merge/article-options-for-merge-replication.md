---
title: Opciones de artículos para replicación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 216baab358f151b3e963a4b87f7dbc194a5a2e92
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049415"
---
# <a name="article-options-for-merge-replication"></a>Opciones de artículos para replicación de mezcla
  Existen muchas opciones para los artículos de tablas de mezcla que le permiten personalizar el comportamiento de la replicación en función de las necesidades de sus aplicaciones. Con la replicación de mezcla, puede hacer lo siguiente:  
  
-   Utilizar filtros de fila, filtros combinados y filtros de columna. Filtrar artículos de tabla permite crear particiones de los datos que se van a publicar. Para obtener más información, vea [Filtrar datos publicados](../publish/filter-published-data.md).  
  
-   Especificar si los cambios en el suscriptor se cargan en el publicador. Para las aplicaciones en las que todos o algunos de los datos deben ser de solo lectura en el suscriptor, los artículos de solo descarga proporcionan ventajas de rendimiento. Para más información, vea [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Especificar que los desencadenadores y las tablas del sistema de replicación no realicen el seguimiento de las eliminaciones de uno o varios artículos. Esta opción puede ser útil en muchas situaciones. Como por ejemplo, cuando se usan eliminaciones por lotes que no es necesario replicar. Para más información, vea [Optimizar el rendimiento de la replicación de mezcla con seguimiento condicional de eliminaciones](optimize-merge-replication-performance-with-conditional-delete-tracking.md).  
  
-   Especifique el orden de procesamiento de los artículos para asegurarse de que los mismos se procesan en el orden requerido por la aplicación. Para más información, vea [Specify merge replication properties](../publish/specify-merge-replication-properties.md) (Especificación de propiedades de replicación de mezcla).  
  
-   Especificar que un conjunto de registros relacionados se procesen como una unidad (de manera predeterminada, la replicación de mezcla procesa los cambios de las tablas fila por fila). Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](group-changes-to-related-rows-with-logical-records.md).  
  
-   Utilizar la detección y resolución de conflictos para los casos en los que se pueden cambiar los mismos datos en varios nodos de una topología. Para más información, vea [Detectar y solucionar conflictos de replicación de mezcla](advanced-merge-replication-conflict-detection-and-resolution.md).  
  
-   Especificar opciones de esquema, por ejemplo si las restricciones y los desencadenadores se copian en el suscriptor. Para obtener más información, vea [Especificar opciones de esquema](../publish/specify-schema-options.md).  
  
-   Utilice un controlador de lógica de negocios para responder a muchas condiciones durante la sincronización. Puede tratarse de cambios de datos, conflictos y errores entre otros. Para obtener más información, consulte [Ejecutar lógica de negocios durante la sincronización de mezcla](execute-business-logic-during-merge-synchronization.md).  
  
## <a name="see-also"></a>Consulte también  
 [Publicar datos y objetos de base de datos](../publish/publish-data-and-database-objects.md)  
  
  
