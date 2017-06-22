---
title: "Especificar la resolución interactiva de conflictos para artículos de mezcla | Microsoft Docs"
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
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d488371a34cefb0ecf73824e362137243c115926
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>Especificar la resolución interactiva de conflictos para artículos de mezcla
  En este tema se describe cómo especificar la resolución interactiva de conflictos para los artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 La replicación de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona una Resolución interactiva que permite solucionar conflictos manualmente durante la sincronización a petición en el Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Una vez habilitada la resolución interactiva, resuelva los conflictos interactivamente durante la sincronización, mediante el Solucionador interactivo. El Solucionador interactivo está disponible a través del Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Para más información, vea [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Administrador de sincronización de Windows&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para especificar la resolución interactiva de conflictos para artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si se realiza una sincronización fuera del Administrador de sincronización de Windows (como una sincronización programada o una sincronización a petición en SQL Server Management Studio o el Monitor de replicación), los conflictos se resuelven automáticamente sin la intervención del usuario, utilizando la resolución especificada para el artículo. Para obtener más información, consulte [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>Para habilitar la resolución interactiva de conflictos para un artículo  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione una tabla. Para más información sobre el uso del asistente y el acceso al cuadro de diálogo, vea [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado** o en **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En la página **Propiedades del artículo - \<Artículo>** o **Propiedades del artículo - \<ArticleType>** , haga clic en la pestaña **Resolución**.  
  
4.  Seleccione **Permitir que el suscriptor resuelva los conflictos de modo interactivo durante la sincronización a petición**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>Para especificar que una suscripción debe utilizar la resolución interactiva de conflictos  
  
1.  En el cuadro de diálogo **Propiedades de la suscripción - \<Suscriptor>: \<baseDeDatosDeSuscripción>**, especifique el valor **True** para la opción **Solucionar conflictos de manera interactiva**. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede especificar mediante programación que el suscriptor utilizará esta interfaz gráfica para solucionar conflictos de artículos cuando se cree una suscripción de extracción a una publicación de combinación. Solo se mostrarán en el Solucionador interactivo los conflictos de artículos que admitan esta opción.  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>Para crear una suscripción de extracción de mezcla que utilice el Solucionador interactivo  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication**. Tenga en cuenta el valor de **allow_interactive_resolver** para cada artículo del conjunto de resultados para el que se utilizará el Solucionador interactivo.  
  
    -   Si este valor es **1**, se utilizará el Solucionador interactivo.  
  
    -   Si este valor es **0**, debe habilitar primero el Solucionador interactivo para cada artículo. Para ello, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, el valor **allow_interactive_resolver** para **@property**y el valor **true** para **@value**.  
  
2.  En la base de datos de suscripciones del suscriptor, ejecute [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Para más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  En la base de datos de suscripciones del suscriptor, ejecute [sp_addmergesubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)y especifique los siguientes parámetros:  
  
    -   **@publisher**, **@publisher_db** (la base de datos publicada) y **@publication**.  
  
    -   El valor **true** para **@enabled_for_syncmgr**.  
  
    -   El valor **true** para **@use_interactive_resolver**.  
  
    -   La información de la cuenta de seguridad que necesita el Agente de mezcla. Para más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
4.  En la base de datos de publicación del publicador, ejecute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md).  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>Para definir un artículo que admita el Solucionador interactivo  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se está publicando para **@source_object**y el valor **true** para **@allow_interactive_resolver**. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
