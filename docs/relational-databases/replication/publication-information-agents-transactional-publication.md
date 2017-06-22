---
title: "Información de publicación, Agentes (Publicación transaccional) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a1e666793719f1a277fffe23d02d4a6630585f61
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="publication-information-agents-transactional-publication"></a>Información de publicación, Agentes (Publicación transaccional)
  La pestaña **Agentes** muestra información resumida de los agentes para la publicación seleccionada. La información del Agente de instantáneas y el Agente de registro del LOG se muestra para todas las publicaciones transaccionales. La información del Agente de lectura de cola se muestra para las publicaciones transaccionales que están habilitadas para las suscripciones de actualización en cola.  
  
## <a name="options"></a>Opciones  
 Para obtener información más detallada y las tareas relacionadas con un agente, haga clic con el botón secundario en la fila de ese agente y, a continuación, haga clic en una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene en una o más columnas en el cuadro de diálogo **Ordenar columnas** .  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se mostrarán y el orden en el que se mostrarán en el cuadro de diálogo **Elegir columnas** .  
  
-   **Filtro**: filtre filas en la cuadrícula basándose en los valores de columna en el cuadro de diálogo **Configuración del filtro** .  
  
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
 Nombre de cada agente de replicación asociado con la publicación. El Agente de distribución está asociado con suscripciones a esta publicación. Para obtener más información, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
 **Última hora de inicio**  
 Hora en la que se inició el agente por última vez.  
  
 **Duración**  
 Tiempo durante el que se ha ejecutado el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [View Information and Perform Tasks for a Publication &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  (Ver información y realizar tareas para una publicación [Monitor de replicación])  
 [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
