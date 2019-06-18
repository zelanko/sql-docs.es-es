---
title: Establecer el período de expiración para las suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], expiration
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- deactivating subscriptions
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7edca09192abc207ef4879c8d8275777451d51a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649235"
---
# <a name="set-the-expiration-period-for-subscriptions"></a>Establecer el período de expiración para las suscripciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo establecer el período de expiración para las suscripciones en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El período de expiración de las suscripciones determina el tiempo que debe transcurrir antes de que una suscripción expire y se quite. Para más información, consulte [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para establecer el período de expiración para las suscripciones con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   El período de expiración de las suscripciones recibe también el nombre de *período de retención de la publicación*. La limpieza de los metadatos de replicación de mezcla depende de este valor:  
  
    -   La replicación no puede limpiar metadatos en las bases de datos de suscripciones y publicaciones hasta que se haya alcanzado el período de retención. Tenga cuidado al especificar un valor elevado para el período de retención, ya que puede afectar negativamente al rendimiento de la replicación. Se recomienda utilizar un valor bajo si puede prever con exactitud que todos los suscriptores se sincronizarán con regularidad dentro del período establecido.  
  
         El período de retención de las publicaciones de combinación tiene un período de gracia de 24 horas para incluir a los suscriptores en diferentes zonas horarias. Si, por ejemplo, se establece un período de retención de un día, el período de retención real será de 48 horas.  
  
    -   Es posible especificar que las suscripciones no expiren nunca, pero se recomienda encarecidamente no utilizar ese valor, ya que los metadatos no se podrían limpiar.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Establezca el período de expiración de las suscripciones en la página **General** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>Para establecer el período de expiración para las suscripciones  
  
1.  En la sección **Expiración de la suscripción** de la página **General** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , especifique si las suscripciones deben caducar.  
  
2.  Si deben expirar, especifique un período de expiración.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede utilizar los procedimientos almacenados de replicación para establecer este valor cuando se crea una publicación o para modificar este valor en un momento posterior.  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para establecer el período de expiración de una suscripción en una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique el período de expiración deseado para la suscripción, en horas, para **@retention** . El período de expiración predeterminado es 336 horas. Para obtener más información, vea [Crear una suscripción](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para establecer el período de expiración de una suscripción en una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique el valor deseado para el período de expiración de la suscripción en **@retention** . Especifique las unidades en las que se expresa el período de expiración para **@retention_period_unit** , que pueden ser unas de las siguientes:  
  
    -   **1** = semana  
  
    -   **2** = mes  
  
    -   **3** = año  
  
     El período de expiración predeterminado es 14 días. Para más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para cambiar el período de expiración de una suscripción a una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique **retención** para **@property** y el nuevo período de expiración de suscripción, en horas, para **@value** .  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para cambiar el período de expiración de una suscripción a una publicación de combinación  
  
1.  En el publicador, ejecute [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando **@publication** y **@publisher** . Tenga en cuenta el valor de **retention_period_unit** en el conjunto de resultados, que puede ser uno de los siguientes:  
  
    -   **0** = día  
  
    -   **1** = semana  
  
    -   **2** = mes  
  
    -   **3** = año  
  
2.  En el publicador, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique **retención** para **@property** y el nuevo período de expiración de suscripción, como texto basado en la unidad de período de retención del paso 1, para **@value** .  
  
3.  (Opcional) En el publicador, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique **retention_period_unit** para **@property** y una nueva unidad para el período de expiración de la suscripción en **@value** .  
  
## <a name="see-also"></a>Consulte también  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
