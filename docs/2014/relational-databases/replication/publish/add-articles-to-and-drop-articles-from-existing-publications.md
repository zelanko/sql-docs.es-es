---
title: Agregar y quitar artículos de publicaciones existentes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 44
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 56a4730e9775a88865da8c59c8f3ef5c60d14839
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109435"
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>Agregar y quitar artículos de publicaciones existentes
  Después de crear una publicación, se le pueden agregar y quitar artículos. Se pueden agregar artículos en cualquier momento, pero las acciones necesarias para quitar artículos dependen del tipo de replicación y del momento en que se quite el artículo.  
  
## <a name="adding-articles"></a>agregar artículos  
 Para agregar un artículo, es necesario agregar el artículo a la publicación, crear una instantánea nueva para la publicación y sincronizar la suscripción para aplicar el esquema y los datos para el nuevo artículo.  
  
> [!NOTE]  
>  Si se agrega un artículo a una publicación de combinación y ya hay un artículo que depende de este nuevo artículo, debe especificar un orden de procesamiento para los dos artículos con el parámetro **@processing_order** de [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) y [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Considere el caso siguiente: publica una tabla pero no publica una función a la que hace referencia la tabla. Si no publica la función, la tabla no se puede crear en el suscriptor. Al agregar la función a la publicación: especifique el valor **1** para el parámetro **@processing_order** de **sp_addmergearticle**y el valor **2** para el parámetro **@processing_order** de **sp_changemergearticle**; especifique el nombre de la tabla para el parámetro **@article**. Este orden de procesamiento garantiza que la función se cree en el suscriptor antes que la tabla que depende de él. Puede usar números distintos para cada artículo, siempre que el número de la función sea inferior al de la tabla.  
  
1.  Agregue uno o más artículos con uno de estos métodos:  
  
    -   [Agregar y quitar artículos de una publicación &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Definir un artículo](define-an-article.md)  
  
2.  Después de agregar un artículo a una publicación, debe crear una nueva instantánea para la publicación (y todas las particiones, si se trata de una publicación de combinación con filtros con parámetros). A continuación, el Agente de distribución o de mezcla copia el esquema y los datos del nuevo artículo al suscriptor (sin reinicializar la publicación completa).  
  
    -   Para crear una instantánea nueva, vea [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
    -   Para crear una instantánea para una publicación de mezcla con filtros con parámetros, consulte [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Una vez creada la instantánea, sincronice la suscripción para copiar el esquema y los datos para el nuevo artículo.  
  
    -   Para sincronizar una suscripción de inserción, consulte [Sincronizar una suscripción de inserción](../synchronize-a-push-subscription.md).  
  
    -   Para sincronizar una suscripción de extracción, consulte [Sincronizar una suscripción de extracción](../synchronize-a-pull-subscription.md).  
  
## <a name="dropping-articles"></a>quitar artículos  
 Puede quitar artículos de una publicación en cualquier momento, pero debe tener en cuenta los siguientes comportamientos:  
  
-   Al quitar un artículo de una publicación no se quita el objeto de la base de datos de publicaciones ni el objeto correspondiente de la base de datos de suscripciones. Use DROP \<Object> para quitar estos objetos, si es necesario. Al quitar un artículo relacionado con otros artículos publicados a través de restricciones de clave externa, se recomienda quitar la tabla del suscriptor de forma manual o, ejecutando un script a petición, especifique un script que incluya las instrucciones DROP \<Object> apropiadas. Para obtener más información, consulte [Ejecutar scripts durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](../execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   En el caso de las publicaciones de combinación con un nivel de compatibilidad igual o superior a 90RTM, puede quitar artículos en cualquier momento, pero necesitará una instantánea nueva. Además:  
  
    -   Si un artículo es el artículo primario de un filtro de combinación o de una relación de registros lógicos, necesitará quitar primero las relaciones; para esto, es necesario reinicializar.  
  
    -   Si un artículo tiene el último filtro con parámetros de una publicación, será necesario reinicializar las suscripciones.  
  
-   En el caso de las publicaciones de combinación con un nivel de compatibilidad inferior a 90RTM, puede quitar artículos sin ningún tipo de consideraciones especiales antes de la sincronización inicial de las suscripciones. Si quita un artículo después de haber sincronizado una o varias suscripciones, deberá quitar, volver a crear y sincronizar estas suscripciones.  
  
-   En las publicaciones de instantáneas o transaccionales, se pueden quitar artículos sin ninguna consideración especial antes de crear las suscripciones. Si quita un artículo después de haber creado una o más suscripciones, deberá quitar, volver a crear y sincronizar estas suscripciones. Para obtener más información sobre cómo quitar suscripciones, consulte [Suscribirse a publicaciones](../subscribe-to-publications.md) y [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql). **sp_dropsubscription** permite quitar un único artículo de la suscripción, en lugar de toda la suscripción.  
  
1.  Para quitar un artículo de una publicación, hay que quitar el artículo y crear una instantánea nueva para la publicación. Al quitar un artículo se invalida la instantánea actual; por lo tanto, es necesario crear una instantánea nueva.  
  
    -   Para quitar un artículo de una publicación, consulte [Agregar y quitar artículos de una publicación &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md) o [Eliminar un artículo](delete-an-article.md).  
  
2.  Después de quitar un artículo de una publicación, debe crear una nueva instantánea para la publicación (y todas las particiones, si se trata de una publicación de combinación con filtros con parámetros).  
  
    -   Para crear una instantánea nueva, vea [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
    -   Para crear una instantánea para una publicación de mezcla con filtros con parámetros, consulte [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Como se indicó antes, en algunos casos es necesario quitar, volver a crear y sincronizar las suscripciones después de quitar un artículo. Para obtener más información, consulte [Suscribirse a publicaciones](../subscribe-to-publications.md) y [Sincronizar datos](../synchronize-data.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos y objetos de base de datos](publish-data-and-database-objects.md)   
 [Reinicializar suscripciones](../reinitialize-subscriptions.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md)  
  
  
