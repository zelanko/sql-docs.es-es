---
title: "Cambiar entre modos de actualizaci&#243;n para una suscripci&#243;n transaccional actualizable | Microsoft Docs"
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
  - "replicación transaccional, suscripciones actualizables"
  - "suscripciones actualizables, modos de actualización"
  - "suscripciones [replicación de SQL Server], actualizables"
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Cambiar entre modos de actualizaci&#243;n para una suscripci&#243;n transaccional actualizable
  En este tema se describe cómo cambiar entre modos en actualización para una suscripción de transacción actualizable en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Especifique el modo que desea utilizar para las suscripciones actualizables con el Asistente para nuevas suscripciones. Para obtener información acerca de cómo establecer el modo cuando se utiliza este asistente, consulte [Ver y modificar propiedades de suscripción de extracción](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
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
  
-   Cuando una suscripción de actualización a una publicación transaccional admite la conmutación por error de un modo de actualización a otro, se puede cambiar entre modos de actualización mediante programación para controlar las situaciones en que la conectividad cambia durante un breve período de tiempo. Se puede establecer el modo de actualización mediante programación y a petición con procedimientos almacenados de replicación. Para más información, consulte [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
> [!NOTE]  
>  Para cambiar el modo de actualización después de crea la suscripción, el **update_mode** propiedad debe establecerse en **conmutación por error** (que permite cambiar de actualización inmediata a actualización en cola) o **en cola la conmutación por error** (que permite cambiar de la actualización en cola a la actualización inmediata) cuando se crea la suscripción. Estas propiedades se establecen automáticamente en el Asistente para nuevas suscripciones.  
  
#### Para establecer el modo de actualización para una suscripción de inserción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Suscripciones locales** .  
  
3.  Haga clic en la suscripción para la que desea establecer el modo de actualización y, a continuación, haga clic en **establecer método de actualización**.  
  
4.  En el **establecer método de actualización - \< suscriptor>: \< Basededatosdesuscripciones>** cuadro de diálogo, seleccione **la actualización inmediata** o **actualización en cola**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para establecer el modo de actualización para una suscripción de extracción  
  
1.  En la **Propiedades de suscripción - \< publicador>: \< Basededatosdepublicaciones>** cuadro de diálogo, seleccione el valor **replicar cambios inmediatamente** o **poner en cola cambios** para el **método de actualización del suscriptor** opción.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Para obtener más información acerca del acceso a la **Propiedades de suscripción - \< publicador>: \< Basededatosdepublicaciones>** cuadro de diálogo, vea [Ver y modificar propiedades de suscripción de extracción](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para cambiar entre modos de actualización  
  
1.  Compruebe que la suscripción admite la conmutación por error ejecutando [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) para una suscripción de extracción o [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) para una suscripción de inserción. Si el valor del **modo de la actualización** en el conjunto de resultados es **3** o **4**, se admite la conmutación por error.  
  
2.  En el suscriptor en la base de datos de suscripción, ejecute [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, y uno de los siguientes valores para **@failover_mode**:  
  
    -   **en la cola** -conmutar por error a actualización en cola cuando se pierde temporalmente conectividad.  
  
    -   **inmediata** -conmutar por error a actualización inmediata cuando se ha restaurado la conectividad.  
  
## Vea también  
 [Suscripciones actualizables para replicación transaccional](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  