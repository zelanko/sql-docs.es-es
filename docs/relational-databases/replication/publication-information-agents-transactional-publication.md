---
title: Información de publicación, Agentes (Publicación transaccional) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e538d324fdd9ce6d17a5583af573711a82b2d946
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133427"
---
# <a name="publication-information-agents-transactional-publication"></a>Información de publicación, Agentes (Publicación transaccional)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La pestaña **Agentes** muestra información resumida de los agentes para la publicación seleccionada. La información del Agente de instantáneas y el Agente de registro del LOG se muestra para todas las publicaciones transaccionales. La información del Agente de lectura de cola se muestra para las publicaciones transaccionales que están habilitadas para las suscripciones de actualización en cola.  
  
## <a name="options"></a>Opciones  
 Para obtener información más detallada y las tareas relacionadas con un agente, haga clic con el botón secundario en la fila de ese agente y, a continuación, haga clic en una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene por una o más columnas en el cuadro de diálogo **Ordenar columnas**.  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se van a mostrar y el orden en el que lo harán en el cuadro de diálogo **Elegir columnas**.  
  
-   **Filtro**: filtre las filas de la cuadrícula en función de los valores de columna del cuadro de diálogo **Configuración del filtro**.  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Estado**  
 Estado de cada agente de replicación asociado con la publicación. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentando comandos con errores  
  
-   No está en ejecución  
  
-   En ejecución  
  
-   Completado  
  
 **Agente**  
 Nombre de cada agente de replicación asociado con la publicación. El Agente de distribución está asociado con suscripciones a esta publicación. Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Última hora de inicio**  
 Hora en la que se inició el agente por última vez.  
  
 **Duración**  
 Tiempo durante el que se ha ejecutado el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication.md)  
 [Visualización de información y realización de tareas mediante el Monitor de replicación](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
  
