---
title: Visualización de información y realización de tareas mediante el Monitor de replicación | Microsoft Docs
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
ms.openlocfilehash: 60586083e8bdfe7f0227db605d9f36d50a59ef0d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049355"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>Visualización de información y realización de tareas mediante el Monitor de replicación
El Monitor de replicación proporciona una serie de pestañas y opciones para ver información y realizar diversas tareas. En este artículo se describe todo lo que se puede ver y realizar con el Monitor de replicación.

## <a name="for-a-publication"></a>Para una publicación

### <a name="view-information"></a>Ver información

  El Monitor de replicación proporciona las siguientes pestañas con información acerca de la publicación seleccionada:  
  
-   **Todas las suscripciones** : esta ficha muestra información acerca de todas las suscripciones a la publicación seleccionada.  
  
-   **Agentes** : en esta pestaña se muestra información sobre todos los agentes utilizados por una publicación:  
  
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
  
     Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. También puede tener acceso a información más detallada y realizar tareas en esta pestaña. Para obtener más información, vea [ver información y realizar tareas mediante el monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
4.  Para ver información acerca de los agentes, haga clic en la pestaña **agentes** . También puede tener acceso a información más detallada y realizar tareas en esta pestaña. Para obtener más información, vea [ver información y realizar tareas mediante el monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).    
5.  Para ver información acerca de los umbrales y las advertencias del agente, haga clic en la pestaña **advertencias** . Para obtener más información, vea [establecer umbrales y advertencias en el monitor de replicación](set-thresholds-and-warnings-in-replication-monitor.md).   
6.  Para ver información acerca de los testigos de seguimiento, haga clic en la pestaña **testigos de seguimiento** . Para obtener más información sobre cómo usar testigos de seguimiento, vea [medir la latencia y validar conexiones para la replicación transaccional](measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="for-a-publisher"></a>Para un publicador
  El Monitor de replicación proporciona las siguientes pestañas que muestran información sobre el publicador seleccionado:  
  
-   **Publicaciones** : esta ficha muestra información acerca de todas las publicaciones en el publicador seleccionado.  
  
-   **Lista de supervisión de suscripciones** : esta pestaña está diseñada para mostrar información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o el rendimiento más bajo. Esta pestaña no se muestra para los distribuidores que ejecutan versiones anteriores a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] .  
  
-   Pestaña **agentes** : en esta pestaña se muestra información detallada sobre los agentes y trabajos utilizados por todos los tipos de replicación. La pestaña también le permite iniciar y detener cada agente y trabajo.  
  
 Para obtener más información acerca de las opciones de esta pestaña, haga clic en el panel derecho y , a continuación, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Vista de información y realización de tareas
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.    
2.  Para ver información sobre todas las publicaciones, haga clic en la pestaña **Publicaciones** .    
3.  Para ver información acerca de las suscripciones, haga clic en la pestaña **lista de supervisión de suscripciones** . También puede tener acceso a información más detallada y realizar tareas desde esta pestaña:    
    -   Para ver información detallada sobre el agente asociado a una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Ver detalles**.    
    -   Para ver las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**.    
    -   Para sincronizar una suscripción de inserción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Iniciar sincronización**.    
    -   Para reinicializar una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Reinicializar suscripción**.   
4.  Para ver información acerca de los agentes, haga clic en la pestaña **agentes** . También puede tener acceso a información más detallada y realizar tareas en esta pestaña:    
    -   Para ver información detallada sobre un agente (por ejemplo, mensajes informativos y mensajes de error), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Ver detalles**.    
    -   Para ver información detallada del trabajo que ejecuta el agente (como la programación, los detalles de los pasos del trabajo, etc.), haga clic con el botón secundario en el agente y, a continuación, haga clic en **Propiedades**.    
    -   Para administrar perfiles para el agente, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Perfil del agente**. Para más información, vea [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md).    
    -   Para iniciar un agente que no se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Iniciar agente**.    
    -   Para detener un agente que se está ejecutando, haga clic con el botón secundario en el agente y, a continuación, haga clic en **Detener agente**.  
  
## <a name="for-a-subscription"></a>Para una suscripción 

  El Monitor de replicación proporciona las siguientes pestañas que incluyen información acerca de las suscripciones:  
  
-   **Todas las suscripciones** : esta ficha muestra información acerca de todas las suscripciones a la publicación seleccionada.  
  
-   **Lista de supervisión de suscripciones** : esta pestaña está diseñada para mostrar información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o el rendimiento más bajo. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obtener más información acerca de las opciones de cada pestaña, haga clic en la pestaña en el panel derecho y, a continuación, haga clic en **Ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="all-subscriptions-tab"></a>Pestaña todas las suscripciones  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.   
2.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Todas las suscripciones** . Para ver solamente aquellas suscripciones que se encuentren en un estado determinado, por ejemplo sincronizando, seleccione una opción de la lista desplegable **Mostrar** .   
3.  Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. También puede tener acceso a información más detallada y realizar tareas en esta pestaña. Para obtener más información, vea [ver información y realizar tareas mediante el monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
### <a name="subscription-watch-list-tab"></a>Pestaña Lista de supervisión de suscripciones  
  
1.  Expanda un grupo de publicador en el panel izquierdo y, a continuación, haga clic en un publicador.   
2.  Para ver información acerca de las suscripciones, haga clic en la pestaña **Lista de supervisión de suscripciones** .  
3.  Seleccione el tipo de suscripción que se va a mostrar en la lista desplegable **Mostrar \<SubscriptionType> suscripciones** . Para ver solamente aquellas suscripciones que se encuentren en un estado determinado, por ejemplo sincronizando, seleccione una opción de la lista desplegable **Mostrar** .    
4.  Para ver y modificar las propiedades de una suscripción, haga clic con el botón secundario en la suscripción y, a continuación, haga clic en **Propiedades**. También puede tener acceso a información más detallada y realizar tareas en esta pestaña. Para obtener más información, vea [ver información y realizar tareas mediante el monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  

## <a name="for-publication-agents"></a>Para los agentes de publicación

  El Monitor de replicación proporciona la pestaña **Agentes** , que incluye información sobre los agentes asociados con la publicación seleccionada. Los Agente de distribución y Agente de mezcla están asociados a las suscripciones; para obtener más información, vea [ver información y realizar tareas mediante el monitor de replicación](view-information-and-perform-tasks-replication-monitor.md).  
  
 Esta pestaña muestra información de los siguientes agentes:    
-   El Agente de instantáneas, utilizado por todas las publicaciones.    
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.    
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
 Para ver más información sobre las opciones de esta pestaña, haga clic en **ayuda** en la barra de menús. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
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
  
-   **Todas las suscripciones** : esta ficha muestra información acerca de todas las suscripciones a la publicación seleccionada.  
  
-   **Lista de supervisión de suscripciones** : esta pestaña está diseñada para mostrar información acerca de las suscripciones de todas las publicaciones disponibles en el publicador seleccionado que tienen errores, advertencias o el rendimiento más bajo. Esta pestaña no se muestra en los distribuidores que se ejecutan en versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
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
  

## <a name="see-also"></a>Consulte también  
 [Ver y modificar propiedades de publicación](../publish/view-and-modify-publication-properties.md)   
 [Supervisión de la replicación](../monitoring-replication.md)  
  