---
title: Cuadro de diálogo Replicación de SQL Server ' información del publicador ' | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 344b899905e844312ee6e5a66455fc2fa14b446f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63462517"
---
# <a name="sql-server-replication-publisher-information-dialog-box"></a>Replicación de SQL Server cuadro de diálogo ' información del publicador '
  La pestaña **Publicaciones** proporciona información de resumen para todas las publicaciones del publicador seleccionado en el panel izquierdo.  
  
## <a name="options"></a>Opciones  
 Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene en una o más columnas en el cuadro de diálogo **Ordenar columnas** .  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se mostrarán y el orden en el que se mostrarán en el cuadro de diálogo **Elegir columnas** .  
  
-   **Filtro**: filtre filas en la cuadrícula basándose en los valores de columna en el cuadro de diálogo **Configuración del filtro** .  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Estado**  
 Estado de cada publicación que se determina mediante el estado de prioridad más alto de sus suscripciones. De forma predeterminada, la cuadrícula que contiene información de publicación se ordena por la columna **Estado** . La siguiente lista muestra los posibles valores de estado y el orden de los valores (por ejemplo, los errores siempre se muestran en la parte superior de la cuadrícula).  
  
-   Error  
  
-   Rendimiento crítico  
  
-   Reintentando comando con errores  
  
-   Aceptar  
  
 El valor de estado **Rendimiento crítico** es importante para las suscripciones transaccionales y de mezcla; en el caso de las suscripciones transaccionales, este valor solamente se puede mostrar si se establece un umbral. Para obtener información sobre la medición del rendimiento y el establecimiento de umbrales, vea [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md) y [Establecer umbrales y advertencias en el Monitor de replicación](monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Publicación**  
 El nombre de cada publicación, con el formato *nombreDeBaseDeDatosDePublicación: nombreDePublicación*.  
  
 **Suscripciones**  
 El número de suscripciones para cada publicación.  
  
 **Sincronizando**  
 El número de suscripciones para cada publicación que se están sincronizando actualmente.  
  
-   Para la replicación transaccional, "sincronizando" significa que el Agente de distribución está en ejecución, pero que no necesariamente se está creando una replicación de los datos.  
  
-   Para la replicación de mezcla, "sincronizando" significa que el Agente de mezcla está en ejecución y que se está creando una replicación de los datos.  
  
-   Para la replicación de instantáneas, "sincronizando" significa que el Agente de distribución está en ejecución y que se está creando una replicación de los datos.  
  
 **Rendimiento medio actual** y **Peor rendimiento actual**  
 Solo para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Clasificación de rendimiento medio y clasificación de peor rendimiento, respectivamente, correspondientes a todas las suscripciones de una publicación. Las clasificaciones se basan en las medidas más recientes tomadas por el Monitor de replicación y no reflejan el rendimiento posterior de una suscripción.  
  
 En la replicación transaccional, el Monitor de replicación solamente muestra un valor para las publicaciones cuyos umbrales de rendimiento están definidos. Si no se han definido umbrales de rendimiento para una publicación, en esta columna se muestra **No habilitado**. En la replicación de mezcla, el Monitor de replicación muestra un valor una vez que se han producido cinco sincronizaciones con al menos 50 cambios en cada una a través del mismo tipo de conexión (de acceso telefónico o LAN). Si ha habido menos de cinco sincronizaciones con al menos 50 cambios, o la sincronización más reciente tiene menos de 50 cambios, está columna está en blanco.  
  
 La clasificación de rendimiento tiene uno de los valores siguientes:  
  
-   Excelente  
  
-   Bueno  
  
-   Regular  
  
-   Insuficiente  
  
-   Crítico  
  
 Para obtener más información sobre cómo se definen las clasificaciones de rendimiento y cómo se establecen los umbrales de rendimiento, vea [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md).  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas mediante el monitor de replicación](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Supervisar la replicación](monitoring-replication.md)  
  
  
