---
title: Crear predicciones de serie temporal (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 109c4eb07dd34aa5ef3e41d794edfc39ffffcac8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119875"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>Crear predicciones de serie temporal (Tutorial intermedio de minería de datos)
  En las tareas anteriores de esta lección, creó un modelo de serie temporal y exploró los resultados. De forma predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] siempre crea un conjunto de cinco (5) predicciones para un modelo de serie temporal y muestra los valores de predicción como parte del gráfico de pronóstico. Sin embargo, también puede crear predicciones personalizadas si crea consultas de predicción de las extensiones de minería de datos (DMX).  
  
 En esta tarea, creará una consulta de predicción que genera las mismas predicciones que vio en el visor. En esta tarea se supone que el usuario ya ha completado las lecciones del Tutorial básico de minería de datos y está familiarizado con el uso del Generador de consultas de predicción. Ahora obtendrá información sobre la creación de consultas específicas de los modelos de serie temporal.  
  
## <a name="creating-time-series-predictions"></a>Crear predicciones de serie temporal  
 Generalmente, el primer paso para crear una consulta de predicción consiste en seleccionar un modelo de minería de datos y una tabla de entrada. Sin embargo, un modelo de serie temporal no requiere una entrada adicional para una predicción normal. Por consiguiente, no necesita especificar ningún origen de datos nuevo al realizar las predicciones, a menos que esté agregando datos al modelo o reemplazándolos.  
  
 En esta lección, debe especificar el número de pasos de la predicción. Puede especificar el nombre de serie con el fin de obtener una predicción para una combinación determinada de producto y región.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para seleccionar un modelo de minería de datos y una tabla de entrada  
  
1.  En el **predicción de modelo de minería de datos** ficha del Diseñador de minería de datos, en el **Mining Model** cuadro, haga clic en **Seleccionar modelo**.  
  
2.  En el **Seleccionar modelo de minería de datos** cuadro de diálogo, expanda la estructura predicción, seleccione el **Forecasting** del modelo en la lista y, a continuación, haga clic en **Aceptar**.  
  
3.  Omitir la **Seleccionar tabla (s) de entrada** cuadro.  
  
    > [!NOTE]  
    >  En un modelo de serie temporal no necesita especificar ninguna entrada independiente a menos que esté haciendo una predicción cruzada.  
  
4.  En el **origen** columna, en la cuadrícula en el **predicción de modelo de minería de datos** pestaña, haga clic en la celda de la primera fila vacía y, a continuación, seleccione **modelo de minería de datos Forecasting**.  
  
5.  En el **campo** columna, seleccione **Model Region**.  
  
     Esta acción agrega el identificador de la serie a la consulta de predicción para indicar la combinación de modelo y la región a las que se aplica la predicción.  
  
6.  Haga clic en la siguiente fila vacía en el **origen** columna y, a continuación, seleccione **función de predicción**.  
  
7.  En el **campo** columna, seleccione **PredictTimeSeries**.  
  
    > [!NOTE]  
    >  También puede usar la función `Predict` con modelos de serie temporal. Sin embargo, la función de predicción solo crea una predicción para cada serie de forma predeterminada. Por lo tanto, para especificar varios pasos de predicción, debe usar el **PredictTimeSeries** función.  
  
8.  En el **modelo de minería de datos** panel, seleccione la columna del modelo de minería de datos, **cantidad.** Arrastre importe hasta el **criterios o argumentos** cuadro para la **PredictTimeSeries** función que agregó anteriormente.  
  
9. Haga clic en el **criterios o argumentos** cuadro y escriba una coma, seguida de **5**, después del nombre del campo.  
  
     El texto en el **criterios o argumentos** cuadro ahora debería mostrar lo siguiente:  
  
     `[Forecasting].[Amount],5`  
  
10. En el **Alias** columna, escriba `PredictAmount`.  
  
11. Haga clic en la siguiente fila vacía en el **origen** columna y, a continuación, seleccione **función de predicción** nuevo.  
  
12. En el **campo** columna, seleccione **PredictTimeSeries**.  
  
13. En el **Mining Model** panel, seleccione la columna Quantity y, a continuación, arrástrelo el **criterios o argumentos** cuadro para el segundo **PredictTimeSeries** función.  
  
14. Haga clic en el **criterios o argumentos** cuadro y escriba una coma, seguida de **5**, después del nombre del campo.  
  
     El texto en el **criterios o argumentos** cuadro ahora debería mostrar lo siguiente:  
  
     `[Forecasting].[ Quantity],5`  
  
15. En el **Alias** columna, escriba `PredictQuantity`.  
  
16. Haga clic en **cambiar a vista de resultado de consulta**.  
  
     Los resultados de la consulta se muestran en formato tabular.  
  
 Recuerde que creó tres tipos diferentes de resultados en el generador de consultas, uno que usa los valores de una columna y dos que reciben los valores predichos de una función de predicción. Por consiguiente, los resultados de la consulta contienen tres columnas independientes. La primera columna contiene la lista de combinaciones de productos y regiones. La segunda y tercera columnas contienen cada una tabla anidada de los resultados de la predicción. Cada tabla anidada contiene el incremento de tiempo y los valores predichos, como en la siguiente tabla:  
  
 Resultados de ejemplo (las cantidades se truncan a dos decimales):  
  
 **M200 Europa PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|25/7/2008|99978.00|  
|25/8/2008|145575.07|  
|25/9/2008|116835.19|  
|25/10/2008|116537.38|  
|25/11/2008|107760.55|  
  
 **M200 Europa PredictQuantity**  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|25/7/2008|52|  
|25/8/2008|67|  
|25/9/2008|58|  
|25/10/2008|57|  
|25/11/2008|54|  
  
 **M200 Norteamérica - PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|25/7/2008|348533.93|  
|25/8/2008|340097.98|  
|25/9/2008|257986.19|  
|25/10/2008|374658.24|  
|25/11/2008|379241.44|  
  
 **M200 Norteamérica - PredictQuantity**  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|25/7/2008|272|  
|25/8/2008|152|  
|25/9/2008|250|  
|25/10/2008|181|  
|25/11/2008|290|  
  
> [!WARNING]  
>  Las fechas usadas en la base de datos de ejemplo han cambiado en esta versión. Si está usando una versión anterior de los datos de ejemplo, podría ver resultados diferentes.  
  
## <a name="saving-the-prediction-results"></a>Guardar los resultados de una predicción  
 Dispone de varias opciones distintas para usar los resultado de la predicción. Puede simplificar los resultados, copiar los datos desde la vista Resultados y pegarlos en una hoja de cálculo de Excel o en otro archivo.  
  
 Para simplificar el proceso de guardar los resultados, el Diseñador de minería de datos también proporciona la capacidad de guardar los datos en una vista de origen de datos. La funcionalidad de guardar los resultados en una vista del origen de datos solo está disponible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Los resultados solo se puede almacenar en un formato plano.  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>Para quitar información de estructura jerárquica de los resultados en el panel Resultados  
  
1.  En el generador de consultas de predicción, haga clic en **cambiar a vista de diseño de consulta**.  
  
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
  
1.  Haga clic en **guardar resultados de la consulta**.  
  
2.  En el **Guardar resultado de consulta de minería de datos** cuadro de diálogo para **origen de datos**, seleccione [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. También puede crear un origen de datos si desea guardar los datos en una base de datos relacional diferente.  
  
3.  En el **nombre de la tabla** columna, escriba el nombre, de la tabla de un nuevo archivo temporal como **predicciones de prueba**.  
  
4.  Haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Para ver la tabla que creó, cree una conexión al motor de base de datos de la instancia donde guardó los datos y cree una consulta.  
  
## <a name="conclusion"></a>Conclusión  
 Ha aprendido a crear un modelo de serie temporal básico, a interpretar los pronósticos y a crear predicciones.  
  
 Las tareas restantes de este tutorial son opcionales y describen las predicciones de serie temporal avanzadas. Si decide continuar, aprenderá a agregar nuevos datos al modelo y a crear predicciones acerca de la serie extendida. También aprenderá a realizar una predicción cruzada, mediante la tendencia del modelo, pero reemplazará los datos con una nueva serie de datos.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Predicciones de serie temporal de Advanced &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
