---
title: "Informaci&#243;n de publicaci&#243;n, Advertencias (Publicaci&#243;n transaccional, SQL Server 2005 y posteriores) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.tran.f1"
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Informaci&#243;n de publicaci&#243;n, Advertencias (Publicaci&#243;n transaccional, SQL Server 2005 y posteriores)
  La pestaña **Advertencias** está disponible para los distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. La pestaña **Advertencias** permite realizar las siguientes tareas para la publicación seleccionada:  
  
-   Habilitar las advertencias para mostrarlas en el Monitor de replicación.  
  
-   Especificar umbrales asociados con las advertencias.  
  
-   Definir alertas asociadas con advertencias.  
  
## Advertencias, umbrales y alertas  
 De forma predeterminada, el Monitor de replicación muestra advertencias de suscripciones no inicializadas: se muestra el estado **Suscripción no inicializada** como una advertencia en la columna **Estado** de las páginas que incluyen información de la suscripción. En publicaciones transaccionales, puede especificar si esas condiciones adicionales producen advertencias:  
  
-   Expiración inminente de la suscripción.  
  
     Esta condición se corresponde con la opción **Advertir si una suscripción expirará dentro del umbral**. Si se alcance o supere el umbral especificado, se muestra el estado de la suscripción como **expiración en breve/expirado** (a menos que se debe mostrar un problema con una prioridad más alta).  
  
-   Superar la latencia especificada. Es el tiempo que transcurre entre la confirmación de una transacción en el publicador y la confirmación de la transacción correspondiente en el suscriptor.  
  
     Esto se corresponde con la opción **Advertir si la latencia supera el valor de umbral**. Si se alcance o supere el umbral especificado, se muestra el estado de la suscripción como **rendimiento crítico** (a menos que se debe mostrar un problema con una prioridad más alta). El umbral también se utiliza para proporcionar una clasificación de rendimiento, que se muestra en la columna **Rendimiento** de las páginas que incluyen información de la suscripción. La clasificación de rendimiento tiene uno de los valores siguientes:  
  
    -   Excelente  
  
    -   Bueno  
  
    -   Regular  
  
    -   Insuficiente  
  
    -   Crítico  
  
 Cuando se habilita una advertencia, también se establece un umbral. Por ejemplo, si habilita la advertencia **Advertir si la latencia supera el valor de umbral**, seleccione el tiempo permitido entre que se confirma una transacción en el publicador y la transacción se confirma en el suscriptor.  
  
 Además de mostrar una advertencia en el Monitor de replicación, llegar a un umbral también puede desencadenar una alerta. Para definir alertas, haga clic en **Configurar alertas** y proporcione información en el cuadro de diálogo **Configurar alertas de replicación** .  
  
## Opciones  
 **Habilitado**  
 Seleccione esta opción si desea habilitar una advertencia y especificar un umbral asociado.  
  
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
  
  