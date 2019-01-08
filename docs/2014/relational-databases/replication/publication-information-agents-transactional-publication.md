---
title: Información de publicación, Agentes (Publicación transaccional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68996f64bd61d96b4a2938a9711519207861fcd3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52780367"
---
# <a name="publication-information-agents-transactional-publication"></a>Información de publicación, Agentes (Publicación transaccional)
  La pestaña **Agentes** muestra información resumida de los agentes para la publicación seleccionada. La información del Agente de instantáneas y el Agente de registro del LOG se muestra para todas las publicaciones transaccionales. La información del Agente de lectura de cola se muestra para las publicaciones transaccionales que están habilitadas para las suscripciones de actualización en cola.  
  
## <a name="options"></a>Opciones  
 Para obtener información más detallada y las tareas relacionadas con un agente, haga clic con el botón secundario en la fila de ese agente y, a continuación, haga clic en una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenación**: Ordenar por una o varias columnas en el **ordenar columnas** cuadro de diálogo.  
  
-   **Elegir columnas para mostrar**: Seleccionar qué columnas desea mostrar y el orden en que se mostrarán en el **Elegir columnas** cuadro de diálogo.  
  
-   **Filtro**: Filtrar las filas en la cuadrícula basándose en valores de columna en la **configuración del filtro** cuadro de diálogo.  
  
-   **Borrar filtro**: Borre cualquier configuración de la cuadrícula de filtro.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Estado**  
 Estado de cada agente de replicación asociado con la publicación. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Reintentando comandos con errores  
  
-   No está en ejecución  
  
-   En ejecución  
  
-   Completada  
  
 **Agente**  
 Nombre de cada agente de replicación asociado con la publicación. El Agente de distribución está asociado con suscripciones a esta publicación. Para obtener más información, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
 **Última hora de inicio**  
 Hora en la que se inició el agente por última vez.  
  
 **Duración**  
 Tiempo durante el que se ha ejecutado el agente. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Última acción**  
 La última acción realizada durante la ejecución más reciente del agente.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [View Information and Perform Tasks for a Publication &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  (Ver información y realizar tareas para una publicación [Monitor de replicación])  
 [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Supervisar la replicación](monitoring-replication.md)  
  
  
