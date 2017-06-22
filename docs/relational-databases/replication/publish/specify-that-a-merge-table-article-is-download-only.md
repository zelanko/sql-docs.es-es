---
title: "Especificar que un artículo de tabla de mezcla es de solo descarga | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 83d7383aff0ccc5ab8f6716135d07c3642e6c9d6
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="specify-that-a-merge-table-article-is-download-only"></a>Especificar que un artículo de tabla de mezcla es de solo descarga
  En este tema se describe cómo especificar que un artículo de tabla de mezcla sea de solo descarga en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Los artículos de solo descarga están diseñados para aplicaciones con datos que no se actualizan en suscriptores. Para obtener más información, vea [Optimize Merge Replication Performance with Download-Only Articles](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md) (Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para especificar que un artículo de tabla de mezcla sea de solo descarga con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si se especifica que un artículo es de solo descarga después de haber inicializado las suscripciones, deben reinicializarse todas las suscripciones de cliente que reciben el artículo. No se tienen que reinicializar las suscripciones de servidor. Para obtener más información sobre los efectos de los cambios de propiedad, vea [Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especifique que un artículo es de solo descarga en la página **Artículos** del Asistente para nueva publicación o en la pestaña **Propiedades** del cuadro de diálogo **Propiedades del artículo: \<artículo>**. Dicho cuadro de diálogo está disponible en el Asistente para nueva publicación y en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>Para especificar que un artículo es de solo descarga en la página Artículos  
  
-   En la página **Artículos** del Asistente para nueva publicación, seleccione una tabla y, a continuación, active la casilla **La tabla resaltada es de solo descarga**.  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>Para especificar que un artículo es de solo descarga en la pestaña Propiedades del cuadro de diálogo Propiedades del artículo: \<artículo>  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione una tabla y luego haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de Tabla resaltado** o **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En la sección **Objeto de destino** de la pestaña **Propiedades** del cuadro de diálogo **Propiedades del artículo: \<artículo>**, especifique uno de los siguientes valores para **Dirección de la sincronización**:  
  
    -   **Solo descargar en suscriptor y prohibir cambios del suscriptor**  
  
    -   **Solo descargar en suscriptor y permitir cambios del suscriptor**  
  
4.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>Para especificar que un nuevo artículo de tabla de mezcla es de solo descarga  
  
1.  Ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especificando el valor **1** o **2** para el parámetro **@subscriber_upload_options**. Los números corresponden al comportamiento siguiente:  
  
    -   **0** - Ninguna restricción (valor predeterminado). Los cambios realizados en el suscriptor se cargan en el publicador.  
  
    -   **1** - Se permiten cambios en el suscriptor, pero no se cargan en el publicador.  
  
    -   **2** - No se permite realizar cambios en el suscriptor.  
  
        > [!NOTE]  
        >  Si la tabla de origen de un artículo ya está publicada en otra publicación, el valor de **@subscriber_upload_options** debe ser el mismo para ambos artículos.  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>Para cambiar un artículo de tabla de mezcla existente a solo descarga  
  
1.  Para determinar si un artículo es de solo descarga, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Tenga en cuenta el valor de **upload_options** para el artículo en el conjunto de resultados.  
  
2.  Si el valor devuelto en el paso 1 es **0**, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando el valor **subscriber_upload_options** para **@property**, un valor **1** para **@force_invalidate_snapshot** y **@force_reinit_subscription**y un valor **1** o **2** para **@value**, lo que corresponde al comportamiento siguiente:  
  
    -   **1** - Se permiten cambios en el suscriptor, pero no se cargan en el publicador.  
  
    -   **2** - No se permite realizar cambios en el suscriptor.  
  
        > [!NOTE]  
        >  Si la tabla de origen de un artículo ya está publicada en otra publicación, el comportamiento de solo descarga debe ser el mismo para ambos artículos.  
  
## <a name="see-also"></a>Vea también  
 [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [Ver y modificar las propiedades de un artículo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
