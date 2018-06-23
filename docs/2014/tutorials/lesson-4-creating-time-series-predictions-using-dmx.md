---
title: 'Lección 4: Crear predicciones de serie temporal utilizando DMX | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b883e43-209d-489a-8dc3-9349f88acae8
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a345b37d13ade71baad6635cee0508e97d7755eb
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312413"
---
# <a name="lesson-4-creating-time-series-predictions-using-dmx"></a>Lección 4: Crear predicciones de serie temporal con DMX
  En esta lección y en la siguiente lección, utilizará extensiones de minería de datos (DMX) para crear tipos distintos de predicciones basados en los modelos de serie temporal que creó en [lección 1: crear un modelo de minería de datos de serie temporal y su estructura de minería de datos](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)y [lección 2: agregar modelos de minería de datos a la estructura de minería de datos de serie temporal](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md).  
  
 Con un modelo de serie temporal, tiene muchas opciones para realizar predicciones:  
  
-   Usar los patrones y datos existentes en el modelo de minería de datos  
  
-   Usar los patrones existentes en el modelo de minería de datos pero suministrar datos nuevos  
  
-   Agregue datos nuevos al modelo o actualice el modelo.  
  
 A continuación se resume la sintaxis para realizar estos tipos de predicción:  
  
 Predicción de serie temporal predeterminada  
 Use [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) para devolver el número especificado de predicciones del modelo de minería de datos entrenado.  
  
 Por ejemplo, vea [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) o [ejemplos de consultas de modelo de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md).  
  
 EXTEND_MODEL_CASES  
 Use [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) con el argumento EXTEND_MODEL_CASES para agregar datos nuevos, extender la serie y crear predicciones basadas en el modelo de minería de datos actualizado.  
  
 Este tutorial contiene un ejemplo de cómo utilizar EXTEND_MODEL_CASES.  
  
 REPLACE_MODEL_CASES  
 Use [PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx) con el argumento REPLACE_MODEL_CASES para reemplazar los datos originales con una nueva serie de datos y, a continuación, crear predicciones basadas en aplicar los patrones en el modelo de minería de datos a los nuevos datos serie.  
  
 Para obtener un ejemplo de cómo usar REPLACE_MODEL_CASES, vea [lección 2: generar un escenario de previsión &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Crear una consulta para obtener las predicciones predeterminadas según los datos existentes.  
  
 En la lección siguiente, realizará las tareas relacionadas siguientes:  
  
-   Crear una consulta para proporcionar datos nuevos y actualizar las predicciones.  
  
 Además de crear consultas manualmente utilizando DMX, también puede crear predicciones con el generador de consultas de predicción de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="simple-time-series-prediction-query"></a>Consulta simple de predicción de serie temporal  
 El primer paso es utilizar la instrucción `SELECT FROM` junto con la función `PredictTimeSeries` para crear predicciones de serie temporal. Los modelos de serie temporal admiten una sintaxis simplificada para crear predicciones: no es necesario proporcionar ninguna entrada, sino que solo tiene que especificar el número de predicciones que crear. A continuación, se incluye un ejemplo genérico de la instrucción:  
  
```  
SELECT <select list>   
FROM [<mining model name>]   
WHERE [<criteria>]  
```  
  
 La lista de selección puede contener columnas del modelo, como el nombre del producto de línea que se va a crear las predicciones, o funciones de predicción, como [Lag &#40;DMX&#41; ](/sql/dmx/lag-dmx) o [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx), que son específicos para los modelos de minería de datos de serie temporal.  
  
#### <a name="to-create-a-simple-time-series-prediction-query"></a>Para crear una consulta simple de predicción de serie temporal  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], seleccione **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    ```  
  
     La primera línea recupera un valor del modelo de minería de datos que identifica la serie.  
  
     La segunda y tercera líneas utilizan la función `PredictTimeSeries`. Cada línea predice un atributo diferente, `[Quantity]` o `[Amount]`. Los números después de los nombres de los atributos de predicción especifican el número de pasos temporales para realizar la predicción.  
  
     La cláusula `AS` se utiliza con el fin de proporcionar un nombre para la columna que devuelve cada función de predicción. Si no proporciona un alias, de forma predeterminada ambas columnas se devuelven con la etiqueta `Expression`.  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    WHERE [criteria>]   
    ```  
  
     por:  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    FROM   
    [Forecasting_MIXED]  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
6.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
7.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y un nombre al archivo `SimpleTimeSeriesPrediction.dmx`.  
  
8.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve seis predicciones para cada una de las dos combinaciones de producto y región que se especifican en la cláusula `WHERE`.  
  
 En la lección siguiente, creará una consulta que proporciona los datos nuevos al modelo y comparará los resultados de esa predicción con la recién creada.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Lección 5: Extender la serie temporal de modelo](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
  
## <a name="see-also"></a>Vea también  
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)   
 [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)   
 [Ejemplos de consultas de modelo de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Lección 2: Generar un escenario de previsión &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
  
