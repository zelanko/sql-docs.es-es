---
title: 'Lección 2: agregar modelos de minería de datos a la estructura de minería de datos de serie temporal | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ae0bb91fafb53c0c077a4e0d82558b550d0e6070
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62855716"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de serie temporal
  En esta lección, agregará un nuevo modelo de minería de datos a la estructura de minería de datos que acaba de crear en la [Lección 1: crear un modelo de minería de datos de serie temporal y una estructura de minería](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)de datos.  
  
## <a name="alter-mining-structure-statement"></a>Instrucción ALTER MINING STRUCTURE  
 Para agregar un nuevo modelo de minería de datos a una estructura de minería de datos existente, use la instrucción [ALTER Mining structure &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) . El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Identificación de la estructura de minería de datos  
  
-   Asignación de un nombre al modelo de minería de datos  
  
-   Definición de la columna de clave  
  
-   Definición de las columnas de predicción  
  
-   Especificación de los cambios de parámetros y el algoritmo  
  
 A continuación, se incluye un ejemplo genérico de la instrucción ALTER MINING STRUCTURE:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 La primera línea de código identifica la estructura de minería de datos existente a la que se agregarán los modelos de minería de datos:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 La siguiente línea de código asigna un nombre al modelo de minería de datos que se agregará a la estructura de minería de datos:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Para obtener información sobre cómo asignar un nombre a un objeto en DMX, consulte [identifiers &#40;dmx&#41;](/sql/dmx/identifiers-dmx).  
  
 Las líneas siguientes del código definen columnas de la estructura de minería de datos que utilizará el modelo de minería de datos:  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 Solo puede utilizar columnas que ya existan en la estructura de minería de datos, y la primera columna de la lista debe ser la columna de clave de la estructura.  
  
 La siguiente línea de código define el algoritmo de minería de datos que genera el modelo de minería de datos y los parámetros del algoritmo que puede establecer en el algoritmo, y especifica si puede obtener detalles a partir del modelo en la vista detallada de los datos en los casos de entrenamiento:  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 Para obtener más información sobre los parámetros de algoritmo que puede ajustar, vea [referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Puede especificar que una columna del modelo de minería de datos se utilice para la predicción mediante la sintaxis siguiente:  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Agregar un modelo de minería de datos de serie temporal nuevo a la estructura.  
  
-   Cambiar los parámetros del algoritmo para utilizar un método de análisis y predicción diferente  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>Agregar un modelo de serie temporal ARIMA a la estructura  
 El primer paso es agregar un nuevo modelo de minería de datos de pronóstico a la estructura existente. De forma predeterminada, el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] crea los modelos de minería de datos de serie temporal utilizando dos algoritmos, ARIMA y ARTXP, y mezclando los resultados. Sin embargo, puede especificar un único algoritmo que utilizar o la mezcla exacta de algoritmos. En este paso, agregará un modelo nuevo que utiliza solo el algoritmo ARIMA. Este algoritmo está optimizado para la predicción a largo plazo.  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>Para agregar un modelo de minería de datos de serie temporal ARIMA  
  
1.  En **Explorador de objetos**, haga clic con el botón secundario [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]en la instancia de, seleccione **nueva consulta**y, a continuación, haga clic en **DMX** para abrir el editor de consultas y una nueva consulta en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción ALTER MINING STRUCTURE en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    <key columns>,  
    ```  
  
     por:  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     Observe que no necesita repetir ninguna información del tipo de contenido o tipo de datos que proporcionó en la instrucción CREATE MINING MODEL, porque esta información ya está almacenada en la estructura de minería de datos.  
  
6.  Reemplace lo siguiente:  
  
    ```  
    <mining model columns>  
    ```  
  
     por:  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  Reemplace lo siguiente:  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     Ahora, la instrucción resultante debería ser como sigue:  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  En el menú **archivo** , haga clic en **Guardar DMXQuery1. DMX como**.  
  
9. En el cuadro de diálogo **Guardar como** , vaya a la carpeta correspondiente y asigne el nombre `Forecasting_ARIMA.dmx`al archivo.  
  
10. En la barra de herramientas, haga clic en el botón **Ejecutar** .  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>Agregar un modelo de serie temporal ARTXP a la estructura  
 El algoritmo ARTXP era el algoritmo de serie temporal predeterminado de SQL Server 2005 y se optimizó para la predicción a corto plazo. Para comparar las predicciones con los tres algoritmos de serie temporal, agregará un modelo más que se basa en el algoritmo ARTXP.  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>Para agregar un modelo de minería de datos de serie temporal ARTXP  
  
1.  Copie el código siguiente en una ventana de consulta en blanco.  
  
     Observe que no necesita cambiar nada excepto el nombre del nuevo modelo de minería de datos y el valor del parámetro FORECAST_METHOD.  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  En el menú **archivo** , haga clic en **Guardar DMXQuery1. DMX como**.  
  
3.  En el cuadro de diálogo **Guardar como** , vaya a la carpeta correspondiente y asigne el nombre `Forecasting_ARTXP.dmx`al archivo.  
  
4.  En la barra de herramientas, haga clic en el botón **Ejecutar** .  
  
 En la siguiente lección procesará todos los modelos y la estructura de minería de datos.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Procesar la estructura de serie temporal y los modelos](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft Time Series Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
