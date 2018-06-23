---
title: Predicciones de serie usan datos actualizados (Tutorial intermedio de datos minería) temporal | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3478a52657e26fa8e376e88bc83a5c4d9813cdc8
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312363"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>Predicciones de serie temporal que usan datos actualizados (tutorial intermedio de minería de datos)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>Crear predicciones mediante datos extendidos de ventas  
 En esta lección, creará una consulta de predicción que agrega los nuevos datos de ventas al modelo. Al extender el modelo con datos nuevos, puede obtener predicciones actualizadas que incluyan los nuevos puntos de datos.  
  
 Crear predicciones de serie temporal que usan los nuevos datos es fácil: basta con agregar el parámetro EXTEND_MODEL_CASES a la [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) función, especifique el origen de los nuevos datos y especifique cuántos predicciones que desea obtener.  
  
> [!WARNING]  
>  El parámetro EXTEND_MODEL_CASES es opcional; de forma predeterminada, el modelo se amplía en cualquier momento que se crea una consulta de predicción de serie temporal combinando nuevos datos como entradas.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>Para crear la consulta de predicción y agregar nuevos datos  
  
1.  Si el modelo no está abierto, haga doble clic en la estructura predicción y en el Diseñador de minería de datos, haga clic en el **predicción de modelo de minería de datos** ficha.  
  
2.  En el **Mining Model** panel, el modelo de pronóstico ya debería estar seleccionado. Si no está seleccionada, haga clic en **Seleccionar modelo**y, a continuación, seleccione el modelo de pronóstico.  
  
3.  En el **Seleccionar tabla (s) de entrada** panel, haga clic en **Seleccionar tabla de casos**.  
  
4.  En el **Seleccionar tabla** cuadro de diálogo, seleccione el origen de datos, [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
     En la lista de vistas del origen de datos, seleccione NewSalesData y, a continuación, haga clic en **Aceptar**.  
  
5.  Haga clic en la superficie del área de diseño y seleccione **modificar conexiones**.  
  
6.  Mediante el **modificar asignación** diálogo cuadro, asigne las columnas en el modelo a las columnas de los datos externos como sigue:  
  
    -   Asignar la columna ReportingDate en el modelo de minería de datos a la columna NewDate en los datos de entrada.  
  
    -   Asignar la columna de cantidad en el modelo de minería de datos a la columna NewAmount en los datos de entrada.  
  
    -   Asignar la columna Quantity en el modelo de minería de datos a la columna NewQty en los datos de entrada.  
  
    -   Asignar la columna ModelRegion en el modelo de minería de datos a la columna de serie en los datos de entrada.  
  
7.  Ahora creará la consulta de predicción.  
  
     Primero, agregue una columna a la consulta de predicción para generar la serie a la que se aplica la predicción.  
  
    1.  En la cuadrícula, haga clic en la primera fila vacía bajo **origen**y, a continuación, seleccione Forecasting.  
  
    2.  En el **campo** columna, seleccione Model Region y para **Alias**, tipo `Model Region`.  
  
8.  A continuación, agregue y modifique la función de predicción.  
  
    1.  Haga clic en una fila vacía y en **origen**, seleccione **función de predicción**.  
  
    2.  Para **campo**, seleccione **PredictTimeSeries**.  
  
    3.  Para **Alias**, tipo **valores predichos**.  
  
    4.  Arrastre el campo cantidad de la **Mining Model** panel en el **criterios o argumento** columna.  
  
    5.  En el **criterios o argumento** columna, después del nombre de campo, escriba el siguiente texto: **5, EXTEND_MODEL_CASES**  
  
         El texto completo de la **criterios o argumento** cuadro de texto debe ser como sigue: `[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. Haga clic en **resultados** y revise los resultados.  
  
     Las predicciones comienzan en julio (el primer segmento de tiempo después del final de los datos originales) y terminan en noviembre (el quinto segmento de tiempo después del final de los datos originales).  
  
 Puede ver que para usar este tipo de consulta de predicción de forma eficaz, debe saber cuándo finalizan los datos antiguos, así como el número de segmentos de tiempo que están en los nuevos datos.  
  
 Por ejemplo, en este modelo, la serie de datos original finalizaba en junio, y los datos corresponden a los meses de julio, agosto y septiembre.  
  
 Las predicciones que usan EXTEND_MODEL_CASES siempre comienzan por el final de la serie de datos original. Por tanto, si solo desea obtener las predicciones de los meses desconocidos, debe especificar el punto inicial y el punto final para la predicción. Ambos valores se especifican como un número de segmentos de tiempo que comienzan al final de los datos antiguos.  
  
 El siguiente procedimiento muestra cómo hacerlo.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>Cambiar los puntos inicial y final de las predicciones  
  
1.  En el generador de consultas de predicción, haga clic en **consulta** para cambiar a la vista DMX.  
  
2.  Busque la instrucción DMX que contiene la función PredictTimeSeries y cámbiela de la forma siguiente:  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  Haga clic en **resultados** y revise los resultados.  
  
     Ahora las predicciones comienzan en octubre (el cuarto segmento de tiempo, contando desde el final de los datos originales) y terminan en diciembre (el sexto segmento de tiempo, contando desde el final de los datos originales).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Usar datos de reemplazo de predicciones de serie temporal &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Contenido del modelo para los modelos de serie temporal de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
