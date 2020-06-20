---
title: Inicializar una suscripción manualmente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4eaeb50da9e4b71a08ec78614ae62ea33e3dc0d1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066003"
---
# <a name="initialize-a-subscription-manually"></a>Inicializar una suscripción manualmente
  En este tema se describe cómo inicializar una suscripción manualmente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Aunque la instantánea inicial se usa normalmente para inicializar una suscripción, las suscripciones a las publicaciones se pueden inicializar sin utilizar una instantánea, con tal de que el esquema y los datos iniciales ya estén presentes en el suscriptor.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si se produce actividad en una base de datos publicada con la replicación transaccional entre el momento en que se copian los datos y el esquema en el suscriptor y el momento en que se inicializa manualmente la suscripción, es posible que los cambios que resulten de dicha actividad no se repliquen en el suscriptor.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Para inicializar manualmente una suscripción a una publicación copie el esquema (y, normalmente, los datos) en la base de datos de suscripciones. El esquema y los datos deben coincidir con la base de datos de publicaciones. A continuación, especifique que la suscripción no requiere esquema y datos en la página **Inicializar suscripciones** del Asistente para nuevas suscripciones. Para obtener más información sobre cómo utilizar este asistente, vea [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md) y [Create a Pull Subscription](create-a-pull-subscription.md).  
  
 Al sincronizar la suscripción por primera vez, los objetos y metadatos requeridos por la replicación se copian en la base de datos de suscripciones.  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>Para inicializar una suscripción a una publicación manualmente  
  
1.  Asegúrese de que el esquema y los datos están copiados en la base de datos de suscripciones.  
  
2.  Desactive la casilla **Inicializar** en la página **Inicializar suscripciones** del Asistente para nuevas suscripciones. Haga esto con cada suscripción que requiera solo copiar metadatos y objetos de replicación.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las suscripciones se pueden inicializar manualmente con los procedimientos almacenados de replicación.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>Para inicializar manualmente una suscripción de extracción a una publicación transaccional  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  En el publicador de la base de datos de publicaciones, ejecute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique **@publication** , **@subscriber** , el nombre de la base de datos en el suscriptor que contiene los datos publicados para **@destination_db** , un valor de **pull** para **@subscription_type** y un valor de **Replication support Only** para **@sync_type** . Para obtener más información, consulte [Create a Pull Subscription](create-a-pull-subscription.md).  
  
3.  En el suscriptor, ejecute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Para obtener más información acerca de las suscripciones de actualización, vea [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
4.  En el suscriptor, ejecute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Para obtener más información, consulte [Create a Pull Subscription](create-a-pull-subscription.md).  
  
5.  Inicie el Agente de distribución para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>Para inicializar manualmente una suscripción de inserción a una publicación transaccional  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  En el publicador de la base de datos de publicaciones, ejecute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique el nombre de la base de datos en el suscriptor que contiene los datos publicados para **@destination_db** , un valor de **inserte** para **@subscription_type** y un valor de **Replication support Only** para **@sync_type** . Para obtener más información acerca de las suscripciones de actualización, vea [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
3.  En el publicador de la base de datos de publicaciones, ejecute [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Para obtener más información, consulte [Create a Push Subscription](create-a-push-subscription.md).  
  
4.  Inicie el Agente de distribución para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>Para inicializar manualmente una suscripción de extracción a una publicación de combinación  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Esto se puede hacer restaurando una copia de seguridad de la base de datos de publicación en el suscriptor.  
  
2.  En el publicador, ejecute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Especifique **@publication** , **@subscriber** , **@subscriber_db** y un valor de **pull** para **@subscription_type** . Esto registra la suscripción de extracción.  
  
3.  En la base de datos del suscriptor que contiene los datos publicados, ejecute [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Especifique un valor de **none** para **@sync_type**.  
  
4.  En el suscriptor, ejecute [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Para obtener más información, consulte [Create a Pull Subscription](create-a-pull-subscription.md).  
  
5.  Inicie el Agente de mezcla para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>Para inicializar manualmente una suscripción de inserción a una publicación de combinación  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Esto se puede hacer restaurando una copia de seguridad de la base de datos de publicación en el suscriptor.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Especifique el nombre de la base de datos en el suscriptor que contiene los datos publicados para **@subscriber_db** , un valor de **inserte** para **@subscription_type** y un valor de **None** para **@sync_type** .  
  
3.  En el publicador de la base de datos de publicaciones, ejecute [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql). Para obtener más información, consulte [Create a Push Subscription](create-a-push-subscription.md).  
  
4.  Inicie el Agente de mezcla para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Consulte también  
 [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](administration/back-up-and-restore-replicated-databases.md)   
 [Procedimientos recomendados de seguridad de replicación](security/replication-security-best-practices.md)  
  
  
