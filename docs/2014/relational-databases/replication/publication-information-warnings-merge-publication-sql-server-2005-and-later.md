---
title: Información de publicación, advertencias (publicación de mezcla, SQL Server 2005 y versiones posterior) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.warningsandagents.merge.f1
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 789d7beda9396e013438c317f28f5bc80b6c07a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206825"
---
# <a name="publication-information-warnings-merge-publication-sql-server-2005-and-later"></a>Información de publicación, Advertencias (Publicación de combinación, SQL Server 2005 y posterior)
  La pestaña **Advertencias** está disponible para los distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. La pestaña **Advertencias** permite realizar las siguientes tareas para la publicación seleccionada:  
  
-   Habilitar advertencias.  
  
-   Especificar umbrales asociados con las advertencias.  
  
-   Definir alertas asociadas con advertencias.  
  
## <a name="warnings-thresholds-and-alerts"></a>Advertencias, umbrales y alertas  
 De forma predeterminada, el Monitor de replicación muestra advertencias de suscripciones no inicializadas: se muestra el estado **Suscripción no inicializada** como una advertencia en la columna **Estado** de las páginas que incluyen información de la suscripción. Para las publicaciones de combinación puede especificar si las siguientes condiciones adicionales generan advertencias:  
  
-   Expiración inminente de la suscripción.  
  
     Esta condición se corresponde con la opción **Advertir si una suscripción expirará dentro del umbral**. Si se alcanza o se supera el umbral especificado, se muestra el estado de la suscripción como **Con expiración en breve/Expirado** (a menos que tenga que mostrarse un problema con una prioridad superior).  
  
-   Si se supera el tiempo de sincronización especificado.  
  
     Esta condición se corresponde con las opciones **Advertir si la duración de una mezcla para las conexiones de acceso telefónico supera el valor de umbral** y **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**. Es posible establecer el valor de ambos umbrales, pero solo se usará uno de ellos durante la sincronización. El Agente de mezcla aplicará el umbral apropiado en función del tipo de conexión.  
  
     Si se alcanza o supera el umbral especificado, se muestra **Mezcla de ejecución prolongada** como estado de la suscripción (a menos que haya que mostrar un problema de prioridad más alta).  
  
-   Si se produce un error en el procesamiento del número de filas especificado en un período de tiempo determinado.  
  
     Esta condición se corresponde con las opciones **Advertir si el número de filas mezcladas por segundo para las conexiones de acceso telefónico es menor que el valor de umbral** y **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**. Es posible establecer el valor de ambos umbrales, pero solo se usará uno de ellos durante la sincronización. El Agente de mezcla aplicará el umbral apropiado en función del tipo de conexión.  
  
     Si se alcanza o se supera el umbral especificado, se muestra el estado de la suscripción como **Rendimiento crítico** (a menos que tenga que mostrarse un problema con una prioridad superior).  
  
 Cuando se habilita una advertencia, también se establece un umbral. Por ejemplo, si se habilita la advertencia **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**, se debe establecer el tiempo máximo permitido para una sincronización de mezcla.  
  
 Además de mostrar una advertencia en el Monitor de replicación, llegar a un umbral también puede desencadenar una alerta. Para definir alertas, haga clic en **Configurar alertas** y proporcione información en el cuadro de diálogo **Configurar alertas de replicación** .  
  
## <a name="options"></a>Opciones  
 **Habilitado**  
 Seleccione esta opción si desea habilitar una advertencia y especificar un umbral asociado.  
  
 **Alerta**  
 Seleccione esta opción para habilitar el valor de alerta para una advertencia determinada de replicación.  
  
 **Advertencia**  
 Descripción de la advertencia asociada al umbral.  
  
 **Umbral**  
 Permite especificar un valor para el umbral.  
  
 **Configurar alertas**  
 Seleccione una fila en la cuadrícula **Advertencias** y haga clic en **Configurar alertas** para abrir el cuadro de diálogo **Configurar alertas de replicación** . El cuadro de diálogo permite definir una alerta que se asociará al umbral y la advertencia seleccionados.  
  
 **Descartar cambios**  
 Haga clic para descartar los cambios realizados en las advertencias y los umbrales.  
  
> [!NOTE]  
>  Hacer clic en **Descartar cambios** no afecta a las alertas definidas en el cuadro de diálogo **Configurar alertas de replicación** .  
  
 **Guardar cambios**  
 Haga clic para guardar los cambios realizados en las advertencias y los umbrales.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas para una publicación &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitoring Replication](monitoring-replication.md)  (Supervisar la replicación)  
 [Establecer umbrales y advertencias en el Monitor de replicación](monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
