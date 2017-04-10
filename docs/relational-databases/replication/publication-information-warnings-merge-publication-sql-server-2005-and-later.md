---
title: "Informaci&#243;n de publicaci&#243;n, Advertencias (Publicaci&#243;n de combinaci&#243;n, SQL Server 2005 y posterior) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.merge.f1"
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Informaci&#243;n de publicaci&#243;n, Advertencias (Publicaci&#243;n de combinaci&#243;n, SQL Server 2005 y posterior)
  La pestaña **Advertencias** está disponible para los distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. La pestaña **Advertencias** permite realizar las siguientes tareas para la publicación seleccionada:  
  
-   Habilitar advertencias.  
  
-   Especificar umbrales asociados con las advertencias.  
  
-   Definir alertas asociadas con advertencias.  
  
## Advertencias, umbrales y alertas  
 De forma predeterminada, el Monitor de replicación muestra advertencias de suscripciones no inicializadas: se muestra el estado **Suscripción no inicializada** como una advertencia en la columna **Estado** de las páginas que incluyen información de la suscripción. Para las publicaciones de combinación puede especificar si las siguientes condiciones adicionales generan advertencias:  
  
-   Expiración inminente de la suscripción.  
  
     Esta condición se corresponde con la opción **Advertir si una suscripción expirará dentro del umbral**. Si se alcance o supere el umbral especificado, se muestra el estado de la suscripción como **expiración en breve/expirado** (a menos que se debe mostrar un problema con una prioridad más alta).  
  
-   Si se supera el tiempo de sincronización especificado.  
  
     Esta condición se corresponde con las opciones **Advertir si la duración de una mezcla para las conexiones de acceso telefónico supera el valor de umbral** y **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**. Es posible establecer el valor de ambos umbrales, pero solo se usará uno de ellos durante la sincronización. El Agente de mezcla aplicará el umbral apropiado en función del tipo de conexión.  
  
     Si se alcance o supere el umbral especificado, se muestra el estado de la suscripción como **mezcla de ejecución prolongada** (a menos que se debe mostrar un problema con una prioridad más alta).  
  
-   Si se produce un error en el procesamiento del número de filas especificado en un período de tiempo determinado.  
  
     Esta condición se corresponde con las opciones **Advertir si el número de filas mezcladas por segundo para las conexiones de acceso telefónico es menor que el valor de umbral** y **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**. Es posible establecer el valor de ambos umbrales, pero solo se usará uno de ellos durante la sincronización. El Agente de mezcla aplicará el umbral apropiado en función del tipo de conexión.  
  
     Si se alcance o supere el umbral especificado, se muestra el estado de la suscripción como **rendimiento crítico** (a menos que se debe mostrar un problema con una prioridad más alta).  
  
 Cuando se habilita una advertencia, también se establece un umbral. Por ejemplo, si se habilita la advertencia **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**, se debe establecer el tiempo máximo permitido para una sincronización de mezcla.  
  
 Además de mostrar una advertencia en el Monitor de replicación, llegar a un umbral también puede desencadenar una alerta. Para definir alertas, haga clic en **Configurar alertas** y proporcione información en el cuadro de diálogo **Configurar alertas de replicación** .  
  
## Opciones  
 **Habilitado**  
 Seleccione esta opción si desea habilitar una advertencia y especificar un umbral asociado.  
  
 **Alerta**  
 Seleccione esta opción para habilitar el valor de alerta para una advertencia determinada de replicación.  
  
 **Advertencia**  
 Descripción de la advertencia asociada al umbral.  
  
 **Umbral**  
 Permite especificar un valor para el umbral.  
  
 **Configurar alertas**  
 Seleccione una fila en la **advertencias** cuadrícula y haga clic en **Configurar alertas** para iniciar el **Configurar alertas de replicación** cuadro de diálogo. El cuadro de diálogo permite definir una alerta que se asociará al umbral y la advertencia seleccionados.  
  
 **Descartar cambios**  
 Haga clic para descartar los cambios realizados en las advertencias y los umbrales.  
  
> [!NOTE]  
>  Haga clic en **Descartar cambios** no afecta a las alertas definidos en el **Configurar alertas de replicación** cuadro de diálogo.  
  
 **Guardar cambios**  
 Haga clic para guardar los cambios realizados en las advertencias y los umbrales.  
  
## Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver la información y realizar tareas para una publicación & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Supervisar el rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Establecer umbrales y advertencias en el Monitor de replicación](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  