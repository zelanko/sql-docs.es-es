---
title: Procesar un modelo de minería de datos | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bfc8d22ff87f467fa89d178d46b422918aa4dd6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34017922"
---
# <a name="process-a-mining-model"></a>Procesar un modelo de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En la pestaña Modelos de minería de datos del Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede procesar un modelo de minería de datos específico que esté asociado a una estructura de minería de datos, o bien, procesar todos los modelos que estén asociados con la estructura.  
  
 Puede procesar un modelo de minería de datos utilizando las siguientes herramientas:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 También puede utilizar un comando XMLA Process. Para más información, vea [Herramientas y enfoques de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>Procesar un modelo de minería de datos mediante las Herramientas de datos de SQL Server  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, seleccione un modelo en la columna o columnas de modelos de la cuadrícula.  
  
2.  En el menú **Modelo de minería de datos** , seleccione **Procesar modelo**.  
  
     Si ha realizado cambios a la estructura de minería de datos, se le pedirá que vuelva a implementar la estructura antes de procesar el modelo. Haga clic en **Sí**.  
  
3.  En el **procesar modelo de minería de datos - \<modelo >** cuadro de diálogo, haga clic en **ejecutar**.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo.  
  
4.  Una vez que haya finalizado el procesamiento del modelo correctamente, haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** .  
  
5.  Haga clic en **cerrar** en el **procesar modelo de minería de datos - \<modelo >** cuadro de diálogo.  
  
 Solo se han procesado la estructura y el modelo de minería de datos seleccionado.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>Procesar todos los modelos de minería de datos asociados a una estructura de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, seleccione la opción **Procesar estructura de minería de datos y todos los modelos** en el menú **Modelo de minería de datos** .  
  
2.  Si ha realizado cambios a la estructura de minería de datos, se le pedirá que vuelva a implementar la estructura antes de procesar los modelos. Haga clic en **Sí**.  
  
3.  En el **procesar estructura de minería de datos - \<estructura >** cuadro de diálogo, haga clic en **ejecutar**.  
  
4.  Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo.  
  
5.  Una vez que haya finalizado el procesamiento de todos los modelos correctamente, haga clic en **Cerrar** en el cuadro de diálogo **Progreso del proceso** .  
  
6.  Haga clic en **cerrar** en el **procesamiento \<modelo >** cuadro de diálogo.  
  
 Se han procesado la estructura y todos los modelos de minería de datos asociados.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
