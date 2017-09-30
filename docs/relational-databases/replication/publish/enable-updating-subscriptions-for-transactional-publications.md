---
title: Habilitar suscripciones actualizables para publicaciones transaccionales | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: e989a795ff6179bdab183a2c7814f099b0448f38
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>Habilitar suscripciones actualizables para publicaciones transaccionales
  En este tema se describe cómo habilitar suscripciones de actualización para publicaciones transaccionales en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> **NOTA** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Habilite suscripciones de actualización para publicaciones transaccionales en la página **Tipo de publicación** del Asistente para nueva publicación.  
  
 Para utilizar suscripciones de actualización, debe configurar también opciones en el Asistente para nuevas suscripciones.  
  
#### <a name="to-enable-updating-subscriptions"></a>Para habilitar las suscripciones de actualización  
  
1.  En la página **Tipo de publicación** del Asistente para nueva publicación, seleccione **Publicación transaccional con suscripciones actualizables**.  
  
2.  En la página **Seguridad del agente** , especifique la configuración de seguridad para el Agente de lectura de cola, el Agente de instantáneas y el Agente de registro del LOG. Para obtener más información acerca de los permisos necesarios para la cuenta con la que se ejecuta el Agente de lectura de cola, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    > **NOTA**: El Agente de lectura de cola se configura aunque solamente se usen suscripciones de actualización inmediata.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Al crear una publicación transaccional mediante programación con procedimientos almacenados de replicación, puede habilitar las suscripciones de actualización inmediatas o en cola.  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>Para crear una publicación que admita suscripciones de actualización inmediatas  
  
1.  Si es necesario, cree un trabajo del Agente de registro del LOG para la base de datos de publicación.  
  
    -   Si ya existe un trabajo de Agente de registro del LOG para la base de datos de publicación, continúe al paso 2.  
  
    -   Si no está seguro de que exista un Agente de registro del LOG para una base de datos publicada, ejecute [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) en la base de datos de publicación del publicador. Si el conjunto de resultados está vacío, es necesario crear un trabajo del Agente de registro del LOG.  
  
    -   En el publicador, ejecute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique las credenciales de Windows de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] con las que se ejecuta el agente para **@job_name** y **@password**. Si el agente va a usar la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**.  
  
2.  Ejecute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) y especifique un valor de **true** para el parámetro **@allow_sync_tran**.  
  
3.  En el publicador, ejecute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique el nombre de publicación usado en el paso 2 para **@publication** y las credenciales de Windows con las que se ejecuta el Agente de instantáneas para **@job_name** y **@password**. Si el agente va a usar la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
4.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  En el Suscriptor, cree una suscripción de actualización a esta publicación.   
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>Para crear una publicación que admita suscripciones de actualización en cola  
  
1.  Si es necesario, cree un trabajo del Agente de registro del LOG para la base de datos de publicación.  
  
    -   Si ya existe un trabajo de Agente de registro del LOG para la base de datos de publicación, continúe al paso 2.  
  
    -   Si no está seguro de que exista un Agente de registro del LOG para una base de datos publicada, ejecute [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) en la base de datos de publicación del publicador. Si el conjunto de resultados está vacío, es necesario crear un trabajo de Agente de registro del LOG.  
  
    -   En el publicador, ejecute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique las credenciales de Windows con las que se ejecuta el agente para **@job_name** y **@password**. Si el agente va a usar la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**.  
  
2.  Si es necesario, cree un trabajo del Agente de lectura de cola para el Distribuidor.  
  
    -   Si ya existe un trabajo del Agente de lectura de cola para la base de datos de distribución, continúe con el paso 3.  
  
    -   Si no está seguro de si existe un trabajo del Agente de lectura de cola para la base de datos de distribución, ejecute [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) en el distribuidor de la base de datos de distribución. Si el conjunto de resultados está vacío, se debe crear un trabajo del Agente de lectura de cola.  
  
    -   En el distribuidor, ejecute [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Especifique las credenciales de Windows con las que se ejecuta el agente para **@job_name** y **@password**. Se usan estas credenciales cuando el Agente de lectura de cola conecta con el Publicador y el Suscriptor. Para obtener más información, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  Ejecute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) y especifique un valor de **true** para el parámetro **@allow_queued_tran** y un valor de **pub wins**, **sub reinit** o **sub wins** para **@conflict_policy**.  
  
4.  En el publicador, ejecute [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique el nombre de publicación usado en el paso 3 para **@publication** y las credenciales de Windows con las que se ejecuta el Agente de instantáneas para **@snapshot_job_name** y **@password**. Si el agente va a usar la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
5.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  En el Suscriptor, cree una suscripción de actualización a esta publicación.  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>Para cambiar la directiva de conflicto para una publicación que permita las suscripciones de actualización en cola  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique un valor de **conflict_policy** para **@property** y el modo de directiva de conflicto deseado de **pub wins**, **sub reinit**o **sub wins** para **@value**.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 Este ejemplo crea una publicación que admitía las suscripciones de extracción de actualizaciones inmediatas y en cola.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## <a name="see-also"></a>Vea también  
 [Establecer opciones de resolución de conflictos de actualización en cola &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)   
 [Tipos de publicaciones para la replicación transaccional](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Crear una suscripción actualizable en una publicación transaccional](create-updatable-subscription-to-transactional-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Usar sqlcmd con variables de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
