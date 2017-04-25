---
title: "Desactivación y expiración de las suscripciones| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 628f62dd5c3d28c42128d7a21285208065c6ddbc
ms.lasthandoff: 04/11/2017

---
# <a name="subscription-expiration-and-deactivation"></a>Desactivación y expiración de las suscripciones
  Las suscripciones se pueden desactivar o pueden expirar si no se sincronizan en un *período de retención*especificado. La acción que se produce depende del tipo de replicación y del período de retención que se supere.  
  
 Para establecer períodos de retención, vea [Establecer el período de expiración para las suscripciones](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md), [Establecer el período de retención de distribución para las publicaciones transaccionales &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/set-distribution-retention-period-for-transactional-publications.md) y [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
## <a name="transactional-replication"></a>Replicación transaccional  
 La replicación transaccional utiliza el período máximo de retención de distribución (el parámetro **@max_distretention** de [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)) y el período de retención de la publicación (el parámetro **@retention** de [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)):  
  
-   Si una suscripción no se sincroniza dentro del período máximo de retención de distribución (el valor predeterminado es de 72 horas) y existen cambios en la base de datos de distribución que no se han entregado al suscriptor, el trabajo **Limpieza de la distribución** que se ejecuta en el distribuidor marcará la suscripción como desactivada. Debe reinicializarse la suscripción.  
  
-   Si una suscripción no se sincroniza dentro del período de retención de la publicación (el valor predeterminado es de 336 horas), la suscripción expirará y el trabajo **Limpieza de suscripciones expiradas** que se ejecuta en el publicador quitará la suscripción. La suscripción se debe volver a crear y sincronizar.  
  
     Si una suscripción de inserción expira, se quita completamente, pero esto no sucede con las suscripciones de extracción. Debe limpiar las suscripciones de extracción en el suscriptor. Para más información, consulte [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
## <a name="merge-replication"></a>Replicación de mezcla  
 La replicación de mezcla utiliza el período de retención de la publicación (los parámetros de **@retention** y **@retention_period_unit** de [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)). Cuando una suscripción expira, debe reinicializarse, porque se quitan los metadatos de la suscripción. Los suscripciones que no se reinicializan se quitan con el trabajo **Limpieza de suscripciones expiradas** que se ejecuta en el publicador. De forma predeterminada, este trabajo se ejecuta diariamente; quita todas las suscripciones de inserción que no se han sincronizado una vez transcurrido el doble de tiempo del período de retención de la publicación. Por ejemplo:  
  
-   Su una publicación tiene un período de retención de 14 días, una suscripción puede expirar si no se ha sincronizado en 14 días.  
  
     Si el publicador está ejecutando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior y el agente de la suscripción es de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, una suscripción expira únicamente si se han producido cambios en los datos de la partición de esa suscripción. Por ejemplo, suponga que un suscriptor recibe datos exclusivamente de los clientes de Alemania. Si el período de retención está establecido en 14 días, la suscripción expira el día 14 solamente si se han producido cambios en los datos de los clientes alemanes en los últimos 14 días.  
  
-   Desde los días 14 a 27 después de la última sincronización, la suscripción se puede reinicializar.  
  
-   Transcurridos 28 días desde la última sincronización, el trabajo **Limpieza de suscripciones expiradas** quita la suscripción. Si una suscripción de inserción expira, se quita completamente, pero esto no sucede con las suscripciones de extracción. Debe limpiar las suscripciones de extracción en el suscriptor. Para más información, consulte [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>Consideraciones para establecer el período de retención de publicaciones de combinación  
 Tenga en cuenta las siguientes consideraciones al establecer el período de retención de publicaciones de combinación:  
  
-   El período de retención de las publicaciones de combinación tiene un período de gracia de 24 horas para incluir a los suscriptores en diferentes zonas horarias. Si, por ejemplo, se establece un período de retención de un día, el período de retención real será de 48 horas.  
  
-   La limpieza de los metadatos de la replicación de mezcla depende del período de retención de la publicación:  
  
    -   La replicación no puede limpiar metadatos en las bases de datos de suscripciones y publicaciones hasta que se haya alcanzado el período de retención. Tenga cuidado al especificar un valor elevado para el período de retención, ya que puede afectar negativamente al rendimiento de la replicación. Se recomienda utilizar un valor bajo si puede prever con exactitud que todos los suscriptores se sincronizarán con regularidad dentro del período establecido.  
  
    -   Es posible especificar que las suscripciones no expiren nunca (el valor 0 para **@retention**), pero se recomienda que no utilice este valor, porque los metadatos no se podrán limpiar.  
  
-   El período de retención de cualquier republicador debe establecerse en un valor igual o menor que el período de retención establecido en el publicador original. También debe utilizar los mismos valores de retención de la publicación para todos los publicadores y sus asociados de sincronización alternativos. El uso de valores distintos puede conducir a la no convergencia. Si necesita cambiar el valor de retención de la publicación, vuelva a inicializar el suscriptor a fin de evitar la no convergencia de los datos.  
  
-   Si después de realizar una limpieza se aumenta el período de retención y se intenta mezclar una suscripción con el publicador (que ya ha eliminado los metadatos), la suscripción no expirará debido al aumento del valor de retención. No obstante, el publicador no tendrá suficientes metadatos para descargar los cambios en el suscriptor, lo que daría lugar a la falta de convergencia.  
  
## <a name="see-also"></a>Vea también  
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Administración del Agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
