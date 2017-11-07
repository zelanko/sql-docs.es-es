---
title: "Eliminar un modelo de minería de datos de una estructura de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0804f594e1e7f6654bd85ce0e4c08aa9649062ff
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>Eliminar un modelo de minería de datos de una estructura de minería de datos
  Puede utilizar el Diseñador de minería de datos para eliminar los modelos de minería de datos, bien mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o bien mediante instrucciones DMX.  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>Eliminar un modelo de minería de datos mediante las Herramientas de datos de SQL Server  
  
1.  Seleccione la pestaña **Modelos de minería de datos** en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el modelo que quiere eliminar y, después, seleccione **Eliminar**.  
  
     Se abre el cuadro de diálogo **Eliminar objetos** .  
  
3.  Haga clic en **Aceptar**.  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>Eliminar un modelo de minería de datos mediante SQL Server Management Studio  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene el modelo.  
  
2.  Expanda **Estructuras de minería de datos**y, a continuación, expanda **Modelos de minería de datos**.  
  
3.  Haga clic con el botón derecho en el modelo que quiere eliminar y, después, seleccione **Eliminar**.  
  
     Al eliminar el modelo, no se eliminan los datos de entrenamiento, solo los metadatos y los patrones creados al realizar el entrenamiento del modelo.  
  
### <a name="delete-a-mining-model-using-dmx"></a>Eliminar un modelo de minería de datos mediante DMX  
  
-   [DROP MINING MODEL &#40;DMX&#41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  

