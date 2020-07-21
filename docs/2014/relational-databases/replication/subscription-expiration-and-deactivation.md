---
title: Desactivación y expiración de las suscripciones| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d81e8b5c02fcfe5399be9e63c8160036a999547
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997939"
---
# <a name="subscription-expiration-and-deactivation"></a>Desactivación y expiración de las suscripciones
  Las suscripciones se pueden desactivar o pueden expirar si no se sincronizan en un *período de retención*especificado. La acción que se produce depende del tipo de replicación y del período de retención que se supere.  
  
 Para establecer períodos de retención, vea [Establecer el período de expiración para las suscripciones](publish/set-the-expiration-period-for-subscriptions.md), [Establecer el período de retención de distribución para las publicaciones transaccionales &#40;SQL Server Management Studio&#41;](set-distribution-retention-period-for-transactional-publications.md) y [Configurar la publicación y la distribución](configure-publishing-and-distribution.md).  
  
## <a name="transactional-replication"></a>Replicación transaccional  
 La replicación transaccional utiliza el período máximo de retención de distribución (el **@max_distretention** parámetro de [sp_adddistributiondb &#40;&#41;de TRANSACT-SQL ](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)) y el período de retención de la publicación (el **@retention** parámetro de [sp_addpublication &#40;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)&#41;):  
  
-   Si una suscripción no se sincroniza dentro del período máximo de retención de distribución (el valor predeterminado es de 72 horas) y existen cambios en la base de datos de distribución que no se han entregado al suscriptor, el trabajo **Limpieza de la distribución** que se ejecuta en el distribuidor marcará la suscripción como desactivada. Debe reinicializarse la suscripción.  
  
-   Si una suscripción no se sincroniza dentro del período de retención de la publicación (el valor predeterminado es de 336 horas), la suscripción expirará y el trabajo **Limpieza de suscripciones expiradas** que se ejecuta en el publicador quitará la suscripción. La suscripción se debe volver a crear y sincronizar.  
  
     Si una suscripción de inserción expira, se quita completamente, pero esto no sucede con las suscripciones de extracción. Debe limpiar las suscripciones de extracción en el suscriptor. Para más información, consulte [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
## <a name="merge-replication"></a>Replicación de mezcla  
 La replicación de mezcla utiliza el período de retención de la publicación (los **@retention** **@retention_period_unit** parámetros y de [sp_addmergepublication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)). Cuando una suscripción expira, debe reinicializarse, porque se quitan los metadatos de la suscripción. Los suscripciones que no se reinicializan se quitan con el trabajo **Limpieza de suscripciones expiradas** que se ejecuta en el publicador. De forma predeterminada, este trabajo se ejecuta diariamente; quita todas las suscripciones de inserción que no se han sincronizado una vez transcurrido el doble de tiempo del período de retención de la publicación. Por ejemplo:  
  
-   Su una publicación tiene un período de retención de 14 días, una suscripción puede expirar si no se ha sincronizado en 14 días.  
  
     Si el publicador está ejecutando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior y el agente de la suscripción es de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, una suscripción expira únicamente si se han producido cambios en los datos de la partición de esa suscripción. Por ejemplo, suponga que un suscriptor recibe datos exclusivamente de los clientes de Alemania. Si el período de retención está establecido en 14 días, la suscripción expira el día 14 solamente si se han producido cambios en los datos de los clientes alemanes en los últimos 14 días.  
  
-   Desde los días 14 a 27 después de la última sincronización, la suscripción se puede reinicializar.  
  
-   Transcurridos 28 días desde la última sincronización, el trabajo **Limpieza de suscripciones expiradas** quita la suscripción. Si una suscripción de inserción expira, se quita completamente, pero esto no sucede con las suscripciones de extracción. Debe limpiar las suscripciones de extracción en el suscriptor. Para más información, consulte [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>Consideraciones para establecer el período de retención de publicaciones de combinación  
 Tenga en cuenta las siguientes consideraciones al establecer el período de retención de publicaciones de combinación:  
  
-   El período de retención de las publicaciones de combinación tiene un período de gracia de 24 horas para incluir a los suscriptores en diferentes zonas horarias. Si, por ejemplo, se establece un período de retención de un día, el período de retención real será de 48 horas.  
  
-   La limpieza de los metadatos de la replicación de mezcla depende del período de retención de la publicación:  
  
    -   La replicación no puede limpiar metadatos en las bases de datos de suscripciones y publicaciones hasta que se haya alcanzado el período de retención. Tenga cuidado al especificar un valor elevado para el período de retención, ya que puede afectar negativamente al rendimiento de la replicación. Se recomienda utilizar un valor bajo si puede prever con exactitud que todos los suscriptores se sincronizarán con regularidad dentro del período establecido.  
  
    -   Es posible especificar que las suscripciones no expiren nunca (un valor de 0 para **@retention** ), pero se recomienda encarecidamente no usar este valor, ya que los metadatos no se pueden limpiar.  
  
-   El período de retención de cualquier republicador debe establecerse en un valor igual o menor que el período de retención establecido en el publicador original. También debe utilizar los mismos valores de retención de la publicación para todos los publicadores y sus asociados de sincronización alternativos. El uso de valores distintos puede conducir a la no convergencia. Si necesita cambiar el valor de retención de la publicación, vuelva a inicializar el suscriptor a fin de evitar la no convergencia de los datos.  
  
-   Si después de realizar una limpieza se aumenta el período de retención y se intenta mezclar una suscripción con el publicador (que ya ha eliminado los metadatos), la suscripción no expirará debido al aumento del valor de retención. No obstante, el publicador no tendrá suficientes metadatos para descargar los cambios en el suscriptor, lo que daría lugar a la falta de convergencia.  
  
## <a name="see-also"></a>Consulte también  
 [Reinicializar suscripciones](reinitialize-subscriptions.md)   
 [Administración del Agente de replicación](agents/replication-agent-administration.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
