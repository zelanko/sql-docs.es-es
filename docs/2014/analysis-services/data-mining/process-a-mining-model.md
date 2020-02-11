---
title: Procesar un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], processing
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd2506e835f634937d5bf135ed7eec7cfa259b5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083098"
---
# <a name="process-a-mining-model"></a>Procesar un modelo de minería de datos
  En la pestaña Modelos de minería de datos del Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede procesar un modelo de minería de datos específico que esté asociado a una estructura de minería de datos, o bien, procesar todos los modelos que estén asociados con la estructura.  
  
 Puede procesar un modelo de minería de datos utilizando las siguientes herramientas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 También puede utilizar un comando XMLA Process. Para más información, vea [Herramientas y enfoques de procesamiento &#40;Analysis Services&#41;](../multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>Procesar un modelo de minería de datos mediante las Herramientas de datos de SQL Server  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, seleccione un modelo en la columna o columnas de modelos de la cuadrícula.  
  
2.  En el menú **Modelo de minería de datos** , seleccione **Procesar modelo**.  
  
     Si ha realizado cambios a la estructura de minería de datos, se le pedirá que vuelva a implementar la estructura antes de procesar el modelo. Haga clic en **Sí**.  
  
3.  En el cuadro de diálogo **procesando>de modelo de \<minería de datos** , haga clic en **Ejecutar**.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo.  
  
4.  Una vez que haya finalizado el procesamiento del modelo correctamente, haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** .  
  
5.  Haga clic en **cerrar** en el cuadro de diálogo **procesando modelo de minería de datos \<:>del modelo** .  
  
 Solo se han procesado la estructura y el modelo de minería de datos seleccionado.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>Procesar todos los modelos de minería de datos asociados a una estructura de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, seleccione la opción **Procesar estructura de minería de datos y todos los modelos** en el menú **Modelo de minería de datos** .  
  
2.  Si ha realizado cambios a la estructura de minería de datos, se le pedirá que vuelva a implementar la estructura antes de procesar los modelos. Haga clic en **Sí**.  
  
3.  En el cuadro de diálogo **procesando>estructura \<de minería de datos** , haga clic en **Ejecutar**.  
  
4.  Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo.  
  
5.  Una vez que haya finalizado el procesamiento de todos los modelos correctamente, haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** .  
  
6.  Haga clic en **cerrar** en el cuadro de diálogo **>del modelo de procesamiento \<** .  
  
 Se han procesado la estructura y todos los modelos de minería de datos asociados.  
  
## <a name="see-also"></a>Consulte también  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
  
