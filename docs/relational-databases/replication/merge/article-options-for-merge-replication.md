---
title: "Opciones de art&#237;culos para replicaci&#243;n de mezcla | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación de mezcla [replicación de SQL Server], opciones de artículo"
  - "artículos [replicación de SQL Server], opciones de replicación de mezcla"
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Opciones de art&#237;culos para replicaci&#243;n de mezcla
  Existen muchas opciones para los artículos de tablas de mezcla que le permiten personalizar el comportamiento de la replicación en función de las necesidades de sus aplicaciones. Con la replicación de mezcla, puede hacer lo siguiente:  
  
-   Utilizar filtros de fila, filtros combinados y filtros de columna. Filtrar artículos de tabla permite crear particiones de los datos que se van a publicar. Para obtener más información, consulte [filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Especificar si los cambios en el suscriptor se cargan en el publicador. Para las aplicaciones en las que todos o algunos de los datos deben ser de solo lectura en el suscriptor, los artículos de solo descarga proporcionan ventajas de rendimiento. Para obtener más información, consulte [optimizar el rendimiento de replicación de mezcla con artículos de la sección](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Especificar que los desencadenadores y las tablas del sistema de replicación no realicen el seguimiento de las eliminaciones de uno o varios artículos. Esta opción puede ser útil en muchas situaciones. Como por ejemplo, cuando se usan eliminaciones por lotes que no es necesario replicar. Para obtener más información, consulte [optimizar el rendimiento de replicación de mezcla con eliminar seguimiento condicional](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md).  
  
-   Especifique el orden de procesamiento de los artículos para asegurarse de que los mismos se procesan en el orden requerido por la aplicación. Para obtener más información, consulte [especificar el procesamiento de orden de combinar artículos](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
-   Especificar que un conjunto de registros relacionados se procesen como una unidad (de manera predeterminada, la replicación de mezcla procesa los cambios de las tablas fila por fila). Para obtener más información, consulte [grupo cambios en las filas relacionadas con registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
-   Utilizar la detección y resolución de conflictos para los casos en los que se pueden cambiar los mismos datos en varios nodos de una topología. Para más información, consulte [Detect and Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md).  
  
-   Especificar opciones de esquema, por ejemplo si las restricciones y los desencadenadores se copian en el suscriptor. Para obtener más información, consulte [especificar opciones de esquema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Utilice un controlador de lógica de negocios para responder a muchas condiciones durante la sincronización. Puede tratarse de cambios de datos, conflictos y errores entre otros. Para obtener más información, consulte [ejecutar lógica de negocios durante la sincronización mezcla](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## Vea también  
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  