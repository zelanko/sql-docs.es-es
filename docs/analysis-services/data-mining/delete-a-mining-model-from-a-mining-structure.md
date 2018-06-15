---
title: Eliminar un modelo de minería de datos de una estructura de minería de datos | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b17489213e0f057d8f291095f01b65f97a977ff1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019322"
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>Eliminar un modelo de minería de datos de una estructura de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
-   [ELIMINAR MODELO DE MINERÍA DE DATOS & #40; DMX & #41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
