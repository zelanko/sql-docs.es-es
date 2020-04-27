---
title: Cuadro de diálogo convertir al modelo de implementación de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dfe1f6e5b752284b6bb0feec96f4f3dfd67cc4f6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060349"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>Convertir a modelo de implementación de paquetes, cuadro de diálogo
  El comando de **Convertir a modelo de implementación de paquetes** permite convertir un paquete al modelo de implementación de paquetes después de comprobar el proyecto y cada paquete en el proyecto para ver la compatibilidad con ese modelo. Si un paquete usa las características exclusivas del modelo de implementación de proyectos, como los parámetros, el paquete no se podrá convertir.  
  
## <a name="task-list"></a>Lista de tareas  
 Para convertir un paquete al modelo de implementación de paquetes es preciso realizar dos pasos.  
  
1.  Cuando se selecciona el comando **Convertir a modelo de implementación de paquetes** en el menú **Proyecto** , el proyecto y cada paquete se comprueban para ver su compatibilidad con este modelo. Los resultados se muestran en tabla **Resultados** .  
  
     Si el proyecto o un paquete no supera la prueba de compatibilidad, haga clic en **Error** en la columna **Resultado** para obtener más información. Haga clic en **Guardar informe** para guardar una copia de esta información en un archivo de texto.  
  
2.  Si el proyecto y todos los paquetes superan la prueba de compatibilidad, haga clic **Aceptar** para convertir el paquete.  
  
> [!NOTE]  
>  Para convertir un proyecto al modelo de implementación de paquetes, use el **Asistente para conversión de proyectos de Integration Services**. Para más información, consulte [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md).  
  
## <a name="see-also"></a>Consulte también  
 [Implementación de proyectos y paquetes](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [Implementación de paquetes &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Asistente para conversión de proyectos de Integration Services](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
