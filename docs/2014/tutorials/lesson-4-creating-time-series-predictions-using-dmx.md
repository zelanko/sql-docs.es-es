---
title: 'Lección 4: crear predicciones de serie temporal con DMX | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6b883e43-209d-489a-8dc3-9349f88acae8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 772e5f5f71ca82dd18fec48730522c80e907414f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312088"
---
# <a name="lesson-4-creating-time-series-predictions-using-dmx"></a>Lección 4: Creación de predicciones de serie temporal con DMX
  En esta lección y en la lección siguiente, utilizará extensiones de minería de datos (DMX) para crear distintos tipos de predicciones en función de los modelos de serie temporal creados en la [Lección 1: crear un modelo de minería de datos de serie temporal y una estructura](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md) de minería de datos y la [Lección 2: agregar modelos de minería de datos a la estructura de minería](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)de datos de serie temporal.  
  
 Con un modelo de serie temporal, tiene muchas opciones para realizar predicciones:  
  
-   Usar los patrones y datos existentes en el modelo de minería de datos  
  
-   Usar los patrones existentes en el modelo de minería de datos pero suministrar datos nuevos  
  
-   Agregue datos nuevos al modelo o actualice el modelo.  
  
 A continuación se resume la sintaxis para realizar estos tipos de predicción:  
  
 Predicción de serie temporal predeterminada  
 Use [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) para devolver el número especificado de predicciones del modelo de minería de datos entrenado.  
  
 Por ejemplo, consulte [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) o [ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md).  
  
 EXTEND_MODEL_CASES  
 Use [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) con el argumento EXTEND_MODEL_CASES para agregar nuevos datos, ampliar la serie y crear predicciones basadas en el modelo de minería de datos actualizado.  
  
 Este tutorial contiene un ejemplo de cómo utilizar EXTEND_MODEL_CASES.  
  
 REPLACE_MODEL_CASES  
 Use [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) con el argumento REPLACE_MODEL_CASES para reemplazar los datos originales por una nueva serie de datos y, a continuación, cree predicciones basadas en la aplicación de los patrones del modelo de minería de datos a la nueva serie de datos.  
  
 Para obtener un ejemplo de cómo usar REPLACE_MODEL_CASES, vea [Lección 2: generar un escenario de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
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
  
 La lista de selección puede contener columnas del modelo, como el nombre de la línea de producto para la que está creando las predicciones, o las funciones de predicción, como [Lag &#40;dmx&#41;](/sql/dmx/lag-dmx) o [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx), que son específicamente para los modelos de minería de datos de serie temporal.  
  
#### <a name="to-create-a-simple-time-series-prediction-query"></a>Para crear una consulta simple de predicción de serie temporal  
  
1.  En **Explorador de objetos**, haga clic con el botón secundario [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]en la instancia de, seleccione **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     Por:  
  
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
  
     Por:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    WHERE [criteria>]   
    ```  
  
     Por:  
  
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
  
6.  En el menú **archivo** , haga clic en **Guardar DMXQuery1. DMX como**.  
  
7.  En el cuadro de diálogo **Guardar como** , vaya a la carpeta correspondiente y asigne el nombre `SimpleTimeSeriesPrediction.dmx`al archivo.  
  
8.  En la barra de herramientas, haga clic en el botón **Ejecutar** .  
  
     La consulta devuelve seis predicciones para cada una de las dos combinaciones de producto y región que se especifican en la cláusula `WHERE`.  
  
 En la lección siguiente, creará una consulta que proporciona los datos nuevos al modelo y comparará los resultados de esa predicción con la recién creada.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Lección 5: Extensión del modelo de serie temporal](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
  
## <a name="see-also"></a>Consulte también  
 [&#41;PredictTimeSeries &#40;DMX](/sql/dmx/predicttimeseries-dmx)   
 [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)   
 [Ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Lección 2: generar un escenario de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
  
