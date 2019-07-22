---
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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bd17e43afa06ba954b092c6f6a5f95a74d21faaf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011203"
---
# <a name="task-host-container"></a>contenedor de tarea

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
  
