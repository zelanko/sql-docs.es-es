---
title: 'Lección 2: Generar un escenario de previsión (Tutorial de minería de datos intermedios) | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time series [Analysis Services]
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 9a988156-c900-4c22-97fa-f6b0c1aea9e2
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 94f73737c1d67a69c4b740371c578b2f41d97a13
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312353"
---
# <a name="lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial"></a>Lección 2: generar un escenario de pronóstico (Tutorial intermedio de minería de datos)
  Como analista de ventas de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], se le ha solicitado un pronóstico de las ventas de productos para el próximo año. En concreto, se le ha solicitado que compare las previsiones de las distintas regiones y líneas de productos. Además, debe determinar si las ventas de diferentes productos varían en función de la época del año.  
  
 Para hallar la información solicitada, en esta lección resumirá los datos de ventas mensuales de la compañía y también resumirá las cifras de ventas en tres regiones: Europa, Norteamérica y Pacífico.  
  
 Una vez que haya completado las tareas de esta lección, podrá responder a las preguntas siguientes:  
  
-   ¿Cómo cambian las ventas de los diferentes modelos de bicicleta a lo largo del año?  
  
-   ¿Hay diferencias entre los patrones de ventas en las tres regiones?  
  
-   ¿Podemos predecir picos de ventas?  
  
 La lección se puede completar en dos partes:  
  
-   La primera parte presenta los conceptos básicos de cómo crear y usar un modelo de serie temporal.  
  
-   La segunda parte le guía por la creación de un modelo general de series temporales basándose en todas las regiones. Puede usar este modelo general para la *predicción cruzada*.  
  
 Para completar las tareas en esta lección, que se enumeran a continuación, utilizará el [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] del origen de datos que haya creado en [lección 1: crear la solución de minería de datos intermedio &#40;Tutorial intermedio de minería de datos&#41; ](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md).  
  
> [!WARNING]  
>  Las fechas en el [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] base de datos de ejemplo se han actualizado para esta versión. Si usa una versión anterior de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], puede crear el modelo según estos pasos, pero podría ver resultados diferentes.  
  
 **Crear un modelo de pronóstico Simple**  
  
-   [Agregar datos de una vista del origen para la predicción &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
-   [Crear una estructura de previsión y un modelo &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Modificar la estructura de previsión &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
-   [Personalizar y procesar el modelo de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [Explorar el modelo de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [Crear predicciones de serie temporal &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
 **Crear un modelo de pronóstico General para la predicción cruzada**  
  
-   [Predicciones de serie temporal de Advanced &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
-   [Usan datos actualizados de predicciones de serie temporal &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
-   [Usar datos de reemplazo de predicciones de serie temporal &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
-   [Comparar las predicciones para modelos de predicción &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Agregar datos de una vista del origen para la predicción &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
 [Descripción de los requisitos para las Series temporales modelo &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>Todas las lecciones  
 [Lección 1: Crear la solución de minería de datos intermedia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 Lección 2: Escenario de pronóstico (tutorial intermedio de minería de datos)  
  
 [Lección 3: Generar un escenario de cesta &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 4: Generar un escenario de agrupación en clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [Lección 5: Generar modelos de regresión logística y Red neuronal &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tutorial de minería de datos básicos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Intermedio de Tutorial de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  