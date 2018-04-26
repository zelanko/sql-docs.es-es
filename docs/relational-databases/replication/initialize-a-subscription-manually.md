---
title: Inicializar una suscripción manualmente | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 78107a993daa7e7b98cecb850b54369295a34040
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="initialize-a-subscription-manually"></a>Inicializar una suscripción manualmente
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describe cómo inicializar una suscripción manualmente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Aunque la instantánea inicial se usa normalmente para inicializar una suscripción, las suscripciones a las publicaciones se pueden inicializar sin utilizar una instantánea, con tal de que el esquema y los datos iniciales ya estén presentes en el suscriptor.  
  

##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si se produce actividad en una base de datos publicada con la replicación transaccional entre el momento en que se copian los datos y el esquema en el suscriptor y el momento en que se inicializa manualmente la suscripción, es posible que los cambios que resulten de dicha actividad no se repliquen en el suscriptor.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Para inicializar manualmente una suscripción a una publicación copie el esquema (y, normalmente, los datos) en la base de datos de suscripciones. El esquema y los datos deben coincidir con la base de datos de publicaciones. A continuación, especifique que la suscripción no requiere esquema y datos en la página **Inicializar suscripciones** del Asistente para nuevas suscripciones. Para obtener más información sobre cómo utilizar este asistente, vea [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) y [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Al sincronizar la suscripción por primera vez, los objetos y metadatos requeridos por la replicación se copian en la base de datos de suscripciones.  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>Para inicializar una suscripción a una publicación manualmente  
  
1.  Asegúrese de que el esquema y los datos están copiados en la base de datos de suscripciones.  
  
2.  Desactive la casilla **Inicializar** en la página **Inicializar suscripciones** del Asistente para nuevas suscripciones. Haga esto con cada suscripción que requiera solo copiar metadatos y objetos de replicación.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las suscripciones se pueden inicializar manualmente con los procedimientos almacenados de replicación.  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>Para inicializar manualmente una suscripción de extracción a una publicación transaccional  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  En el publicador de la base de datos de publicaciones, ejecute [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, el nombre de la base de datos del suscriptor que contiene los datos publicados para **@destination_db**, un valor de **pull** para **@subscription_type**y un valor de **replication support only** para **@sync_type**. Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
3.  En el suscriptor, ejecute [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Para obtener más información acerca de las suscripciones de actualización, vea [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
4.  En el suscriptor, ejecute [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Inicie el Agente de distribución para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>Para inicializar manualmente una suscripción de inserción a una publicación transaccional  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
2.  En el publicador de la base de datos de publicaciones, ejecute [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique el nombre de la base de datos del suscriptor que contiene los datos publicados para **@destination_db**, un valor de **push** para **@subscription_type**y un valor de **replication support only** para **@sync_type**. Para obtener más información acerca de las suscripciones de actualización, vea [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx).  
  
3.  En el publicador de la base de datos de publicaciones, ejecute [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Para obtener más información, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Inicie el Agente de distribución para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>Para inicializar manualmente una suscripción de extracción a una publicación de combinación  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Esto se puede hacer restaurando una copia de seguridad de la base de datos de publicación en el suscriptor.  
  
2.  En el publicador, ejecute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, **@subscriber_db**y un valor de **pull** para **@subscription_type**. Esto registra la suscripción de extracción.  
  
3.  En la base de datos del suscriptor que contiene los datos publicados, ejecute [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Especifique un valor de **none** para **@sync_type**.  
  
4.  En el suscriptor, ejecute [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
5.  Inicie el Agente de mezcla para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>Para inicializar manualmente una suscripción de inserción a una publicación de combinación  
  
1.  Asegúrese de que el esquema y los datos existen en la base de datos de suscripciones. Esto se puede hacer restaurando una copia de seguridad de la base de datos de publicación en el suscriptor.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Especifique el nombre de la base de datos del suscriptor que contiene los datos publicados para **@subscriber_db**, un valor de **push** para **@subscription_type**y un valor de **none** para **@sync_type**.  
  
3.  En el publicador de la base de datos de publicaciones, ejecute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Para obtener más información, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
4.  Inicie el Agente de mezcla para transferir los objetos de replicación y descargue los cambios más recientes del publicador. Para obtener más información, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Ver también  
 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
