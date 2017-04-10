---
title: "Establecer umbrales y advertencias en el Monitor de replicaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "alertas [replicación de SQL Server]"
  - "Agente de mezcla, umbrales y advertencias"
  - "Agente de distribución, umbrales y advertencias"
  - "umbrales [replicación de SQL Server]"
  - "Monitor de replicación, umbrales y advertencias"
  - "supervisar rendimiento [replicación de SQL Server], umbrales y advertencias"
ms.assetid: 3a409c2c-b77e-4001-b81a-1dcd918618ec
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Establecer umbrales y advertencias en el Monitor de replicaci&#243;n
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se muestra información de estado de las publicaciones y suscripciones. De forma predeterminada, en el Monitor de replicación solamente se muestran advertencias de suscripciones no inicializadas, pero puede habilitar advertencias para otras condiciones. Se recomienda habilitar las advertencias para la topología, con el fin de estar puntualmente informado sobre el estado y rendimiento.  
  
 Al habilitar una advertencia, debe especificar un umbral. Cuando se alcanza o se supera ese umbral, aparece la advertencia (a menos que haya un problema de mayor prioridad). Además de mostrar una advertencia en el Monitor de replicación, llegar a un umbral también puede desencadenar una alerta. Se pueden habilitar advertencias para las siguientes condiciones:  
  
-   Expiración inminente de la suscripción  
  
     Se aplica a todos los tipos de replicación. Si se alcance o supere el umbral especificado, se muestra el estado de la suscripción como **expiración en breve/expirado**.  
  
-   Si se supera la latencia especificada (el intervalo de tiempo que transcurre entre la confirmación de una transacción en el publicador y confirmación de la transacción correspondiente en el suscriptor).  
  
     Esto se aplica a la replicación transaccional. Si se alcanza o se supera el umbral especificado, el estado de la suscripción se muestra como **Rendimiento crítico**.  
  
-   Si se supera el tiempo de sincronización especificado.  
  
     Esto se aplica a la replicación de mezcla. Si se alcance o supere el umbral especificado, el estado se muestra como **mezcla de ejecución prolongada**. Puede especificar diferentes umbrales para las conexiones de acceso telefónico y de red de área local (LAN).  
  
-   Si se produce un error en el procesamiento del número de filas especificado en un período de tiempo determinado.  
  
     Esto se aplica a la replicación de mezcla. Si se alcanza o sobrepasa el umbral especificado, el estado se mostrará como **Rendimiento crítico**. Puede especificar diferentes umbrales para las conexiones de acceso telefónico y de LAN.  
  
 Para obtener más información sobre las advertencias **rendimiento crítico** y **mezcla de ejecución prolongada**, consulte [Monitor de rendimiento con el Monitor de replicación](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **En este tema**  
  
-   [Establecer umbrales y advertencias para una publicación transaccional](#Transactional)  
  
-   [Establecer umbrales y advertencias para una publicación de mezcla](#Merge)  
  
-   [Establecer umbrales y advertencias para una publicación de instantánea](#Snapshot)  
  
##  <a name="Transactional"></a> Para establecer umbrales y advertencias para una publicación transaccional  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Advertencias** . Para ver más información acerca de las opciones de esta pestaña, haga clic en **Ayuda** en la barra de menús.  
  
3.  Para habilitar una advertencia, active la casilla apropiada: **Advertir si una suscripción expirará dentro del umbral** o **Advertir si la latencia supera el valor de umbral**.  
  
4.  En la columna **Umbral** , establezca un umbral para las advertencias. Por ejemplo, si activó la casilla **Advertir si la latencia supera el valor de umbral** en el paso 3, puede seleccionar una latencia de **60 segundos** en la columna **Umbral** .  
  
5.  Haga clic en **Guardar cambios**.  
  
#### Para configurar una alerta para un umbral  
  
1.  Haga clic en **Configurar alertas**.  
  
2.  En el cuadro de diálogo **Configurar alertas de replicación** , seleccione una alerta y haga clic en **Configurar**.  
  
     Este cuadro de diálogo muestra alertas para todos los tipos de publicaciones, incluidas las alertas que no están relacionadas con los umbrales de supervisión. Para obtener más información, consulte [usar alertas para eventos del agente de replicación](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Establecer opciones en el **\< NombreAlerta> Propiedades de alerta** cuadro de diálogo:  
  
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.  
  
    -   En el **respuesta** página, especifique si se debe enviar un correo electrónico o se debe ejecutar un trabajo.  
  
    -   En la página **Opciones** , personalice el texto de la respuesta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Haga clic en **Cerrar**.  
  
##  <a name="Merge"></a> Establecer umbrales y advertencias para una publicación de mezcla  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Advertencias** . Para ver más información acerca de las opciones de esta pestaña, haga clic en **Ayuda** en la barra de menús.  
  
3.  Para habilitar una advertencia, active la casilla apropiada:  
  
    -   **Advertir si una suscripción expirará dentro del umbral**  
  
    -   **Advertir si la duración de una mezcla para las conexiones de acceso telefónico supera el valor de umbral**  
  
    -   **Advertir si la duración de una mezcla para las conexiones LAN supera el valor de umbral**  
  
    -   **Advertir si el número de filas mezcladas por segundo para las conexiones LAN es menor que el valor de umbral**  
  
    -   **Advertir si el número de filas mezcladas por segundo para las conexiones de acceso telefónico es menor que el valor de umbral**  
  
4.  En la columna **Umbral** , establezca umbrales para las advertencias. Por ejemplo, si ha activado **Advertir si la duración de una mezcla para las conexiones de acceso telefónico supera el valor de umbral** en el paso 3, en la columna **Umbral** debe seleccionar un tiempo de **10 minutos** .  
  
5.  Haga clic en **Guardar cambios**.  
  
#### Para configurar una alerta para un umbral  
  
1.  Haga clic en **Configurar alertas**.  
  
2.  En el cuadro de diálogo **Configurar alertas de replicación** , seleccione una alerta y haga clic en **Configurar**.  
  
     Este cuadro de diálogo muestra alertas para todos los tipos de publicaciones, incluidas las alertas que no están relacionadas con los umbrales de supervisión.  
  
3.  Establecer opciones en el **\< NombreAlerta> Propiedades de alerta** cuadro de diálogo:  
  
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.  
  
    -   En el **respuesta** página, especifique si se debe enviar un correo electrónico o se debe ejecutar un trabajo.  
  
    -   En la página **Opciones** , personalice el texto de la respuesta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Haga clic en **Cerrar**.  
  
##  <a name="Snapshot"></a> Establecer umbrales y advertencias para una publicación de instantánea  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Advertencias** . Para ver más información acerca de las opciones de esta pestaña, haga clic en **Ayuda** en el menú superior.  
  
3.  Para habilitar una advertencia, active la casilla **Advertir si una suscripción expirará dentro del umbral**.  
  
4.  En la columna **Umbral** , establezca un umbral para la advertencia. Por ejemplo, puede seleccionar un valor de **70%** en la columna **Umbral** .  
  
5.  Haga clic en **Guardar cambios**.  
  
#### Para configurar una alerta para un umbral  
  
1.  Haga clic en **Configurar alertas**.  
  
2.  En el cuadro de diálogo **Configurar alertas de replicación** , seleccione una alerta y haga clic en **Configurar**.  
  
     Este cuadro de diálogo muestra alertas para todos los tipos de publicaciones, incluidas las alertas que no están relacionadas con los umbrales de supervisión. Para obtener más información, consulte [usar alertas para eventos del agente de replicación](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Establecer opciones en el **\< NombreAlerta> Propiedades de alerta** cuadro de diálogo:  
  
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.  
  
    -   En el **respuesta** página, especifique si se debe enviar un correo electrónico o se debe ejecutar un trabajo.  
  
    -   En la página **Opciones** , personalice el texto de la respuesta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Haga clic en **Cerrar**.  
  
## Vea también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  