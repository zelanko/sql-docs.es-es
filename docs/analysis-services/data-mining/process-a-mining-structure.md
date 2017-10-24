---
title: "Procesar una estructura de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2e9c6f31a8701571b2d9be03eecd34050757e7a7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="process-a-mining-structure"></a>Procesar una estructura de minería de datos
  Para poder examinar o trabajar con los modelos de minería de datos asociados a una estructura de minería de datos, se debe implementar el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y procesar la estructura y los modelos de minería de datos. Además, si realiza un cambio en la estructura o los modelos de minería de datos, se le solicitará que vuelva a implementarlos y procesarlos. Al procesar la estructura en la pestaña **Estructura de minería de datos** del Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] se procesan todos los modelos asociados.  
  
 Puede procesar una estructura de minería de datos mediante estas herramientas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: comando Process  
  
 Para obtener información sobre cómo procesar modelos individuales, vea [Procesar un modelo de minería de datos](../../analysis-services/data-mining/process-a-mining-model.md).  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>Para procesar una estructura de minería de datos y todos los modelos asociados a las herramientas de datos de SQL Server  
  
1.  Seleccione **Procesar estructura de minería de datos y todos los modelos** en la opción de menú **Modelo de minería de datos** en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
     Si ha realizado cambios en la estructura, se le pedirá que vuelva a implementar la estructure antes de procesar los modelos. Haga clic en **Sí**.  
  
2.  Haga clic en **ejecutar** en el **procesar estructura de minería de datos - \<estructura >** cuadro de diálogo.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar los detalles del procesamiento del modelo.  
  
3.  Haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** cuando el procesamiento de los modelos se haya completado.  
  
4.  Haga clic en **cerrar** en el **procesar estructura de minería de datos - \<estructura >** cuadro de diálogo.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  

