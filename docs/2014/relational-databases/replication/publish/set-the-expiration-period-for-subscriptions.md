---
title: Establecer el período de expiración para las suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 663de184c811291c4b583ddbaf2fb6862097c54f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882180"
---
# <a name="set-the-expiration-period-for-subscriptions"></a>Establecer el período de expiración para las suscripciones
  En este tema se describe cómo establecer el período de expiración para las suscripciones en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El período de expiración de las suscripciones determina el tiempo que debe transcurrir antes de que una suscripción expire y se quite. Para más información, consulte [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para establecer el período de expiración para las suscripciones con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
  
-   El período de expiración de las suscripciones recibe también el nombre de *período de retención de la publicación*. La limpieza de los metadatos de replicación de mezcla depende de este valor:  
  
    -   La replicación no puede limpiar metadatos en las bases de datos de suscripciones y publicaciones hasta que se haya alcanzado el período de retención. Tenga cuidado al especificar un valor elevado para el período de retención, ya que puede afectar negativamente al rendimiento de la replicación. Se recomienda utilizar un valor bajo si puede prever con exactitud que todos los suscriptores se sincronizarán con regularidad dentro del período establecido.  
  
         El período de retención de las publicaciones de combinación tiene un período de gracia de 24 horas para incluir a los suscriptores en diferentes zonas horarias. Si, por ejemplo, se establece un período de retención de un día, el período de retención real será de 48 horas.  
  
    -   Es posible especificar que las suscripciones no expiren nunca, pero se recomienda encarecidamente no utilizar ese valor, ya que los metadatos no se podrían limpiar.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Establezca el período de expiración de las suscripciones en la página **General** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>Para establecer el período de expiración para las suscripciones  
  
1.  En la sección **Expiración de la suscripción** de la página **General** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , especifique si las suscripciones deben caducar.  
  
2.  Si deben expirar, especifique un período de expiración.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede utilizar los procedimientos almacenados de replicación para establecer este valor cuando se crea una publicación o para modificar este valor en un momento posterior.  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para establecer el período de expiración de una suscripción en una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique el período de expiración deseado para la suscripción, en horas, para **\@retention**. El período de expiración predeterminado es 336 horas. Para obtener más información, vea [Crear una suscripción](create-a-publication.md).  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para establecer el período de expiración de una suscripción en una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique el valor deseado para el período de expiración de la suscripción en **\@retention**. Especifique las unidades en las que se expresa el período de expiración para **\@retention_period_unit**, que pueden ser unas de las siguientes:  
  
    -   **1** = semana  
  
    -   **2** = mes  
  
    -   **3** = año  
  
     El período de expiración predeterminado es 14 días. Para obtener más información, vea [Crear una suscripción](create-a-publication.md).  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para cambiar el período de expiración de una suscripción a una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique **retention** para **\@property** y el nuevo período de expiración de suscripción, en horas, para **\@value**.  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para cambiar el período de expiración de una suscripción a una publicación de combinación  
  
1.  En el publicador, ejecute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), y especifique **\@publication** y **\@publisher**. Tenga en cuenta el valor de **retention_period_unit** en el conjunto de resultados, que puede ser uno de los siguientes:  
  
    -   **0** = día  
  
    -   **1** = semana  
  
    -   **2** = mes  
  
    -   **3** = año  
  
2.  En el publicador, ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique **retention** para **\@property** y el nuevo período de expiración de suscripción, como texto en función de la unidad de período de retención del paso 1, para **\@value**.  
  
3.  (Opcional) En el publicador, ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique **retention_period_unit** para **\@property** y una nueva unidad para el período de expiración de la suscripción para **\@value**.  
  
## <a name="see-also"></a>Consulte también  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Desactivación y expiración de la suscripción](../subscription-expiration-and-deactivation.md)  
  
  
