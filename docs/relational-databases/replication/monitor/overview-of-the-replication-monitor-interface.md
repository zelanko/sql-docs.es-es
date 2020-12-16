---
description: Información general de la interfaz del Monitor de replicación
title: Información general de la interfaz del Monitor de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 078f0e34-7153-45c4-8725-778b5bef88da
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 92101ce00eb74e7a48a7e72b320eb536e4d60022
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477826"
---
# <a name="overview-of-the-replication-monitor-interface"></a>Información general de la interfaz del Monitor de replicación
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  El Monitor de replicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] presenta una vista centrada en el publicador o en el distribuidor de toda la actividad de replicación en un formato de dos paneles. Se agrega un publicador al monitor en el panel izquierdo y, en el panel derecho, el monitor muestra información sobre el publicador, sus publicaciones, las suscripciones a esas publicaciones y los diversos agentes de replicación. Además de presentar información de la topología de replicación, el Monitor de replicación permite realizar varias tareas, como iniciar y detener agentes y validar datos.  
  
## <a name="viewing-information-for-the-entire-topology"></a>Ver información de toda la topología  
 El panel izquierdo del Monitor de replicación muestra  
  
-   Grupos de publicadores, publicadores y publicaciones.  
  
-   Distribuidores, publicadores y publicaciones.  
  
 Para ver cualquier información en el Monitor de replicación, primero debe agregar un publicador. Para obtener más información, vea [Agregar y quitar publicadores del Monitor de replicación](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
 El panel izquierdo ayuda a responder a las siguientes preguntas:  
  
-   ¿Es correcto el sistema de replicación?  
  
     El estado del sistema de replicación es relativamente correcto si no existen iconos de error en los nodos del panel izquierdo. Para obtener una vista más completa del estado del sistema, también debe comprobar la pestaña **Lista de supervisión de suscripciones** , en la que se muestra información sobre las suscripciones que pueden requerir atención.  
  
-   ¿Por qué no se ejecuta un agente?  
  
     Un agente no funciona en un momento determinado porque no está programado para ejecutarse o porque se ha producido un error. Si se ha producido un error, se muestra un icono de error en los nodos correspondientes del panel izquierdo. Por ejemplo, si el Agente de instantáneas de una publicación se detiene debido a un error, se muestra un icono de error en el grupo de publicador, el publicador y los nodos de publicación. En la pestaña **Agentes** de la publicación se muestra información resumida del Agente de instantáneas; haga doble clic en el Agente de instantáneas de esta pestaña para obtener información detallada del error.  
  
## <a name="viewing-information-and-performing-tasks-related-to-distributors"></a>Ver información y realizar tareas relacionadas con distribuidores  
 El Monitor de replicación muestra información sobre distribuidores en tres pestañas:  
  
-   Pestaña **Publicaciones**  
  
     Esta pestaña proporciona información resumida de todas las publicaciones de un distribuidor.  
  
-   Pestaña **Lista de supervisión de suscripciones**  
  
     Esta pestaña proporciona información sobre las suscripciones del distribuidor seleccionado. Puede filtrar la lista de suscripciones para ver errores, advertencias y las suscripciones que tienen un rendimiento bajo. La pestaña le permite igualmente realizar las siguientes tareas: acceder a las propiedades de la suscripción, acceder a información detallada sobre el agente o agentes asociados con una suscripción, así como reinicializar y validar suscripciones.  
  
     La pestaña **Lista de supervisión de suscripciones** ayuda a responder a las siguientes preguntas:  
  
    -   ¿Qué suscripciones son lentas?  
  
         Establezca opciones en esta pestaña para que la cuadrícula muestre las suscripciones ordenadas por su rendimiento relativo.  
  
    -   ¿Es correcto el sistema de replicación?  
  
         La cuadrícula de esta pestaña muestra iconos de advertencia y error en las suscripciones que requieran su atención.  
  
     Esta pestaña no está disponible para distribuidores que ejecuten versiones de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o anterior.  
  
-   Pestaña **Agentes**  
  
     Esta pestaña muestra información detallada sobre los agentes y trabajos utilizados por todos los tipos de replicación. La pestaña también le permite iniciar y detener cada agente y trabajo.  
  
 El Monitor de replicación también proporciona un menú contextual para el nodo de distribuidor. Haga clic con el botón secundario en un distribuidor del panel izquierdo con el fin de realizar las siguientes tareas:  
  
-   Agregar un publicador al Monitor de replicación.  
  
-   Editar la configuración del Monitor de replicación del distribuidor.  
  
-   Cambiar a la vista de grupo de publicador.  
  
## <a name="viewing-information-and-performing-tasks-related-to-publishers"></a>Ver información y realizar tareas relacionadas con publicadores  
 El Monitor de replicación muestra información sobre publicadores en tres pestañas:  
  
-   Pestaña **Publicaciones**  
  
     Esta pestaña proporciona información resumida de todas las publicaciones en un publicador.  
  
-   Pestaña **Lista de supervisión de suscripciones**  
  
     Esta pestaña está diseñada para mostrar información sobre suscripciones de todas las publicaciones disponibles en el publicador seleccionado. Puede filtrar la lista de suscripciones para ver errores, advertencias y las suscripciones que tienen un rendimiento bajo. La pestaña le permite igualmente: tener acceso a las propiedades de la suscripción, tener acceso a información detallada sobre el agente o agentes asociados con una suscripción, y reinicializar y validar suscripciones.  
  
     La pestaña **Lista de supervisión de suscripciones** ayuda a responder a las siguientes preguntas:  
  
    -   ¿Qué suscripciones son lentas?  
  
         Establezca opciones en esta pestaña para que la cuadrícula muestre las suscripciones ordenadas por su rendimiento relativo.  
  
    -   ¿Es correcto el sistema de replicación?  
  
         La cuadrícula de esta pestaña muestra iconos de advertencia y error en las suscripciones que requieran su atención.  
  
     Esta pestaña no se muestra en los distribuidores que ejecuten versiones anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   Pestaña **Agentes**  
  
     Esta pestaña muestra información detallada sobre los agentes y trabajos utilizados por todos los tipos de replicación. La pestaña también le permite iniciar y detener cada agente y trabajo.  
  
 Para obtener más información, consulte [Ver información y realizar tareas para un publicador &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 El Monitor de replicación también proporciona un menú contextual para el nodo de publicador. En el panel izquierdo, haga clic con el botón secundario en un publicador para:  
  
-   Editar la configuración del Monitor de replicación para el publicador.  
  
-   Quitar el publicador del Monitor de replicación.  
  
-   Ver y editar perfiles de agente.  
  
-   Conectarse o desconectarse del distribuidor que almacena información sobre el publicador.  
  
## <a name="viewing-information-and-performing-tasks-related-to-publications"></a>Ver información y realizar tareas relacionadas con publicaciones  
 El Monitor de replicación muestra información sobre publicaciones en tres pestañas y varias ventanas de detalles:  
  
-   Pestaña **Todas las suscripciones**  
  
     En esta pestaña se muestra información acerca de todas las suscripciones de la publicación seleccionada. De forma predeterminada, esta pestaña está ordenada por orden de prioridad: primero los errores, a continuación las advertencias y, por último, en orden creciente de rendimiento, las suscripciones con rendimiento bajo en la parte superior.  
  
     La pestaña **Todas las suscripciones** ayuda a responder a las siguientes preguntas:  
  
    -   ¿Qué suscripciones son lentas?  
  
         Establezca opciones en esta pestaña para que la cuadrícula muestre las suscripciones ordenadas por su rendimiento relativo.  
  
    -   ¿Es correcto el sistema de replicación?  
  
         La cuadrícula de esta pestaña muestra iconos de advertencia y error en las suscripciones que requieran su atención.  
  
-   Pestaña **Agentes**  
  
     En esta pestaña se muestra información sobre los agentes utilizados por la replicación. Esta pestaña muestra información de los siguientes agentes:  
  
    -   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
    -   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
    -   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
     La pestaña también permite realizar las tareas siguientes: tener acceso a información detallada sobre cada agente e iniciar y detener cada agente. Para obtener información sobre los agentes asociados con suscripciones (el Agente de distribución y el Agente de mezcla), vea la sección "Ver información y realizar tareas relacionadas con suscripciones" en este tema.  
  
-   Pestaña **Advertencias**  
  
     Esta pestaña le permite especificar advertencias y alertas para los agentes. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Pestaña **Testigos de seguimiento** (solo replicación transaccional)  
  
     Esta pestaña permite medir la latencia, es decir, el tiempo que transcurre entre la confirmación de una transacción en el publicador y la confirmación de la transacción correspondiente en el suscriptor.  
  
     Esta pestaña ayuda a responder a la siguiente pregunta:  
  
    -   ¿Cuánto tardará una transacción confirmada ahora en llegar al suscriptor en la replicación transaccional?  
  
         Vea el tiempo total que tarda una transacción en viajar por el sistema y compárelo también con tiempos anteriores.  
  
     Esta pestaña no se muestra para los distribuidores que ejecuten [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o anterior. Para obtener más información sobre cómo utilizar los testigos de seguimiento, vea [Medir la latencia y validar las conexiones de la replicación transaccional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
-   Ventanas de detalles para los agentes asociados con una publicación. Los siguientes agentes están asociados con publicaciones:  
  
    -   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
    -   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
    -   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
     Haga doble clic en un agente en el Monitor de replicación para tener acceso a información en la ventana de detalles. Además de los agentes mencionados anteriormente, hay agentes asociados con suscripciones: el Agente de distribución para suscripciones a instantánea y publicaciones transaccionales, y el agente de mezcla para suscripciones a publicaciones de combinación. Para obtener más información, vea la sección "Ver información y realizar tareas relacionadas con suscripciones" en este tema.  
  
     Las ventanas de detalles de agente proporcionan información sobre las sesiones del agente, incluida la hora de inicio, la hora de finalización, la duración y las acciones realizadas en una sesión. Ayudan a responder a la siguiente pregunta:  
  
    -   ¿Por qué no se ejecuta un agente?  
  
         Los mensajes de error disponibles proporcionan información detallada sobre por qué no funciona un agente y un punto inicial para solucionar problemas con los agentes asociados con una publicación.  
  
 Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 El Monitor de replicación también proporciona un menú contextual para el nodo de publicaciones. En el panel izquierdo, haga clic con el botón secundario en una publicación para:  
  
-   Reinicializar todas las suscripciones en una publicación.  
  
-   Validar todas las suscripciones en una publicación.  
  
-   Generar una instantánea para una publicación.  
  
-   Ver y editar las propiedades de una publicación.  
  
## <a name="viewing-information-and-performing-tasks-related-to-subscriptions"></a>Ver información y realizar tareas relacionadas con suscripciones  
 El Monitor de replicación muestra información sobre suscripciones en varias pestañas diferentes. Haga doble clic en una suscripción en el Monitor de replicación para tener acceso a estas pestañas en una ventana de detalles. Todas estas pestañas son útiles para responder a la pregunta "¿Por qué no funciona un agente?". Los mensajes de error disponibles proporcionan información detallada sobre por qué no funciona un agente y un punto inicial para solucionar problemas con los agentes asociados con una suscripción.  
  
-   **Todas las suscripciones** y **Lista de supervisión de suscripciones**  
  
     Estas pestañas se han descrito anteriormente en este tema.  
  
-   Pestaña **Historial de Publicador a distribuidor** (solo replicación transaccional)  
  
     En esta pestaña se muestra información sobre el Agente de registro del LOG para una publicación (la pestaña es idéntica a la ventana de detalles del Agente de registro del LOG).  
  
-   Pestaña **Historial de Distribuidor a suscriptor** (replicación de instantánea y replicación transaccional)  
  
     En esta pestaña se muestra información sobre el Agente de distribución para una suscripción.  
  
-   Pestaña **Comandos sin distribuir** (solo replicación transaccional)  
  
     En esta pestaña se muestra información sobre le número de comandos de la base de datos de distribución que no se han entregado al suscriptor seleccionado y el tiempo estimado para entregar esos comandos. La pestaña ayuda a responder a la pregunta, "¿Qué retraso tiene mi suscripción?" Esta pestaña no se muestra en los distribuidores que ejecuten versiones anteriores a SQL Server 2005.  
  
-   Pestaña **Historial de sincronizaciones** (solo replicación de mezcla)  
  
     En esta pestaña se muestra información sobre el Agente de mezcla para una suscripción. Esta pestaña ayuda a responder a la siguiente pregunta:  
  
    -   ¿Por qué es lenta la suscripción de mezcla?  
  
         En esta pestaña se proporcionan estadísticas detalladas de cada artículo procesado durante la sincronización, incluido el tiempo invertido en cada fase del proceso (carga de cambios, descarga de cambios, etc.). Puede ayudar a identificar con precisión tablas específicas que provocan lentitud y el mejor lugar para solucionar problemas de rendimiento con suscripciones de mezcla.  
  
 Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).
  
## <a name="viewing-information-and-performing-tasks-related-to-agent-profiles"></a>Ver información y realizar tareas relacionadas con perfiles de agente  
 El Monitor de replicación incluye varios cuadros de diálogo para administrar perfiles de agente. Los perfiles de agente son conjuntos de parámetros de un agente que determinan su comportamiento. Para obtener más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md). Los cuadros de diálogo son:  
  
-   **Perfiles de agente**  
  
     Este cuadro de diálogo permite: cambiar las propiedades de perfiles, crear y eliminar perfiles, especificar un perfil predeterminado y especificar que todos los agentes de un tipo específico (por ejemplo, los Agentes de instantáneas) deben utilizar un perfil determinado.  
  
-   **Propiedades de \<AgentProfileName>**  
  
     Este cuadro de diálogo permite ver y editar la configuración de parámetros de un perfil.  
  
-   **Nuevo perfil de agente**  
  
     Este cuadro de diálogo permite crear un perfil nuevo y, opcionalmente, incluye los valores de un perfil existente.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
