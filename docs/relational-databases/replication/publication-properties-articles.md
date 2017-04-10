---
title: "Propiedades de la publicaci&#243;n, Art&#237;culos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.articles.f1"
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Propiedades de la publicaci&#243;n, Art&#237;culos
  La página **Artículos** del cuadro de diálogo **Propiedades de la publicación** contiene información acerca de los artículos incluidos en una publicación, le permite agregar artículos a publicaciones existentes o quitarlos de las mismas y le permite cambiar las propiedades de los artículos y los filtros de columnas.  
  
> [!NOTE]  
>  Una vez creada una publicación, algunos cambios de las propiedades requieren una nueva instantánea. Si una publicación tiene suscripciones, algunos cambios también requieren reinicializar todas las suscripciones. Para obtener más información, consulte [Propiedades de artículo y publicación de cambio](../../relational-databases/replication/publish/change-publication-and-article-properties.md) y [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 Para publicar un objeto de base de datos que depende de uno o más objetos de base de datos, debe publicar todos los objetos a los que se hace referencia. Por ejemplo, si publica una vista que depende de una tabla, también debe publicar la tabla.  
  
 Los objetos que no se pueden publicar presentan un icono rojo al lado, con una explicación en el panel de información en la parte inferior de la página del asistente. No es posible publicar los siguientes objetos:  
  
-   Objetos cifrados.  
  
-   Vistas indizadas que contienen columnas que permiten valores NULL.  
  
-   Las tablas sin claves principales no se pueden publicar en las publicaciones transaccionales.  
  
-   No es posible publicar tablas en publicaciones de combinación o publicaciones transaccionales habilitadas para suscripciones de actualización en cola. Para obtener más información acerca de cómo publicar un artículo en más de una publicación, consulte la sección "Publicación tablas en varias publicaciones" en [publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
## Publicadores de Oracle  
 Existen consideraciones adicionales para los publicadores de Oracle:  
  
-   Para obtener una lista de objetos que se pueden publicar desde Oracle, vea [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md). No se mostrarán los objetos que no se pueden publicar.  
  
-   Para obtener una lista de los tipos de datos que se pueden publicar, vea [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md). No se mostrarán columnas con tipos de datos que no se pueden publicar.  
  
## Filtros de columnas  
 Filtrar columnas en esta página debe expandir una tabla en la **objetos para publicar** panel y, a continuación, seleccionando sólo las columnas necesarias (puede filtrar las filas en el **filtrar filas de tabla** página de este asistente). Filtrar columnas es útil por diversas razones, entre las que se incluye la seguridad (evitar replicaciones de datos confidenciales) y el rendimiento (por ejemplo, evitar la replicación de columnas de objetos binarios grandes (BLOB)). Para obtener más información acerca de cómo filtrar columnas, incluida una lista de tipos de columna que no se pueden filtrar, consulte [filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md).  
  
## Opciones  
 El panel **Objetos para publicar** le permite:  
  
-   Ver todos los objetos disponibles para la replicación.  
  
-   Agregar un artículo a una publicación si activa la casilla mostrada junto al objeto.  
  
-   Quitar un objeto de una publicación si desactiva la casilla mostrada junto al objeto. Para obtener información acerca de cuándo se pueden quitar artículos, vea [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Incluir todos los objetos de un tipo determinado (por ejemplo, una tabla) en la publicación seleccionando la casilla de verificación junto al tipo de objeto (como **tablas**).  
  
-   Expandir los nodos de tabla para ver las columnas en la tabla.  
  
-   Filtrar las columnas de tabla de una publicación si desactiva la casilla mostrada junto a la columna o incluir columnas no publicadas si activa la casilla.  
  
-   Haga clic con el botón secundario en un objeto del panel para ver un menú de comandos para dicho objeto.  
  
 **Propiedades del artículo**  
 Haga clic en **Propiedades del artículo** , y, a continuación, haga clic en uno de los siguientes:  
  
-   Haga clic en **establecer propiedades de resaltado \< ObjectType> artículo** para iniciar el **Propiedades del artículo: \< ObjectName>** cuadro de diálogo; propiedad los cambios realizados en este cuadro de diálogo se aplican únicamente al objeto que está resaltado en el panel de objetos en el **artículos** página.  
  
-   Haga clic en **establecer propiedades de todos los \< ObjectType> artículos**, para iniciar la **Propiedades para todos \< ObjectType> artículos** cuadro de diálogo; propiedad los cambios realizados en este cuadro de diálogo se aplican a todos los objetos de ese tipo en el panel de objetos en el **artículos** página, las que todavía no se ha seleccionado para la publicación incluidas.  
  
    > [!NOTE]  
    >  Cambios de propiedades realizados en la **para todas las propiedades de \< ObjectType> artículos** cuadro de diálogo reemplazan los realizados anteriormente en la **Propiedades del artículo: \< ObjectName>** cuadro de diálogo. Por ejemplo, si desea establecer varios valores predeterminados para todos los artículos de un tipo de objeto, pero solamente desea establecer algunas propiedades para objetos individuales, establezca primero los valores predeterminados para todos los artículos. A continuación, establezca las propiedades de los objetos individuales.  
  
 **La tabla resaltada es de solo descarga**  
 Solo replicación de mezcla. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Seleccione esta opción para especificar qué cambios no desea permitir en el suscriptor si usa una suscripción de cliente. Los artículos de solo descarga no se pueden actualizar en el suscriptor, y por ello los metadatos de seguimiento no se envían a los suscriptores. Esto puede reducir la capacidad de almacenamiento en los suscriptores y aumentar el rendimiento, sobre todo si la conexión de red es lenta. Esta opción corresponde a un valor de **Sólo descargar en suscriptor y prohibir cambios del suscriptor** para la opción **dirección de sincronización** en la **Propiedades del artículo** cuadro de diálogo. Para obtener más información, consulte [optimizar el rendimiento de replicación de mezcla con artículos de la sección](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Mostrar solamente los objetos seleccionados en la lista**  
 Active esta casilla para mostrar solamente aquellos artículos seleccionados en el panel de objetos.  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Crear y aplicar la instantánea inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  