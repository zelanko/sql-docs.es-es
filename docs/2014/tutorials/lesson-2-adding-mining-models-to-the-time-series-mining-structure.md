---
title: 'Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de serie temporal | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cee3d839ae7a7bcce62c8a3a1d2f7cb62b1155e2
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312493"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de serie temporal
  En esta lección, agregará un nuevo modelo de minería de datos a la estructura de minería de datos que acaba de crear en [lección 1: crear un modelo de minería de datos de serie temporal y la estructura de minería de datos](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md).  
  
## <a name="alter-mining-structure-statement"></a>Instrucción ALTER MINING STRUCTURE  
 Para agregar un nuevo modelo de minería de datos a una estructura de minería de datos existente, se utiliza el [ALTER MINING STRUCTURE &#40;DMX&#41;] (instrucción (~/dmx/alter-mining-structure-dmx.md). El código de la instrucción se puede dividir en las partes siguientes:  
  
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
  
 Para obtener información sobre la nomenclatura de un objeto en DMX, vea [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
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
  
 Para obtener más información acerca de los parámetros de algoritmo que puede ajustar, vea [Microsoft Time Series Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
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
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], seleccione **nueva consulta**y, a continuación, haga clic en **DMX** para abrir el Editor de consultas y una consulta en blanco.  
  
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
  
8.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
9. En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y un nombre al archivo `Forecasting_ARIMA.dmx`.  
  
10. En la barra de herramientas, haga clic en el **Execute** botón.  
  
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
  
2.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
3.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y un nombre al archivo `Forecasting_ARTXP.dmx`.  
  
4.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
 En la siguiente lección procesará todos los modelos y la estructura de minería de datos.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Procesar la estructura y modelos de la serie temporal](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
