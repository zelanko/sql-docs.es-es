---
title: Cuadro de diálogo Replicación de SQL Server ' información del distribuidor ' | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.Distributor.Publications.f1
- sql12.rep.monitor.Distributor.commonjobs..f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ca0717a63c9660c225ec238e1e4d2423f7d01ba
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010792"
---
# <a name="distributor-information-dialog-box"></a>Información del distribuidor (cuadro de diálogo) 
En este tema se proporciona información sobre el cuadro de diálogo **distribuidor** 

## <a name="publications"></a>Publicaciones

  La pestaña **Publicaciones** proporciona información de resumen para todas las publicaciones del distribuidor seleccionado en el recuadro izquierdo.  
  
### <a name="options"></a>Opciones  
 La información que se muestra sobre las publicaciones admitidas por el distribuidor incluye una columna que contiene la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del publicador. De lo contrario, la información de publicación será la misma que la información de publicación que se proporciona cuando se ven publicaciones en la vista Publicador del Monitor de replicación. Para obtener más información sobre las columnas en la pestaña **Publicaciones** , vea [Publisher Information, Publications](publisher-information-publications.md).  

## <a name="subscription-watch-list"></a>Lista de supervisión de suscripciones

### <a name="transactional-replication"></a>Replicación transaccional 
  La información de las suscripciones transaccionales incluye el nombre del publicador. De lo contrario, la funcionalidad y la información proporcionadas en este cuadro de diálogo son las mismas que las de la vista Publicador. Para más información sobre cómo utilizar este cuadro de diálogo, vea [Publisher Information, Subscription Watch List &#40;Transactional Publication, SQL Server 2005 and Later&#41;](publisher-information-subscription-watch-list-transactional.md) (Información del publicador, Lista de supervisión de suscripciones (Publicación de transacciones, SQL Server 2005 y versiones posteriores)).  

### <a name="merge-replication"></a>Replicación de mezcla
  El nombre del publicador se incluye en la información para las suscripciones de publicaciones de combinación. De lo contrario, la funcionalidad y la información proporcionadas en este cuadro de diálogo son las mismas que las de la vista Publicador. Para más información sobre cómo utilizar este cuadro de diálogo, vea [Publisher Information, Subscription Watch List &#40;Merge Publication, SQL Server 2005 and Later&#41;](publisher-information-subscription-watch-list-merge-publication.md) (Información del publicador, Lista de supervisión de suscripciones (Publicación de mezcla, SQL Server 2005 y versiones posteriores)). 

### <a name="snapshot-replication"></a>Replicación de instantáneas
  El nombre del publicador se incluye en la información para las suscripciones de publicaciones de instantáneas. De lo contrario, la funcionalidad y la información proporcionadas en este cuadro de diálogo son las mismas que las de la vista Publicador. Para más información sobre cómo utilizar este cuadro de diálogo, vea [Publisher Information, Subscription Watch List &#40;Snapshot Publication, SQL Server 2005 and Later&#41;](publisher-information-subscription-watch-list-snapshot.md) (Información del publicador, Lista de supervisión de suscripciones (Publicación de instantáneas, SQL Server 2005 y versiones posteriores)).  

## <a name="agents"></a>Agentes
   La pestaña **Agentes** muestra información acerca de los agentes y trabajos de mantenimiento asociados con el publicador y el suscriptor.  
  
 Los agentes que están disponibles en la pestaña **Agentes** de un distribuidor en la vista Distribuidor incluyen todos los agentes que están disponibles en la pestaña **Agentes** de un publicador. Sin embargo, la pestaña **Agentes** para un distribuidor en la vista Distribuidor también incluye un Agente de distribuidor y un Agente de mezcla.  
  
 Para obtener más información acerca de los agentes de instantánea, registro del LOB y de lectura de cola, y de los trabajos del mantenimiento, vea [Publisher Information, Agents](publisher-information-agents.md). Observe que cuando está viendo información del agente en la pestaña **Agentes** para un distribuidor, se presenta la información del publicador para los agentes de registro del LOG y de instantánea. Sin embargo, en la pestaña **Agentes** de un distribuidor de la vista Distribuidor, también puede seleccionar **Agente de distribuidor** y **Agente de mezcla**.  
  
### <a name="options"></a>Opciones  
 En las secciones siguientes se describen los datos que se muestran en esta pestaña para el Agente de distribuidor o Agente de mezcla.  
  
### <a name="distributor-agent"></a>Agente de distribuidor  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error    
-   Volver a intentar    
-   En ejecución    
-   No está en ejecución    
-   No se ha iniciado nunca  
  
 **Publicador**  
 La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del publicador.  
  
 **Publicación**  
 Nombre de la publicación a la que está asociada el agente.  
  
 **Suscripción**  
 Nombre de la suscripción, con el formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicación: inserción, extracción o anónima.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Intervalo de tiempo que se ejecutó el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los comandos de inicialización en la base de datos de distribución durante la última ejecución del agente.  
  
 **Latency**  
 El tiempo, en segundos, que ha transcurrido entre el último cambio confirmado en la base de datos de publicación y el comando correspondiente que se confirma en la base de datos de distribución.  
  
 **#Trans**  
 El número de transacciones confirmadas en la base de datos de distribución durante la última ejecución del agente.  
  
 **#Cmds**  
 El número de comandos confirmados en la base de datos de distribución durante la última ejecución del agente. Un comando es lo mismo que un cambio en los datos, como una actualización.  
  
 **Avg. #Cmds**  
 El promedio de comandos por transacción durante la última ejecución del agente.  
  
### <a name="merge-agent"></a>Agente de mezcla  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error    
-   Volver a intentar    
-   En ejecución    
-   No está en ejecución    
-   No se ha iniciado nunca  
  
 **Publicador**  
 La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del publicador.  
  
 **Publicación**  
 Nombre de la publicación a la que está asociada el agente.  
  
 **Suscripción**  
 Nombre de la suscripción, con el formato: [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo de replicación: inserción, extracción o anónima.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Intervalo de tiempo que se ejecutó el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los cambios en la base de datos de distribución.  
  
 **Inserciones de publicador**  
 Número de comandos INSERT aplicados en el publicador.  
  
 **Actualizaciones de publicador**  
 Número de comandos UPDATE aplicados en el publicador.  
  
 **Eliminaciones de publicador**  
 Número de comandos DELETE aplicados en el publicador.  
  
 **Conflictos de publicador**  
 Número de conflictos producidos en el publicador durante el proceso de mezcla.  
  
 **Inserciones de suscriptor**  
 Número de comandos INSERT aplicados en el suscriptor.  
  
 **Actualizaciones de suscriptor**  
 Número de comandos UPDATE aplicados en el suscriptor.  
  
 **Eliminaciones de suscriptor**  
 Número de comandos DELETE aplicados en el suscriptor.  
  
 **Conflictos de suscriptor**  
 Número de conflictos producidos en el suscriptor durante el proceso de mezcla.  
  
 
## <a name="see-also"></a>Consulte también  
 [Iniciar el monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Supervisión de la replicación](monitoring-replication.md)  
  
  
