---
title: "Actualizar datos en el Monitor de replicaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "actualizar datos"
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Actualizar datos en el Monitor de replicaci&#243;n
  En el Monitor de replicación, la ventana principal y las ventanas de detalles (las ventanas que se inician desde la ventana principal) se pueden actualizar automática o manualmente. Para actualizar una ventana manualmente, presione F5. De manera predeterminada, la ventana principal se actualiza automáticamente cada cinco segundos; este valor se puede personalizar para cada publicador.  
  
 Los datos mostrados en el Monitor de replicación se consultan desde una memoria caché; Para obtener información sobre la relación entre la memoria caché y actualizar el Monitor de replicación, consulte [almacenamiento en caché, actualizar y supervisar el rendimiento de replicación](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md). Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### Para establecer las opciones de actualización del Monitor de replicación  
  
1.  Haga clic en un publicador en el panel izquierdo del Monitor de replicación y, a continuación, haga clic en **Configuración del publicador**.  
  
2.  En el cuadro de diálogo **Configuración del publicador** , establezca las opciones **Actualizar automáticamente** y **Frecuencia de actualización** . El valor establecido en **Actualizar automáticamente** afecta a la ventana principal del Monitor de replicación. El **frecuencia de actualización** configuración también afecta a las ventanas de detalle que se establecen para actualizar automáticamente (cambios en la configuración solo afecta a las ventanas de detalles abiertas después del cambio).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para especificar que una ventana de detalles se actualice automáticamente  
  
1.  Abra una ventana de detalles en el Monitor de replicación. Por ejemplo:  
  
    1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
    2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
    3.  Haga clic en una suscripción y, a continuación, haga clic en **Ver detalles**.  
  
2.  En el **suscripción \< SubscriptionName>** ventana de detalles, haga clic en **acción**, y, a continuación, haga clic en **actualización automática**. La frecuencia de actualización es establece con el valor que se especifique en **Frecuencia de actualización** en el cuadro de diálogo **Configuración del publicador** .  
  
## Vea también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  