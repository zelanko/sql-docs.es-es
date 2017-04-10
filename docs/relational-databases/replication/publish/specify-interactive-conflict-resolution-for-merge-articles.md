---
title: "Especificar la resoluci&#243;n interactiva de conflictos para art&#237;culos de mezcla | Microsoft Docs"
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
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], solucionador interactivo"
  - "resolución interactiva de conflictos [replicación de SQL Server]"
  - "artículos [replicación de SQL Server], resolución de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Especificar la resoluci&#243;n interactiva de conflictos para art&#237;culos de mezcla
  En este tema se describe cómo especificar la resolución interactiva de conflictos para los artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la replicación proporciona una resolución interactiva, que permite resolver conflictos manualmente durante la sincronización a petición en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Administrador de sincronización de Windows. Una vez habilitada la resolución interactiva, resuelva los conflictos interactivamente durante la sincronización, mediante el Solucionador interactivo. El Solucionador interactivo está disponible a través del Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Para obtener más información, consulte [sincronizar una suscripción utilizando Windows Synchronization Manager & #40; Administrador de sincronización de Windows & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para especificar la resolución interactiva de conflictos para artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si se realiza una sincronización fuera del Administrador de sincronización de Windows (como una sincronización programada o una sincronización a petición en SQL Server Management Studio o el Monitor de replicación), los conflictos se resuelven automáticamente sin la intervención del usuario, utilizando la resolución especificada para el artículo. Para obtener más información, consulte [Interactive Conflict Resolution](../../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para habilitar la resolución interactiva de conflictos para un artículo  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado** o en **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En la **Propiedades del artículo: \< artículo>** o **Propiedades del artículo: \< ArticleType>** haga clic en el **resolución** ficha.  
  
4.  Seleccione **Permitir que el suscriptor resuelva los conflictos interactivamente durante la sincronización a petición**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### Para especificar que una suscripción debe utilizar la resolución interactiva de conflictos  
  
1.  En la **Propiedades de suscripción - \< suscriptor>: \< Basededatosdesuscripciones>** cuadro de diálogo, especifique un valor de **True** para el **resolver conflictos de manera interactiva** opción. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede especificar mediante programación que el suscriptor utilizará esta interfaz gráfica para solucionar conflictos de artículos cuando se cree una suscripción de extracción a una publicación de combinación. Solo se mostrarán en el Solucionador interactivo los conflictos de artículos que admitan esta opción.  
  
#### Para crear una suscripción de extracción de mezcla que utilice el Solucionador interactivo  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication**. Tenga en cuenta el valor de **allow_interactive_resolver** para cada artículo en el conjunto de resultados para que se utilizará la resolución interactiva.  
  
    -   Si este valor es **1**, se utilizará el Solucionador interactivo.  
  
    -   Si este valor es **0**, debe habilitar primero el Solucionador interactivo para cada artículo. Para ello, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, un valor de **allow_interactive_resolver** para **@property**, y un valor de **true** para **@value**.  
  
2.  En el suscriptor en la base de datos de suscripción, ejecute [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Para más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  En el suscriptor en la base de datos de suscripción, ejecute [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), especifique los siguientes parámetros:  
  
    -   **@publisher**, **@publisher_db** (la base de datos publicada), y **@publication**.  
  
    -   Un valor de **true** para **@enabled_for_syncmgr**.  
  
    -   Un valor de **true** para **@use_interactive_resolver**.  
  
    -   La información de la cuenta de seguridad que necesita el Agente de mezcla. Para más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
4.  En el publicador de la base de datos de publicación, ejecute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md).  
  
#### Para definir un artículo que admita el Solucionador interactivo  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, y un valor de **true** para **@allow_interactive_resolver**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Vea también  
 [Ver y resolver conflictos de datos de publicaciones de mezcla & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [Resolución interactiva de conflictos](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  