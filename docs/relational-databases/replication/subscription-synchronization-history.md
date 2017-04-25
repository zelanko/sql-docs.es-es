---
title: "Suscripción, historial de sincronizaciones | Microsoft Docs"
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
- sql13.rep.monitor.subscription.synchhistory.f1
ms.assetid: 85f666f6-14ee-4f19-b385-e5cc508aabe4
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da555ce4d256a6f4990831c6c7f3a2c2db5997a
ms.lasthandoff: 04/11/2017

---
# <a name="subscription-synchronization-history"></a>Suscripción, historial de sincronizaciones
  La pestaña **Historial de sincronizaciones** muestra información detallada sobre el Agente de mezcla, incluido el estado, las estadísticas de artículos, el historial, mensajes de información y mensajes de error.  
  
## <a name="options"></a>Opciones  
 Seleccione en el menú **Ver** las sesiones del Agente de mezcla que desea ver y después seleccione una sesión específica en la cuadrícula con la etiqueta **Sesiones del Agente de mezcla**. En la cuadrícula con la etiqueta **Artículos procesados en la sesión seleccionada**se muestra información detallada sobre la sesión.  
  
 **Ver**  
 Permite seleccionar las sesiones del Agente de mezcla que desea ver.  
  
 **Estado**  
 Estado del Agente de mezcla al final de la sesión. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Completado  
  
-   Intentando de nuevo  
  
-   En ejecución  
  
 **Start Time**  
 Muestra la hora de inicio de la sesión.  
  
 **Hora de finalización**  
 Muestra la hora de finalización de la sesión. Si no se ha detenido el agente, el campo se mostrará vacío.  
  
 **Duración**  
 Tiempo de ejecución del Agente de mezcla en una sesión. Este tiempo representa el tiempo transcurrido si el agente se está ejecutando actualmente o el tiempo total de ejecución si ya finalizó la ejecución.  
  
 **Comandos cargados**  
 Número de filas cargadas durante la sesión del Agente de mezcla.  
  
 **Comandos descargados**  
 Número de filas descargadas durante la sesión del Agente de mezcla.  
  
 **Mensaje de error**  
 Si la sesión finalizó con un error, este campo muestra el último mensaje de error registrado por el Agente de mezcla. Si la sesión no ha finalizado con error, el campo se mostrará vacío.  
  
 **Artículo**  
 Nombre de cada artículo de la publicación y las siguientes fases de procesamiento para la publicación completa:  
  
-   **Inicialización**. Se refiere a iniciar el Agente de mezcla (no es sinónimo de inicializar una suscripción, que implica aplicar una instantánea).  
  
-   **Cambios de esquema e inserciones masivas**.  
  
-   **Cargar cambios al publicador**.  
  
-   **Descargar cambios al suscriptor**.  
  
 Se incluyen las fases para que la cuadrícula pueda mostrar la cantidad de tiempo y el porcentaje del tiempo total dedicado a cada fase en la sesión seleccionada.  
  
 **% del total**  
 Porcentaje del tiempo total de procesamiento dedicado a cada fase en la sesión seleccionada.  
  
 **Duración**  
 Tiempo dedicado a cada fase de procesamiento. Este tiempo representa el tiempo transcurrido si el Agente de mezcla se está ejecutando actualmente para la sesión y el tiempo total de ejecución si ya finalizó su ejecución.  
  
 **Inserts**  
 Número de filas insertadas en esta fase de la sesión seleccionada.  
  
 **Actualizaciones**  
 Número de filas actualizadas en esta fase de la sesión seleccionada.  
  
 **Eliminaciones**  
 Número de filas eliminadas en esta fase de la sesión seleccionada.  
  
 **Conflictos**  
 Número de conflictos en la sesión seleccionada.  
  
 **Cambios de esquema**  
 Número de cambios de esquema en la sesión seleccionada. Los cambios de esquema pueden ser resultado de: cambios de esquema replicados desde la base de datos de publicación, adición o eliminación de artículos, o cambios de propiedades de un artículo o una publicación.  
  
 **Último mensaje de la sesión seleccionada**  
 Esta área de texto muestra el último mensaje de la sesión seleccionada. Cuando se produce un error se muestra información detallada sobre el error y el comando que se estaba ejecutando. También incluye vínculos a la información adicional relativa al error.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
