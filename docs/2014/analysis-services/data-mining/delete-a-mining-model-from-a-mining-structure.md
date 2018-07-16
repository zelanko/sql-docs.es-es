---
title: Eliminar un modelo de minería de datos de una estructura de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b5d2a4500de682ecf9d0745c472d793ac4848235
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319445"
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
  
-   [MODELO DE MINERÍA DE DATOS DE COLOCACIÓN &AMP;#40;DMX&AMP;#41;](/sql/dmx/drop-mining-model-dmx)  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
  
