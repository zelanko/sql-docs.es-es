---
title: Procesar una estructura de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50882400f085d00f8e9fd13e1e1532cf62105947
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733278"
---
# <a name="process-a-mining-structure"></a>Procesar una estructura de minería de datos
  Para poder examinar o trabajar con los modelos de minería de datos asociados a una estructura de minería de datos, se debe implementar el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y procesar la estructura y los modelos de minería de datos. Además, si realiza un cambio en la estructura o los modelos de minería de datos, se le solicitará que vuelva a implementarlos y procesarlos. Al procesar la estructura en la pestaña **Estructura de minería de datos** del Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] se procesan todos los modelos asociados.  
  
 Puede procesar una estructura de minería de datos mediante estas herramientas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: Process, comando  
  
 Para obtener información sobre cómo procesar modelos individuales, vea [Procesar un modelo de minería de datos](process-a-mining-model.md).  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>Para procesar una estructura de minería de datos y todos los modelos asociados a las herramientas de datos de SQL Server  
  
1.  Seleccione **Procesar estructura de minería de datos y todos los modelos** en la opción de menú **Modelo de minería de datos** en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
     Si ha realizado cambios en la estructura, se le pedirá que vuelva a implementar la estructure antes de procesar los modelos. Haga clic en **Sí**.  
  
2.  Haga clic en **ejecutar** en el **procesando estructura de minería de datos - \<estructura >** cuadro de diálogo.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar los detalles del procesamiento del modelo.  
  
3.  Haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** cuando el procesamiento de los modelos se haya completado.  
  
4.  Haga clic en **cerrar** en el **procesando estructura de minería de datos - \<estructura >** cuadro de diálogo.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](mining-structure-tasks-and-how-tos.md)  
  
  
