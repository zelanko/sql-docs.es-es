---
title: Ver información y realizar tareas con el Monitor de replicación | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 400db44d053caf131ef13947adbd0154875995cf
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54136377"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>Ver información y realizar tareas mediante el Monitor de replicación
Monitor de replicación proporciona una serie de fichas y opciones para ver información y realizar diversas tareas. En este artículo se describe los diferentes elementos que se pueden ver y realizar al utilizar al Monitor de replicación.

## <a name="for-a-publication"></a>Para una publicación

### <a name="view-information"></a>Ver información

  El Monitor de replicación proporciona las siguientes pestañas con información acerca de la publicación seleccionada:  
  
-   **Todas las suscripciones** -esta ficha muestra información sobre todas las suscripciones a la publicación seleccionada.  
  
-   **Los agentes** -esta pestaña muestra información acerca de todos los agentes utilizados por una publicación:  
  
    -   El Agente de instantáneas, utilizado por todas las publicaciones.    
    -   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.    
    -   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola.  
  
-   **Advertencias** (para distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores)   
    -   Esta pestaña permite especificar advertencias y alertas para agentes.  
  
-   **Testigos de seguimiento** (solo replicación transaccional, para distribuidores que ejecuten [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores)  
  
     Esta pestaña permite medir la latencia, es decir, el tiempo que transcurre entre la confirmación de una transacción en el publicador y la confirmación de la transacción correspondiente en el suscriptor.  
  
 Para obtener más información acerca de las opciones de cada pestaña, haga clic en la pestaña en el panel derecho y, a continuación, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="perform-tasks"></a>Realizar tareas
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.    
2.  Para ver y modificar las propiedades de una publicación, haga clic con el botón secundario en la publicación y, a continuación, haga clic en **Propiedades**.    
3.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Todas las suscripciones** .  
  
     Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada. Para obtener más información, consulte [ver información y realizar tareas con el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
4.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada. Para obtener más información, consulte [ver información y realizar tareas con el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).    
5.  Para ver información sobre las advertencias del agente y umbrales, haga clic en la pestaña **Advertencias** . Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md).   
6.  Para ver información acerca de los token de seguimiento, haga clic en la pestaña **Token de seguimiento** . Para obtener más información acerca de cómo utilizar los testigos de seguimiento, vea [Medir la latencia y validar las conexiones de la replicación transaccional](measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="for-a-publisher"></a>Para un publicador
  El Monitor de replicación proporciona las siguientes pestañas que muestran información sobre el publicador seleccionado:  
  
-   **Las publicaciones** -esta pestaña muestra información sobre todas las publicaciones del publicador seleccionado.  
  
-   **Lista de supervisión** -esta pestaña está diseñada para mostrar información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o un rendimiento insuficiente. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   **Los agentes** pestaña: esta pestaña muestra información detallada sobre los agentes y trabajos que se usan por todos los tipos de replicación. La pestaña también le permite iniciar y detener cada agente y trabajo.  
  
 Para obtener más información acerca de las opciones de esta pestaña, haga clic en el panel derecho y , a continuación, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Vista de información y realización de tareas
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.    
2.  Para ver información sobre todas las publicaciones, haga clic en la pestaña **Publicaciones** .    
3.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Lista de supervisión de suscripciones** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:    
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver detalles**.    
    -   Para ver las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**.    
    -   Para sincronizar una suscripción de inserción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.    
    -   Para reinicializar una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.   
4.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:    
    -   Para ver información detallada sobre un agente (por ejemplo, mensajes informativos y mensajes de error), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Ver detalles**.    
    -   Para ver información detallada del trabajo que ejecuta el agente (como la programación, los detalles de los pasos del trabajo, etc.), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Propiedades**.    
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md).    
    -   Para iniciar un agente que no se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Iniciar agente**.    
    -   Para detener un agente que se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Detener agente**.  
  
## <a name="for-a-subscription"></a>Para obtener una suscripción 

  El Monitor de replicación proporciona las siguientes pestañas que incluyen información acerca de las suscripciones:  
  
-   **Todas las suscripciones** -esta ficha muestra información sobre todas las suscripciones a la publicación seleccionada.  
  
-   **Lista de supervisión** -esta pestaña está diseñada para mostrar información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o un rendimiento insuficiente. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obtener más información acerca de las opciones de cada pestaña, haga clic en la pestaña en el panel derecho y, a continuación, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="all-subscriptions-tab"></a>Pestaña de todas las suscripciones  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.   
2.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Todas las suscripciones** . Para ver solamente aquellas suscripciones que se encuentren en un estado determinado, por ejemplo sincronizando, seleccione una opción de la lista desplegable **Mostrar** .   
3.  Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada. Para obtener más información, consulte [ver información y realizar tareas con el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
### <a name="subscription-watch-list-tab"></a>Pestaña de la lista de supervisión de suscripciones  
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.   
2.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Lista de supervisión de suscripciones** .  
3.  Seleccione el tipo de suscripción que quiere mostrar en la lista desplegable **Mostrar suscripciones \<TipoDeSuscripción>** . Para ver solamente aquellas suscripciones que se encuentren en un estado determinado, por ejemplo sincronizando, seleccione una opción de la lista desplegable **Mostrar** .    
4.  Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada. Para obtener más información, consulte [ver información y realizar tareas con el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  

## <a name="for-publication-agents"></a>Para los agentes de publicación

  El Monitor de replicación proporciona la pestaña **Agentes** , que incluye información sobre los agentes asociados con la publicación seleccionada. El agente de distribución y agente de mezcla están asociados con suscripciones; Para obtener más información, consulte [ver información y realizar tareas con el Monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
 Esta pestaña muestra información de los siguientes agentes:    
-   El Agente de instantáneas, utilizado por todas las publicaciones.    
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.    
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
 Para ver más información acerca de las opciones de esta pestaña, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Vista de información y realización de tareas 
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.    
2.  Para ver información sobre los agentes, haga clic en la pestaña **Agentes** . En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre un agente (por ejemplo, mensajes informativos y mensajes de error), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Ver detalles**.    
    -   Para ver información detallada del trabajo que ejecuta el agente (como la programación, los detalles de los pasos del trabajo, etc.), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Propiedades**.    
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md).  
    -   Para iniciar un agente que no se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Iniciar agente**.  
      -   Para detener un agente que se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Detener agente**.  

## <a name="for-subscription-agents"></a>Para los agentes de suscripción

### <a name="view-information-and-perform-tasks"></a>Ver información y realizar tareas
  El Monitor de replicación proporciona dos pestañas que permiten obtener acceso a información sobre los agentes asociados con una suscripción:  
  
-   **Todas las suscripciones** -esta ficha muestra información sobre todas las suscripciones a la publicación seleccionada.  
  
-   **Lista de supervisión** -esta pestaña está diseñada para mostrar información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o un rendimiento insuficiente. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obtener más información acerca de las opciones de cada pestaña, haga clic en la pestaña en el panel derecho y, a continuación, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Vista de información y realización de tareas 
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.   
2.  Haga clic en la pestaña **Todas las suscripciones** para ver información sobre todas las suscripciones. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:  
  
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver detalles**. La información detallada incluye: historial del agente y mensajes de error, estadísticas de rendimiento de la replicación transaccional y estadísticas de sincronización de los artículos de la replicación de mezcla.    
         Las pestañas de la ventana de detalle que se muestra dependen del tipo de suscripción: en las suscripciones de instantánea, la pestaña es **Historial de Distribuidor a suscriptor**; en las suscripciones transaccionales, las pestañas son **Historial de Publicador a distribuidor**, **Historial de Distribuidor a suscriptor**y **Comandos sin distribuir**; en las suscripciones de mezcla, la pestaña es **Historial de sincronizaciones**.    
    -   Para sincronizar una suscripción de inserción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.    
    -   Para reinicializar una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.    
    -   Para validar una única suscripción de mezcla, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripción**. Para validar todas las suscripciones de una publicación de combinación, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar todas las suscripciones**. Para validar todas las suscripciones de una publicación transaccional, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripciones**.    
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md).  
  
### <a name="view-information-and-perform-tasks"></a>Vista de información y realización de tareas
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.   
2.  Haga clic en la pestaña **Lista de supervisión de suscripciones** para ver información sobre todas las suscripciones. En esta pestaña, también puede realizar tareas y tener acceso a información más detallada:    
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver detalles**. La información detallada incluye: historial del agente y mensajes de error, estadísticas de rendimiento de la replicación transaccional y estadísticas de sincronización de los artículos de la replicación de mezcla.    
         Las pestañas de la ventana de detalle que se muestra dependen del tipo de suscripción: en las suscripciones de instantánea, la pestaña es **Historial de Distribuidor a suscriptor**; en las suscripciones transaccionales, las pestañas son **Historial de Publicador a distribuidor**, **Historial de Distribuidor a suscriptor**y **Rendimiento**; en las suscripciones de mezcla, la pestaña es **Historial de sincronizaciones**.    
    -   Para sincronizar una suscripción de inserción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.    
    -   Para reinicializar una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.    
    -   Para validar una única suscripción de mezcla, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripción**. Para validar todas las suscripciones de una publicación de combinación, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar todas las suscripciones**. Para validar todas las suscripciones de una publicación transaccional, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Validar suscripciones**.    
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md).  
  

## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../publish/view-and-modify-publication-properties.md)   
 [Supervisar la replicación](../monitoring-replication.md)  
  