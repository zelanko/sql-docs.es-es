---
title: Agregar un modelo de regresión logística a la estructura de centro de llamadas (Tutorial de minería de datos intermedios) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ccadf7665b112b6ba1055fdcf69aeb99609c3ab3
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312434"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>Agregar un modelo de regresión logística a la estructura de centro de llamadas (Tutorial intermedio de minería de datos)
  Además de analizar los factores que pueden influir en las operaciones del centro de llamadas, se le pidió que proporcionara recomendaciones concretas sobre la manera en que el personal puede mejorar la calidad de servicio. En esta tarea usará la misma estructura de minería de datos con la que creó el modelo de exploración y agregará un modelo de minería de datos que después se usará para crear predicciones.  
  
 En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], un modelo de regresión logística se basa en el algoritmo de redes neuronales, lo que ofrece la misma flexibilidad y eficacia que un modelo de red neuronal. Sin embargo, la regresión logística es especialmente adecuada para predecir resultados binarios.  
  
 En este escenario, usará la misma estructura de minería de datos que utilizó para el modelo de red neuronal. Sin embargo, personalizará el nuevo modelo para abordar las cuestiones empresariales. Le interesa la mejora de la calidad de servicio y determinar cuántos operadores experimentados necesita; para ello, configurará el modelo para predecir esos valores.  
  
 Para asegurarse de que todos los modelos basados en los datos del centro de llamadas se parecen lo más posible, usará el mismo valor de inicialización que antes. Al establecer el parámetro de inicialización se garantiza que el modelo procesa los datos a partir del mismo punto inicial, y se minimizan las variaciones causadas por las anomalías en los datos.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>Para agregar un nuevo modelo de minería de datos a la estructura de minería de datos del centro de llamadas  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos, **Call Center Binned**y seleccione **abrir diseñador**.  
  
2.  En el Diseñador de minería de datos, haga clic en el **modelos de minería de datos** ficha.  
  
3.  Haga clic en **crear un modelo de minería de datos relacionadas**.  
  
4.  En el **nuevo modelo de minería de datos** cuadro de diálogo para **nombre del modelo**, tipo `Call Center - LR`.  Para **nombre del algoritmo**, seleccione **regresión logística de Microsoft**.  
  
5.  Haga clic en **Aceptar**.  
  
     El nuevo modelo de minería de datos se muestra en el **modelos de minería de datos** ficha.  
  
### <a name="to-customize-the-logistic-regression-model"></a>Para personalizar el modelo de regresión logística  
  
1.  En la columna para el nuevo modelo de minería de datos, `Call Center - LR`, mantenga Fact CallCenter ID como la clave.  
  
2.  Cambie el valor de ServiceGrade y Level Two Operators a **Predict**.  
  
     Ambas columnas se usarán como entrada y para la predicción. Básicamente, crea dos modelos independientes en los mismos datos: uno que predice el número de operadores y otro que predice la calificación del servicio.  
  
3.  Cambiar todas las demás columnas a **entrada**.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>Para especificar el valor de inicialización y procesar los modelos  
  
1.  En el **Mining Model** pestaña, haga clic en la columna del modelo denominado Call Center - LR y seleccione **establecer parámetros de algoritmo**.  
  
2.  En la fila correspondiente al parámetro HOLDOUT_SEED, haga clic en la celda vacía situada debajo **valor**y el tipo de `1`. Haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  El valor de inicialización que elija no es importante siempre y cuando use el mismo para todos los modelos relacionados.  
  
3.  En el **modelos de minería de datos** menú, seleccione **procesar estructura de minería de datos y todos los modelos**. Haga clic en **Sí** para implementar el proyecto de minería de datos actualizados en el servidor.  
  
4.  En el **modelo de minería de datos de proceso** cuadro de diálogo, haga clic en **ejecutar**.  
  
5.  Haga clic en **cerrar** para cerrar el **progreso del proceso** cuadro de diálogo y, a continuación, haga clic en **cerrar** en el **modelo de minería de datos de proceso** cuadro de diálogo.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear predicciones para los modelos de centro de llamadas &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  