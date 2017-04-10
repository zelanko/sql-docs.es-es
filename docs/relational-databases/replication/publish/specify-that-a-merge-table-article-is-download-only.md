---
title: "Especificar que un art&#237;culo de tabla de mezcla es de solo descarga | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación de mezcla [replicación de SQL Server], artículos de solo descarga"
  - "artículos [replicación de SQL Server], de sólo descarga"
  - "artículos de solo descarga"
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Especificar que un art&#237;culo de tabla de mezcla es de solo descarga
  En este tema se describe cómo especificar que un artículo de tabla de mezcla sea de solo descarga en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Los artículos de solo descarga están diseñados para aplicaciones con datos que no se actualizan en suscriptores. Para obtener más información, consulte [optimizar el rendimiento de replicación de mezcla con artículos de la sección](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para especificar que un artículo de tabla de mezcla sea de solo descarga con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si se especifica que un artículo es de solo descarga después de haber inicializado las suscripciones, deben reinicializarse todas las suscripciones de cliente que reciben el artículo. No se tienen que reinicializar las suscripciones de servidor. Para obtener más información sobre los efectos de los cambios de propiedad, vea [Propiedades de artículo y publicación de cambio](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especificar que un artículo es de solo descarga en el **artículos** página del Asistente para nueva publicación o **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo. Este cuadro de diálogo está disponible en el Asistente para nueva publicación y **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar que un artículo es de solo descarga en la página Artículos  
  
-   En el **artículos** página del nuevo Asistente de publicación, seleccione una tabla y, a continuación, seleccione la casilla de verificación **tabla resaltada es de sólo descarga**.  
  
#### Para especificar que un artículo es de sólo descarga en la ficha de propiedades de las propiedades del artículo: \< artículo> cuadro de diálogo  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de Tabla resaltado** o **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En el **el objeto de destino** sección de la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, especifique uno de los siguientes valores para **dirección de sincronización**:  
  
    -   **Solo descargar en suscriptor y prohibir cambios del suscriptor**  
  
    -   **Solo descargar en suscriptor y permitir cambios del suscriptor**  
  
4.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para especificar que un nuevo artículo de tabla de mezcla es de solo descarga  
  
1.  Ejecutar [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especificando un valor de **1** o **2** para el parámetro **@subscriber_upload_options**. Los números corresponden al comportamiento siguiente:  
  
    -   **0** -sin restricciones (valor predeterminado). Los cambios realizados en el suscriptor se cargan en el publicador.  
  
    -   **1** : se permiten cambios en el suscriptor, pero no se cargan en el publicador.  
  
    -   **2** -no se permiten cambios en el suscriptor.  
  
        > [!NOTE]  
        >  Si la tabla de origen para un artículo ya está publicada en otra publicación, el valor de **@subscriber_upload_options** debe ser el mismo para ambos artículos.  
  
#### Para cambiar un artículo de tabla de mezcla existente a solo descarga  
  
1.  Para determinar si un artículo es de sólo descarga, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Tenga en cuenta el valor de **upload_options** para el artículo en el resultado establecido.  
  
2.  Si el valor devuelto en el paso 1 es **0**, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando un valor de **subscriber_upload_options** para **@property**, un valor de **1** para **@force_invalidate_snapshot** y **@force_reinit_subscription**, y un valor de **1** o **2** para **@value**, que se corresponde con el siguiente comportamiento:  
  
    -   **1** : se permiten cambios en el suscriptor, pero no se cargan en el publicador.  
  
    -   **2** -no se permiten cambios en el suscriptor.  
  
        > [!NOTE]  
        >  Si la tabla de origen de un artículo ya está publicada en otra publicación, el comportamiento de solo descarga debe ser el mismo para ambos artículos.  
  
## Vea también  
 [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md)   
 [Ver y modificar las propiedades de un artículo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  