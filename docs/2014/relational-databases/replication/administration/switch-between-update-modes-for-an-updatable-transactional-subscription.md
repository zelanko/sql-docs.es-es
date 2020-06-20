---
title: Cambiar entre modos de actualización para una suscripción transaccional actualizable | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c31814d1e2ab6fac64ffcde883f3cac2439828a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055733"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>Cambiar entre modos de actualización para una suscripción transaccional actualizable
  En este tema se describe cómo cambiar entre modos en actualización para una suscripción de transacción actualizable en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Especifique el modo que desea utilizar para las suscripciones actualizables con el Asistente para nuevas suscripciones. Para información sobre cómo establecer el modo cuando se utiliza este asistente, vea [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md) (Ver y modificar las propiedades de una suscripción de extracción).  
  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Puede conmutar por error desde actualización inmediata a actualización en cola en cualquier momento. No obstante, una vez hecho esto, no se puede volver a actualización inmediata hasta que el suscriptor y el publicador estén conectados y el Agente de lectura de cola haya aplicado todos los mensajes pendientes en la cola al publicador.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
  
-   Cuando una suscripción de actualización a una publicación transaccional admite la conmutación por error de un modo de actualización a otro, se puede cambiar entre modos de actualización mediante programación para controlar las situaciones en que la conectividad cambia durante un breve período de tiempo. Se puede establecer el modo de actualización mediante programación y a petición con procedimientos almacenados de replicación. Para más información, consulte [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
> [!NOTE]  
>  Para cambiar el modo de actualización después de crear la suscripción, debe establecer la propiedad **update_mode** en **failover** (que permite cambiar de la actualización inmediata a la actualización en cola) o **queued failover** (que permite cambiar de la actualización en cola a la actualización inmediata) al crear la suscripción. Estas propiedades se establecen automáticamente en el Asistente para nuevas suscripciones.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>Para establecer el modo de actualización para una suscripción de inserción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, la carpeta **Suscripciones locales**.  
  
3.  Haga clic con el botón secundario en la suscripción para la que desea establecer el modo de actualización y, a continuación, haga clic en **Establecer método de actualización**.  
  
4.  En el cuadro de diálogo **establecer método de actualización- \<Subscriber> : \<SubscriptionDatabase> ** , seleccione actualización **inmediata** o **actualización en cola**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>Para establecer el modo de actualización para una suscripción de extracción  
  
1.  En el cuadro de diálogo **propiedades de suscripción- \<Publisher> \<PublicationDatabase> :** , seleccione el valor **replicar cambios inmediatamente** o **poner en cola los cambios** para la opción **método de actualización del suscriptor** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Para obtener más información sobre el acceso al cuadro **de diálogo Propiedades de suscripción- \<Publisher> \<PublicationDatabase> :** , vea [ver y modificar propiedades de suscripción de extracción](../view-and-modify-pull-subscription-properties.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>Para cambiar entre modos de actualización  
  
1.  Compruebe que la suscripción admite la conmutación por error ejecutando [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql) para una suscripción de extracción o [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) para una suscripción de inserción. Si el valor del **modo de la actualización** en el conjunto de resultados es **3** o **4**, se admite la conmutación por error.  
  
2.  En el publicador de la base de datos de suscripciones, ejecute [sp_setreplfailovermode](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql). Especifique **@publisher** , **@publisher_db** , **@publication** y uno de los siguientes valores para **@failover_mode** :  
  
    -   **queued** : conmutación por error a actualización en cola cuando se ha perdido la conectividad temporalmente.  
  
    -   **immediate** : conmutación por error a actualización inmediata cuando se ha restaurado la conectividad.  
  
## <a name="see-also"></a>Consulte también  
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
