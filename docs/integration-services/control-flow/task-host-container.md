---
title: "Contenedor de tarea | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.taskhostcontainer.f1"
helpviewer_keywords: 
  - "contenedores [Integration Services], host de tarea"
  - "contenedor de tarea"
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
caps.latest.revision: 45
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# Contenedor de tarea
  El contenedor del host de la tarea encapsula una tarea individual. En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , el host de la tarea no se configura por separado, sino al establecer las propiedades de la tarea que encapsula. Para obtener más información sobre las tareas encapsuladas por los contenedores del host de la tarea, vea [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md).  
  
 Este contenedor extiende el uso las de variables y los controladores de eventos al nivel de tarea. Para obtener más información, vea [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md) y [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## Configuración del host de la tarea  
 Puede establecer propiedades en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o mediante programación.  
  
 Para obtener información sobre cómo establecer estas propiedades en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vea [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
 Para obtener información sobre cómo establecer mediante programación estas propiedades, vea <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>.  
  
## Tareas relacionadas  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Vea también  
 [Contenedores de Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  