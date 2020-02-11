---
title: Predicciones de serie temporal que usan datos actualizados (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2017defaba74071b1a12bee14a5d8907e4c71cda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067561"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>Predicciones de serie temporal que usan datos actualizados (tutorial intermedio de minería de datos)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>Crear predicciones mediante datos extendidos de ventas  
 En esta lección, creará una consulta de predicción que agrega los nuevos datos de ventas al modelo. Al extender el modelo con datos nuevos, puede obtener predicciones actualizadas que incluyan los nuevos puntos de datos.  
  
 La creación de predicciones de serie temporal que usan datos nuevos es fácil: simplemente agregue el parámetro EXTEND_MODEL_CASES a la función [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) , especifique el origen de los nuevos datos y especifique cuántas predicciones desea obtener.  
  
> [!WARNING]  
>  El parámetro EXTEND_MODEL_CASES es opcional; de forma predeterminada, el modelo se amplía en cualquier momento que se crea una consulta de predicción de serie temporal combinando nuevos datos como entradas.  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>Para crear la consulta de predicción y agregar nuevos datos  
  
1.  Si el modelo aún no está abierto, haga doble clic en la estructura de previsión y, en el diseñador de minería de datos, haga clic en la pestaña **predicción de modelo de minería** de datos.  
  
2.  En el panel **modelo de minería de datos** , la previsión del modelo ya debe estar seleccionada. Si no está seleccionada, haga clic en **Seleccionar modelo**y, a continuación, seleccione el modelo, previsión.  
  
3.  En el panel **seleccionar tabla (s) de entrada** , haga clic en **seleccionar tabla de casos**.  
  
4.  En el cuadro de diálogo **seleccionar tabla** , seleccione el origen de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]datos.  
  
     En la lista de vistas del origen de datos, seleccione NewSalesData y, a continuación, haga clic en **Aceptar**.  
  
5.  Haga clic con el botón secundario en la superficie del área de diseño y seleccione **modificar conexiones**.  
  
6.  Mediante el cuadro de diálogo **modificar asignación** , asigne las columnas del modelo a las columnas de los datos externos como se indica a continuación:  
  
    -   Asigne la columna ReportingDate del modelo de minería de datos a la columna NewDate de los datos de entrada.  
  
    -   Asigne la columna amount del modelo de minería de datos a la columna NewAmount de los datos de entrada.  
  
    -   Asigne la columna quantity del modelo de minería de datos a la columna NewQty de los datos de entrada.  
  
    -   Asigne la columna ModelRegion del modelo de minería de datos a la columna de la serie en los datos de entrada.  
  
7.  Ahora creará la consulta de predicción.  
  
     Primero, agregue una columna a la consulta de predicción para generar la serie a la que se aplica la predicción.  
  
    1.  En la cuadrícula, haga clic en la primera fila vacía, en **origen**y, a continuación, seleccione previsión.  
  
    2.  En la columna **campo** , seleccione región del modelo y, en **alias**, escriba `Model Region`.  
  
8.  A continuación, agregue y modifique la función de predicción.  
  
    1.  Haga clic en una fila vacía y, en **origen**, seleccione **función de predicción**.  
  
    2.  En **campo**, seleccione **PredictTimeSeries**.  
  
    3.  En **alias**, escriba **valores predichos**.  
  
    4.  Arrastre la cantidad de campo del panel **modelo de minería de datos** a la columna **criterios o argumento** .  
  
    5.  En la columna **criterios o argumento** , después del nombre del campo, escriba el texto siguiente: **5, EXTEND_MODEL_CASES**  
  
         El texto completo del cuadro de texto **criterios/argumento** debe ser el siguiente:`[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. Haga clic en **resultados** y revise los resultados.  
  
     Las predicciones comienzan en julio (el primer segmento de tiempo después del final de los datos originales) y terminan en noviembre (el quinto segmento de tiempo después del final de los datos originales).  
  
 Puede ver que para usar este tipo de consulta de predicción de forma eficaz, debe saber cuándo finalizan los datos antiguos, así como el número de segmentos de tiempo que están en los nuevos datos.  
  
 Por ejemplo, en este modelo, la serie de datos original finalizaba en junio, y los datos corresponden a los meses de julio, agosto y septiembre.  
  
 Las predicciones que usan EXTEND_MODEL_CASES siempre comienzan por el final de la serie de datos original. Por tanto, si solo desea obtener las predicciones de los meses desconocidos, debe especificar el punto inicial y el punto final para la predicción. Ambos valores se especifican como un número de segmentos de tiempo que comienzan al final de los datos antiguos.  
  
 El siguiente procedimiento muestra cómo hacerlo.  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>Cambiar los puntos inicial y final de las predicciones  
  
1.  En Generador de consultas de predicción, haga clic en **consulta** para cambiar a la vista DMX.  
  
2.  Busque la instrucción DMX que contiene la función PredictTimeSeries y cámbiela de la forma siguiente:  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  Haga clic en **resultados** y revise los resultados.  
  
     Ahora las predicciones comienzan en octubre (el cuarto segmento de tiempo, contando desde el final de los datos originales) y terminan en diciembre (el sexto segmento de tiempo, contando desde el final de los datos originales).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Predicciones de serie temporal que usan datos de reemplazo &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services-minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
