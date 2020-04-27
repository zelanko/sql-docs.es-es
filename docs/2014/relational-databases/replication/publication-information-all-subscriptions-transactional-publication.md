---
title: Información de publicación, Todas las suscripciones (Publicación transaccional) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.allsubscriptions.tran.f1
ms.assetid: 7073350c-f667-4f70-88e9-152c9a1b08dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6cc3ae7c4c39517f40b49d2ddd98ccdc397ee345
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63021818"
---
# <a name="publication-information-all-subscriptions-transactional-publication"></a>Información de publicación, Todas las suscripciones (Publicación transaccional)
  La pestaña **Todas las suscripciones** muestra información de todas las suscripciones a la publicación transaccional seleccionada.  
  
## <a name="options"></a>Opciones  
 Para obtener información más detallada y las tareas de una suscripción, haga clic con el botón secundario en la fila de dicha suscripción y, a continuación, haga clic en una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene en una o más columnas en el cuadro de diálogo **Ordenar columnas** .  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se mostrarán y el orden en el que se mostrarán en el cuadro de diálogo **Elegir columnas** .  
  
-   **Filtro**: filtre filas en la cuadrícula basándose en los valores de columna en el cuadro de diálogo **Configuración del filtro** .  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Mostrar**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Seleccione los estados de la suscripción que se mostrarán para el tipo de suscripción seleccionado. Por ejemplo, puede seleccionar mostrar solo aquellas suscripciones que tienen errores.  
  
 **Estado**  
 Es el estado de cada suscripción, determinado por el estado del Agente de distribución o el Agente de registro del LOG (se muestra el estado de prioridad más alto; el estado también se puede determinar mediante el Agente de lectura de cola si se utilizan suscripciones de actualización en cola).  
  
 De forma predeterminada, la cuadrícula que contiene la información de suscripción está ordenada por la columna **Estado** (y, a continuación, por la columna **Rendimiento** de las suscripciones con el mismo estado). La siguiente lista muestra los valores de estado posibles y el criterio de ordenación de los valores (por ejemplo, los errores se muestran siempre en la parte superior de la cuadrícula).  
  
-   Error  
  
-   Rendimiento crítico (solo para[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores)  
  
-   Con expiración en breve/Expirado (solo para[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores)  
  
-   Suscripción no inicializada (solo para[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores)  
  
-   Reintentando comando con errores  
  
-   No está en ejecución  
  
-   En ejecución  
  
 El criterio de clasificación también determina qué valor se muestra si una misma suscripción presenta varios estados. Por ejemplo, si una suscripción tiene un error y expirará en breve, la columna **Estado** muestra **Error**.  
  
 Los valores de estado **Rendimiento crítico**, **Con expiración en breve/Expirado**y **Suscripción no inicializada** son advertencias. Cuando se muestra una advertencia, también aparece la columna **Estado** si un agente está ejecutándose. Por ejemplo, el estado podría ser **En ejecución, Rendimiento crítico**.  
  
 Los valores de estado **Rendimiento crítico** y **Con expiración en breve/Expirado** se muestran únicamente si se establecen umbrales. Para obtener información sobre la medición del rendimiento y el establecimiento de umbrales, vea [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md) y [Establecer umbrales y advertencias en el Monitor de replicación](monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Suscripción**  
 Muestra el nombre de cada suscripción, en el formato: *nombreDeSuscriptor: nombreDeBaseDeDatosDeSuscripción*.  
  
 **Rendimiento**  
 Solo para[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. La clasificación del rendimiento para cada suscripción se basa en las medidas más recientes tomadas por el Monitor de replicación y no refleja el rendimiento histórico. El rendimiento se mide para suscripciones a publicaciones que tienen definidos umbrales de rendimiento; si una publicación no tiene umbrales de rendimiento definidos, esta columna muestra **No habilitado**. La clasificación de rendimiento tiene uno de los valores siguientes:  
  
-   Excelente  
  
-   Bueno  
  
-   Regular  
  
-   Insuficiente  
  
-   Crítico  
  
 Si el rendimiento es crítico, se muestra **Rendimiento crítico** en la columna **Estado** . Para obtener más información sobre cómo se definen las clasificaciones de rendimiento y cómo se establecen los umbrales de rendimiento, vea [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md).  
  
 **Latencia**  
 Solo para[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Muestra el tiempo promedio que transcurre entre la confirmación de una transacción en el publicador y la confirmación de la transacción correspondiente en el suscriptor. La latencia que se muestra se basa en las mediciones más recientes realizadas por el Monitor de replicación. Para obtener más información sobre cómo medir la latencia, vea [Medir la latencia y validar las conexiones de la replicación transaccional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar el monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas mediante el monitor de replicación](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Supervisión de la replicación](monitoring-replication.md)  
  
  
