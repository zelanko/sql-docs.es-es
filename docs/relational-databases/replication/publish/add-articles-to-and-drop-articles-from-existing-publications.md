---
title: "Agregar y quitar art&#237;culos de publicaciones existentes | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "artículos [replicación de SQL Server], anular"
  - "eliminar artículos"
  - "artículos, quitar"
  - "quitar artículos"
  - "agregar artículos"
  - "administrar replicación, artículos"
  - "publicaciones [replicación de SQL Server], agregar y quitar artículos"
  - "artículos [replicación de SQL Server], agregar"
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Agregar y quitar art&#237;culos de publicaciones existentes
  Después de crear una publicación, se le pueden agregar y quitar artículos. Se pueden agregar artículos en cualquier momento, pero las acciones necesarias para quitar artículos dependen del tipo de replicación y del momento en que se quite el artículo.  
  
## Agregar artículos  
 Para agregar un artículo, es necesario agregar el artículo a la publicación, crear una instantánea nueva para la publicación y sincronizar la suscripción para aplicar el esquema y los datos para el nuevo artículo.  
  
> [!NOTE]  
>  Si se agrega un artículo a una publicación de mezcla y depende de un artículo existente en el nuevo artículo, debe especificar un orden de procesamiento para ambos artículos mediante el **@processing_order** parámetro de [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) y [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Considere el caso siguiente: publica una tabla pero no publica una función a la que hace referencia la tabla. Si no publica la función, la tabla no se puede crear en el suscriptor. Al agregar la función a la publicación: especifique un valor de **1** para la **@processing_order** parámetro de **sp_addmergearticle**; y especifique un valor de **2** para el **@processing_order** parámetro de **sp_changemergearticle**, especificando el nombre de tabla para el parámetro **@article**. Este orden de procesamiento garantiza que la función se cree en el suscriptor antes que la tabla que depende de él. Puede usar números distintos para cada artículo, siempre que el número de la función sea inferior al de la tabla.  
  
1.  Agregue uno o más artículos con uno de estos métodos:  
  
    -   [Agregar y quitar artículos de una publicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  Después de agregar un artículo a una publicación, debe crear una nueva instantánea para la publicación (y todas las particiones, si se trata de una publicación de combinación con filtros con parámetros). A continuación, el Agente de distribución o de mezcla copia el esquema y los datos del nuevo artículo al suscriptor (sin reinicializar la publicación completa).  
  
    -   Para crear una instantánea nueva, vea [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Para crear una nueva instantánea para una publicación de mezcla con filtros con parámetros, vea [crear una instantánea para una publicación de mezcla con filtros parametrizados](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Una vez creada la instantánea, sincronice la suscripción para copiar el esquema y los datos para el nuevo artículo.  
  
    -   Para sincronizar una suscripción de inserción, vea [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
    -   Para sincronizar una suscripción de extracción, vea [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## Quitar artículos  
 Puede quitar artículos de una publicación en cualquier momento, pero debe tener en cuenta los siguientes comportamientos:  
  
-   Al quitar un artículo de una publicación no se quita el objeto de la base de datos de publicaciones ni el objeto correspondiente de la base de datos de suscripciones. Utilice DROP \< objeto> para quitar estos objetos si es necesario. Cuando se quita un artículo que está relacionado con otros artículos publicados a través de restricciones de clave externa, se recomienda que coloque la tabla en el suscriptor manualmente o mediante la ejecución del script a petición: especificar un script que incluye la COLOCACIÓN apropiada \< objeto> instrucciones. Para obtener más información, consulte [Ejecutar Scripts durante la sincronización & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   En el caso de las publicaciones de combinación con un nivel de compatibilidad igual o superior a 90RTM, puede quitar artículos en cualquier momento, pero necesitará una instantánea nueva. Además:  
  
    -   Si un artículo es el artículo primario de un filtro de combinación o de una relación de registros lógicos, necesitará quitar primero las relaciones; para esto, es necesario reinicializar.  
  
    -   Si un artículo tiene el último filtro con parámetros de una publicación, será necesario reinicializar las suscripciones.  
  
-   En el caso de las publicaciones de combinación con un nivel de compatibilidad inferior a 90RTM, puede quitar artículos sin ningún tipo de consideraciones especiales antes de la sincronización inicial de las suscripciones. Si quita un artículo después de haber sincronizado una o varias suscripciones, deberá quitar, volver a crear y sincronizar estas suscripciones.  
  
-   En las publicaciones de instantáneas o transaccionales, se pueden quitar artículos sin ninguna consideración especial antes de crear las suscripciones. Si quita un artículo después de haber creado una o más suscripciones, deberá quitar, volver a crear y sincronizar estas suscripciones. Para obtener más información acerca de cómo quitar suscripciones, consulte [suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md) y [sp_dropsubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). **sp_dropsubscription** le permite quitar un único artículo de la suscripción, en lugar de toda la suscripción.  
  
1.  Para quitar un artículo de una publicación, hay que quitar el artículo y crear una instantánea nueva para la publicación. Al quitar un artículo se invalida la instantánea actual; por lo tanto, es necesario crear una instantánea nueva.  
  
    -   Para quitar un artículo de una publicación, vea [Agregar y quitar artículos de una publicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) o [Eliminar un artículo](../../../relational-databases/replication/publish/delete-an-article.md).  
  
2.  Después de quitar un artículo de una publicación, debe crear una nueva instantánea para la publicación (y todas las particiones, si se trata de una publicación de combinación con filtros con parámetros).  
  
    -   Para crear una instantánea nueva, vea [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Para crear una nueva instantánea para una publicación de mezcla con filtros con parámetros, vea [crear una instantánea para una publicación de mezcla con filtros parametrizados](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Como se indicó antes, en algunos casos es necesario quitar, volver a crear y sincronizar las suscripciones después de quitar un artículo. Para obtener más información, consulte [suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md) y [sincronizar datos](../../../relational-databases/replication/synchronize-data.md).  
  
## Vea también  
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  