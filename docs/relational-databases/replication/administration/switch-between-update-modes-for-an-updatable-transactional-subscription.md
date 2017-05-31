---
title: "Cambiar entre modos de actualización para una suscripción transaccional actualizable | Microsoft Docs"
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
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 271b9ff4060284d50e66130f8bbd4b8d5b288912
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>Cambiar entre modos de actualización para una suscripción transaccional actualizable
  En este tema se describe cómo cambiar entre modos en actualización para una suscripción de transacción actualizable en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Especifique el modo que desea utilizar para las suscripciones actualizables con el Asistente para nuevas suscripciones. Para información sobre cómo establecer el modo cuando se utiliza este asistente, vea [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md) (Ver y modificar las propiedades de una suscripción de extracción).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para cambiar entre modos de actualización para una suscripción transaccional actualizable con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Puede conmutar por error desde actualización inmediata a actualización en cola en cualquier momento. No obstante, una vez hecho esto, no se puede volver a actualización inmediata hasta que el suscriptor y el publicador estén conectados y el Agente de lectura de cola haya aplicado todos los mensajes pendientes en la cola al publicador.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Cuando una suscripción de actualización a una publicación transaccional admite la conmutación por error de un modo de actualización a otro, se puede cambiar entre modos de actualización mediante programación para controlar las situaciones en que la conectividad cambia durante un breve período de tiempo. Se puede establecer el modo de actualización mediante programación y a petición con procedimientos almacenados de replicación. Para más información, vea [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
> [!NOTE]  
>  Para cambiar el modo de actualización después de crear la suscripción, debe establecer la propiedad **update_mode** en **failover** (que permite cambiar de la actualización inmediata a la actualización en cola) o **queued failover** (que permite cambiar de la actualización en cola a la actualización inmediata) al crear la suscripción. Estas propiedades se establecen automáticamente en el Asistente para nuevas suscripciones.  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>Para establecer el modo de actualización para una suscripción de inserción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Suscripciones locales** .  
  
3.  Haga clic con el botón secundario en la suscripción para la que desea establecer el modo de actualización y, a continuación, haga clic en **Establecer método de actualización**.  
  
4.  En el cuadro de diálogo **Establecer método de actualización - \<suscriptor>: \<baseBatosDeSuscripción>**, seleccione **Actualización inmediata** o **Actualización en cola**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>Para establecer el modo de actualización para una suscripción de extracción  
  
1.  En el cuadro de diálogo **Propiedades de suscripción - \<Publicador>: \<baseBatosDeSuscripción>**, seleccione el valor **Replicar cambios inmediatamente** o **Poner en cola cambios** para la opción **Método de actualización del suscriptor**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Para más información sobre el acceso al cuadro de diálogo **Propiedades de la suscripción: \<publicador>: \<baseDatosPublicación**, vea [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md) (Ver y modificar las propiedades de una suscripción de extracción).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-switch-between-update-modes"></a>Para cambiar entre modos de actualización  
  
1.  Compruebe que la suscripción admite la conmutación por error ejecutando [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) para una suscripción de extracción o [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) para una suscripción de inserción. Si el valor del **modo de la actualización** en el conjunto de resultados es **3** o **4**, se admite la conmutación por error.  
  
2.  En el publicador de la base de datos de suscripciones, ejecute [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**y uno de los valores siguientes para **@failover_mode**:  
  
    -   **queued** : conmutación por error a actualización en cola cuando se ha perdido la conectividad temporalmente.  
  
    -   **immediate** : conmutación por error a actualización inmediata cuando se ha restaurado la conectividad.  
  
## <a name="see-also"></a>Vea también  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
