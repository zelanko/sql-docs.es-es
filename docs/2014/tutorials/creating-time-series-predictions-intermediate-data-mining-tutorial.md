---
title: Crear predicciones de serie temporal (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca1aa4022931c78f6139a8058c05adc707af5e77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63313888"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>Crear predicciones de serie temporal (Tutorial intermedio de minería de datos)
  En las tareas anteriores de esta lección, creó un modelo de serie temporal y exploró los resultados. De forma predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] siempre crea un conjunto de cinco (5) predicciones para un modelo de serie temporal y muestra los valores de predicción como parte del gráfico de pronóstico. Sin embargo, también puede crear predicciones personalizadas si crea consultas de predicción de las extensiones de minería de datos (DMX).  
  
 En esta tarea, creará una consulta de predicción que genera las mismas predicciones que vio en el visor. En esta tarea se supone que el usuario ya ha completado las lecciones del Tutorial básico de minería de datos y está familiarizado con el uso del Generador de consultas de predicción. Ahora obtendrá información sobre la creación de consultas específicas de los modelos de serie temporal.  
  
## <a name="creating-time-series-predictions"></a>Crear predicciones de serie temporal  
 Generalmente, el primer paso para crear una consulta de predicción consiste en seleccionar un modelo de minería de datos y una tabla de entrada. Sin embargo, un modelo de serie temporal no requiere una entrada adicional para una predicción normal. Por consiguiente, no necesita especificar ningún origen de datos nuevo al realizar las predicciones, a menos que esté agregando datos al modelo o reemplazándolos.  
  
 En esta lección, debe especificar el número de pasos de la predicción. Puede especificar el nombre de serie con el fin de obtener una predicción para una combinación determinada de producto y región.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para seleccionar un modelo de minería de datos y una tabla de entrada  
  
1.  En la pestaña **predicción de modelo de minería** de datos del diseñador de minería de datos, en el cuadro modelo de **minería** de datos, haga clic en **Seleccionar modelo**.  
  
2.  En el cuadro de diálogo **Seleccionar modelo de minería de datos** , expanda la estructura previsión, seleccione el modelo de **previsión** en la lista y, a continuación, haga clic en **Aceptar**.  
  
3.  Omita el cuadro **seleccionar tabla (s) de entrada** .  
  
    > [!NOTE]  
    >  En un modelo de serie temporal no necesita especificar ninguna entrada independiente a menos que esté haciendo una predicción cruzada.  
  
4.  En la columna **origen** , en la cuadrícula de la pestaña **predicción de modelo de minería de datos** , haga clic en la celda de la primera fila vacía y, a continuación, seleccione modelo de minería de datos de **previsión**.  
  
5.  En la columna **campo** , seleccione **región del modelo**.  
  
     Esta acción agrega el identificador de la serie a la consulta de predicción para indicar la combinación de modelo y la región a las que se aplica la predicción.  
  
6.  Haga clic en la siguiente fila vacía de la columna **origen** y, a continuación, seleccione **función de predicción**.  
  
7.  En la columna **campo** , seleccione **PredictTimeSeries**.  
  
    > [!NOTE]  
    >  También puede usar la función `Predict` con modelos de serie temporal. Sin embargo, la función de predicción solo crea una predicción para cada serie de forma predeterminada. Por lo tanto, para especificar varios pasos de predicción, debe usar la función **PredictTimeSeries** .  
  
8.  En el panel **modelo de minería de datos** , seleccione la columna del modelo de minería de datos **amount.** Arrastre amount hasta el cuadro **criterios o argumentos** de la función **PredictTimeSeries** que agregó anteriormente.  
  
9. Haga clic en el cuadro **criterios y argumentos** y escriba una coma seguida de **5**, después del nombre del campo.  
  
     El texto del cuadro **criterios o argumentos** ahora debería mostrar lo siguiente:  
  
     `[Forecasting].[Amount],5`  
  
10. En la columna **alias** , escriba `PredictAmount`.  
  
11. Haga clic en la siguiente fila vacía de la columna **origen** y, a continuación, vuelva a seleccionar la **función de predicción** .  
  
12. En la columna **campo** , seleccione **PredictTimeSeries**.  
  
13. En el panel **modelo de minería de datos** , seleccione la columna quantity y arrástrela al cuadro **criterios o argumentos** de la segunda función **PredictTimeSeries** .  
  
14. Haga clic en el cuadro **criterios y argumentos** y escriba una coma seguida de **5**, después del nombre del campo.  
  
     El texto del cuadro **criterios o argumentos** ahora debería mostrar lo siguiente:  
  
     `[Forecasting].[ Quantity],5`  
  
15. En la columna **alias** , escriba `PredictQuantity`.  
  
16. Haga clic en **cambiar a vista de resultado de consulta**.  
  
     Los resultados de la consulta se muestran en formato tabular.  
  
 Recuerde que creó tres tipos diferentes de resultados en el generador de consultas, uno que usa los valores de una columna y dos que reciben los valores predichos de una función de predicción. Por consiguiente, los resultados de la consulta contienen tres columnas independientes. La primera columna contiene la lista de combinaciones de productos y regiones. La segunda y tercera columnas contienen cada una tabla anidada de los resultados de la predicción. Cada tabla anidada contiene el incremento de tiempo y los valores predichos, como en la siguiente tabla:  
  
 Resultados de ejemplo (las cantidades se truncan a dos decimales):  
  
 **M200 Europe PredictAmount**  
  
|$TIME|Importe|  
|-----------|------------|  
|7/25/2008|99978,00|  
|8/25/2008|145575,07|  
|9/25/2008|116835,19|  
|10/25/2008|116537,38|  
|11/25/2008|107760,55|  
  
 **M200 Europe PredictQuantity**  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|7/25/2008|52|  
|8/25/2008|67|  
|9/25/2008|58|  
|10/25/2008|57|  
|11/25/2008|54|  
  
 **M200 Norteamérica-PredictAmount**  
  
|$TIME|Importe|  
|-----------|------------|  
|7/25/2008|348533,93|  
|8/25/2008|340097,98|  
|9/25/2008|257986,19|  
|10/25/2008|374658,24|  
|11/25/2008|379241,44|  
  
 **M200 Norteamérica-PredictQuantity**  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|7/25/2008|272|  
|8/25/2008|152|  
|9/25/2008|250|  
|10/25/2008|181|  
|11/25/2008|290|  
  
> [!WARNING]  
>  Las fechas usadas en la base de datos de ejemplo han cambiado en esta versión. Si está usando una versión anterior de los datos de ejemplo, podría ver resultados diferentes.  
  
## <a name="saving-the-prediction-results"></a>Guardar los resultados de una predicción  
 Dispone de varias opciones distintas para usar los resultado de la predicción. Puede simplificar los resultados, copiar los datos desde la vista Resultados y pegarlos en una hoja de cálculo de Excel o en otro archivo.  
  
 Para simplificar el proceso de guardar los resultados, el Diseñador de minería de datos también proporciona la capacidad de guardar los datos en una vista de origen de datos. La funcionalidad de guardar los resultados en una vista del origen de datos solo está disponible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Los resultados solo se puede almacenar en un formato plano.  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>Para quitar información de estructura jerárquica de los resultados en el panel Resultados  
  
1.  En el Generador de consultas de predicción, haga clic en **cambiar a vista de diseño de consulta**.  
  
     La vista cambia para permitir la modificación manual del texto de las consultas DMX.  
  
2.  Escriba la palabra clave `FLATTENED` después de la palabra clave `SELECT`. El texto completo de la consulta debería ser como sigue:  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    ```  
  
3.  Opcionalmente, puede escribir una cláusula para restringir los resultados, como en el ejemplo siguiente:  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    WHERE [Forecasting].[Model Region] = 'M200 North America'   
    OR [Forecasting].[Model Region] = 'M200 Europe'  
  
    ```  
  
4.  Haga clic en **cambiar a vista de resultado de consulta**.  
  
#### <a name="to-export-prediction-query-results"></a>Para exportar los resultados de una consulta de predicción  
  
1.  Haga clic en **Guardar resultados**de la consulta.  
  
2.  En el cuadro de diálogo **Guardar resultado de consulta de minería de datos** , en [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]origen de **datos**, seleccione. También puede crear un origen de datos si desea guardar los datos en una base de datos relacional diferente.  
  
3.  En la columna **nombre de tabla** , escriba un nuevo nombre de tabla temporal, como **predicciones de prueba**.  
  
4.  Haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Para ver la tabla que creó, cree una conexión al motor de base de datos de la instancia donde guardó los datos y cree una consulta.  
  
## <a name="conclusion"></a>Conclusión  
 Ha aprendido a crear un modelo de serie temporal básico, a interpretar los pronósticos y a crear predicciones.  
  
 Las tareas restantes de este tutorial son opcionales y describen las predicciones de serie temporal avanzadas. Si decide continuar, aprenderá a agregar nuevos datos al modelo y a crear predicciones acerca de la serie extendida. También aprenderá a realizar una predicción cruzada, mediante la tendencia del modelo, pero reemplazará los datos con una nueva serie de datos.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Predicciones de serie temporal avanzadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
