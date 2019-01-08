---
title: Especificar la resolución interactiva de conflictos para artículos de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 710db513395aa5a9c51df55b54bafbdc425ecb5d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749298"
---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>Especificar la resolución interactiva de conflictos para artículos de mezcla
  En este tema se describe cómo especificar la resolución interactiva de conflictos para los artículos de mezcla en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 La replicación de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona una Resolución interactiva que permite solucionar conflictos manualmente durante la sincronización a petición en el Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Una vez habilitada la resolución interactiva, resuelva los conflictos interactivamente durante la sincronización, mediante el Solucionador interactivo. El Solucionador interactivo está disponible a través del Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Para más información, vea [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Administrador de sincronización de Windows&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para especificar la resolución interactiva de conflictos para artículos de mezcla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si se realiza una sincronización fuera del Administrador de sincronización de Windows (como una sincronización programada o una sincronización a petición en SQL Server Management Studio o el Monitor de replicación), los conflictos se resuelven automáticamente sin la intervención del usuario, utilizando la resolución especificada para el artículo. Para obtener más información, consulte [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>Para habilitar la resolución interactiva de conflictos para un artículo  
  
1.  En la página **Artículos** del Asistente para nueva publicación o en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione una tabla. Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Create a Publication](create-a-publication.md) (Crear una publicación) y [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado** o en **Establecer propiedades de todos los artículos de la tabla**.  
  
3.  En la página **Propiedades del artículo - \<Artículo>** o **Propiedades del artículo - \<ArticleType>** , haga clic en la pestaña **Resolución**.  
  
4.  Seleccione **Permitir que el suscriptor resuelva los conflictos de modo interactivo durante la sincronización a petición**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Si se encuentra en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>Para especificar que una suscripción debe utilizar la resolución interactiva de conflictos  
  
1.  En el **propiedades de suscripción - \<suscriptor >: \<Basededatosdesuscripción >** diálogo cuadro, especifique un valor de **True** para el **resuelva los conflictos interactivamente** opción. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md).  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede especificar mediante programación que el suscriptor utilizará esta interfaz gráfica para solucionar conflictos de artículos cuando se cree una suscripción de extracción a una publicación de combinación. Solo se mostrarán en el Solucionador interactivo los conflictos de artículos que admitan esta opción.  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>Para crear una suscripción de extracción de mezcla que utilice el Solucionador interactivo  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), especificando **@publication**. Tenga en cuenta el valor de **allow_interactive_resolver** para cada artículo del conjunto de resultados para el que se utilizará el Solucionador interactivo.  
  
    -   Si este valor es **1**, se utilizará el Solucionador interactivo.  
  
    -   Si este valor es **0**, debe habilitar primero el Solucionador interactivo para cada artículo. Para ello, ejecute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, el valor **allow_interactive_resolver** para **@property**y el valor **true** para **@value**.  
  
2.  En la base de datos de suscripciones del suscriptor, ejecute [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Para obtener más información, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
3.  En la base de datos de suscripciones del suscriptor, ejecute [sp_addmergesubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)y especifique los siguientes parámetros:  
  
    -   **@publisher**, **@publisher_db** (la base de datos publicada) y **@publication**.  
  
    -   El valor **true** para **@enabled_for_syncmgr**.  
  
    -   El valor **true** para **@use_interactive_resolver**.  
  
    -   La información de la cuenta de seguridad que necesita el Agente de mezcla. Para más información, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
4.  En la base de datos de publicación del publicador, ejecute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql).  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>Para definir un artículo que admita el Solucionador interactivo  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se está publicando para **@source_object**y el valor **true** para **@allow_interactive_resolver**. Para más información, consulte [Define an Article](define-an-article.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](../view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
