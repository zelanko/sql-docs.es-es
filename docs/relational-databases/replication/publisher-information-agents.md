---
title: Información de publicador, Agentes | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.commonjobs.f1
ms.assetid: 2346c00d-c269-45a1-af14-68e7fd7ebd7e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5e6192da995dac47d974c3c3f2ff6c5f576acc2e
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123966"
---
# <a name="publisher-information-agents"></a>Información de publicador, Agentes
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La pestaña **Agentes** muestra información sobre los agentes y trabajos de mantenimiento asociados con el publicador:  
  
-   Agente de instantáneas, que se muestra en todas las publicaciones.  
  
-   Agente de registro del LOG, que se muestra en todas las publicaciones transaccionales.  
  
-   Agente de lectura de cola, que se muestra en las publicaciones transaccionales habilitadas para las suscripciones de actualización en cola.  
  
-   Trabajos del mantenimiento, que se muestran en todas las publicaciones:  
  
    -   Reinicialización de suscripciones con errores de validación de datos  
  
    -   Limpieza de historial del agente: distribución  
  
    -   Actualizador de supervisión de replicación para distribución  
  
    -   Comprobación de agentes de replicación  
  
    -   Limpieza de distribución: distribución  
  
    -   Limpieza de suscripciones expiradas  
  
 Para obtener más información sobre estos trabajos, vea [Administración del Agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
## <a name="options"></a>Opciones  
 Para mostrar información sobre un agente o trabajo, seleccione la opción correspondiente en el menú desplegable **Tipos de agente y trabajo** . Para obtener información más detallada y ver cuáles son las tareas relacionadas con un agente o un trabajo, haga clic con el botón secundario en la fila del agente o el trabajo correspondiente y después elija una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene por una o más columnas en el cuadro de diálogo **Ordenar columnas**.  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se van a mostrar y el orden en el que lo harán en el cuadro de diálogo **Elegir columnas**.  
  
-   **Filtro**: filtre las filas de la cuadrícula en función de los valores de columna del cuadro de diálogo **Configuración del filtro**.  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 En las secciones siguientes se describen los datos que se muestran en esta pestaña para cada agente o trabajo.  
  
### <a name="snapshot-agent"></a>Agente de instantáneas  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentar  
  
-   En ejecución  
  
-   Completado  
  
 **Publicación**  
 Nombre de la publicación a la que está asociada el agente.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Tiempo de ejecución del agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los comandos de inicialización en la base de datos de distribución durante la última ejecución del agente.  
  
 **#Trans**  
 El número de transacciones confirmadas en la base de datos de distribución durante la última ejecución del agente.  
  
 **#Cmds**  
 El número de comandos confirmados en la base de datos de distribución durante la última ejecución del agente. Un comando equivale a un cambio en los datos, como una actualización.  
  
### <a name="log-reader-agent"></a>Agente de registro del LOG  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentar  
  
-   En ejecución  
  
-   No está en ejecución  
  
 **Base de datos de publicaciones**  
 Nombre de la publicación a la que está asociada el agente.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Tiempo de ejecución del agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los cambios en la base de datos de distribución.  
  
 **Latencia**  
 El tiempo, en segundos, que ha transcurrido entre el último cambio confirmado en la base de datos de publicación y el comando correspondiente que se confirma en la base de datos de distribución.  
  
 **#Trans**  
 El número de transacciones confirmadas en la base de datos de distribución durante la última ejecución del agente.  
  
 **#Cmds**  
 El número de comandos confirmados en la base de datos de distribución durante la última ejecución del agente. Un comando equivale a un cambio en los datos, como una actualización.  
  
 **Avg. #Cmds**  
 El promedio de comandos por transacción durante la última ejecución del agente.  
  
### <a name="queue-reader-agent"></a>Agente de lectura de cola  
 **Estado**  
 Estado del agente. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentar  
  
-   En ejecución  
  
-   No está en ejecución  
  
 **Base de datos de distribución**  
 Nombre de la base de datos de distribución a la que está asociada el agente.  
  
 **Última hora de inicio**  
 Última hora en que se inició el agente.  
  
 **Duración**  
 Tiempo de ejecución del agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
 **Tasa de entrega**  
 La tasa, en comandos por segundo, a la que se confirman los cambios en la base de datos de distribución.  
  
 **Latencia**  
 El tiempo, en segundos, que ha transcurrido entre el último cambio confirmado en una base de datos de suscripciones y el comando correspondiente que se confirma en la base de datos de publicación.  
  
 **#Trans**  
 El número de transacciones confirmadas en la base de datos de publicación durante la última ejecución del agente.  
  
 **#Cmds**  
 El número de comandos confirmados en la base de datos de publicación durante la última ejecución del agente. Un comando equivale a un cambio en los datos, como una actualización.  
  
 **Avg. #Cmds**  
 El promedio de comandos por transacción durante la última ejecución del agente.  
  
### <a name="maintenance-jobs"></a>Trabajos de mantenimiento  
 **Estado**  
 Indica el estado de cada trabajo. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentar  
  
-   En ejecución  
  
-   No está en ejecución  
  
 **Trabajo**  
 Nombre del trabajo.  
  
 **Última hora de inicio**  
 Última hora en que se inició el trabajo.  
  
 **Duración**  
 Tiempo durante el que se ha ejecutado el trabajo. El tiempo representa el tiempo transcurrido si el trabajo se está ejecutando y el tiempo total si el trabajo se ha ejecutado anteriormente.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del trabajo.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualización de información y realización de tareas mediante el Monitor de replicación](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
