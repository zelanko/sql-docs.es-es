---
description: contenedor de tarea
title: Contenedor del host de la tarea | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd2ab8fe157992077618f426f68931c8c87d8ed7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496007"
---
# <a name="task-host-container"></a>contenedor de tarea

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El contenedor del host de la tarea encapsula una tarea individual. En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , el host de la tarea no se configura por separado, sino al establecer las propiedades de la tarea que encapsula. Para obtener más información sobre las tareas encapsuladas por los contenedores del host de la tarea, vea [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md).  
  
 Este contenedor extiende el uso las de variables y los controladores de eventos al nivel de tarea. Para obtener más información, vea [Controladores de eventos de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md) y [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="configuration-of-the-task-host"></a>Configuración del host de la tarea  
 Puede establecer propiedades en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o mediante programación.  
  
 Para obtener información sobre cómo establecer estas propiedades en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vea [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
 Para obtener información sobre cómo establecer mediante programación estas propiedades, vea <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Consulte también  
 [Contenedores de Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  
