---
title: Probar la exactitud con gráficos de elevación (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 864f255556063ea5011e3d3954294edcbdd9cb5b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329008"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>Probar la exactitud con gráficos de mejora respecto al modelo predictivo (Tutorial básico de minería de datos)
  En el **gráfico de precisión de minería de datos** ficha del Diseñador de minería de datos, puede calcular el grado en cada uno de los modelos realiza predicciones y comparar los resultados de cada modelo directamente en los resultados de los otros modelos. Este método de comparación se conoce como un *gráfico de elevación*. Normalmente, la exactitud de la predicción de un modelo de minería de datos se cuantifica mediante la mejora respecto al modelo predictivo o la exactitud de la clasificación. En este tutorial utilizaremos solamente el gráfico de mejora respecto al modelo predictivo.  
  
 En este tema, realizará las tareas siguientes:  
  
-   [Elija los datos de entrada](#BKMK_InputData)  
  
-   [Configurar parámetros del gráfico de precisión](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a> Elección de los datos de entrada  
 El primer paso a la hora de probar la precisión de los modelos de minería de datos consiste en seleccionar el origen de datos que usará para realizar las pruebas. Probará la exactitud de los modelos con sus datos de prueba y, a continuación, los utilizará con datos externos.  
  
#### <a name="to-select-the-data-set"></a>Para seleccionar el conjunto de datos  
  
1.  Cambie a la **gráfico de precisión de minería de datos** ficha en el Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y seleccione el **selección de entrada** ficha.  
  
2.  En el cuadro de grupo **Seleccionar un conjunto de datos para usarlo en un gráfico de precisión** , seleccione **Usar casos de prueba de estructura de minería de datos**. Estos son los datos de prueba que separó cuando creó la estructura de minería de datos.  
  
     Para obtener más información sobre las otras opciones, consulte [elegir un tipo de gráfico de precisión y establecer opciones de gráfico](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
##  <a name="BKMK_Selecting"></a> Establecer los parámetros del gráfico de precisión  
 Para crear un gráfico de precisión, debe definir tres cosas:  
  
-   ¿Qué modelos debe incluir en el gráfico de precisión?  
  
-   ¿Qué atributo de predicción desea medir? Algunos modelos pueden tener varios objetivos, pero cada gráfico solo puede medir un resultado cada vez.  
  
     Para utilizar una columna como el **nombre de columna de predicción** en un gráfico de precisión, las columnas deben tener el tipo de uso de `Predict` o `Predict Only`. Además, el tipo de contenido de la columna de destino debe ser `Discrete` o `Discretized`. Es decir, no puede medir la precisión en salidas numéricas continuas con el gráfico de elevación.  
  
-   Desea medir la precisión general del modelo, o su precisión para predecir un valor concreto (por ejemplo [Bike Buyer] = ‘Yes’)  
  
#### <a name="to-generate-the-lift-chart"></a>Para generar el gráfico de elevación  
  
1.  En la pestaña **Selección de entrada** del Diseñador de minería de datos, en **Seleccione las columnas del modelo de minería de datos de predicción que se mostrarán en el gráfico de elevación**, active la casilla correspondiente a **Sincronizar valores y columnas de predicción**.  
  
2.  En la columna **Nombre de columna de predicción** , compruebe que **Bike Buyer** está seleccionado para cada modelo.  
  
3.  En la columna **Mostrar** , seleccione cada uno de los modelos.  
  
     De forma predeterminada, todos los modelos de la estructura de minería de datos aparecen seleccionados. Puede decidir no incluir un modelo específico, pero para este tutorial deje todos los modelos seleccionados.  
  
4.  En la columna **Valor de predicción** , seleccione **1**. El mismo valor se rellena automáticamente para cada modelo que tiene la misma columna de predicción.  
  
5.  Seleccione el **gráfico de elevación** ficha.  
  
     Al hacer clic en la pestaña, se ejecuta una consulta de predicción para obtener predicciones de los datos de prueba, y se comparan los resultados con los valores conocidos. Los resultados se trazan en el gráfico.  
  
     Si especifica un resultado objetivo determinado mediante la **valor de predicción** opción, el gráfico de elevación traza los resultados de suposiciones aleatorias y los resultados de un modelo ideal.  
  
    -   La línea de suposición aleatoria muestra cuál sería el grado de precisión del modelo sin utilizar ningún dato para informar de sus predicciones: es decir, una división 50-50 entre dos resultados. El gráfico de elevación ayuda a visualizar la mejora del funcionamiento del modelo con respecto a una estimación aleatoria.  
  
    -   La línea del modelo ideal representa el límite superior de precisión. Muestra el beneficio máximo posible que podría conseguir si el modelo siempre hiciera sus predicciones con precisión.  
  
     Los modelos de minería de datos que creó estarán normalmente entre estos dos extremos. Cualquier mejora con respecto a la estimación aleatoria se considera *elevación*.  
  
6.  Utilice la leyenda para buscar las líneas coloreadas que representan el modelo ideal y el modelo de suposición aleatoria.  
  
     Observará que el `TM_Decision_Tree` modelo proporciona la máxima elevación, superando a los modelos de la agrupación en clústeres y Bayes Naive.  
  
 Para obtener una explicación detallada de un gráfico de elevación similar a la que se creó en esta lección, vea [gráfico de elevación &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Probar un modelo filtrado &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Gráfico de elevación &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [Pestaña gráfico de elevación &#40;vista Gráfico de precisión de minería de datos&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
