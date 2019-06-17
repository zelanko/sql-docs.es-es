---
title: 'Lección 1: Creación de una serie temporal del modelo de minería de datos y la estructura de minería de datos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b201f2b8-9ab5-425b-9ff3-fe321a60a7b7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2513bc3837dd224f6561eb0015ced538ea3add8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678448"
---
# <a name="lesson-1-creating-a-time-series-mining-model-and-mining-structure"></a>Lección 1: Creación de un modelo de minería de datos de serie temporal y una estructura de minería de datos
  En esta lección, creará un modelo de minería de datos que le permita predecir valores a lo largo del tiempo, según datos históricos. Al crear el modelo, la estructura subyacente se generará automáticamente y se utilizará como base para otros modelos de minería de datos.  
  
 En esta lección se supone que conoce los modelos de predicción y los requisitos del algoritmo de serie temporal de Microsoft. Para más información, consulte [Microsoft Time Series Algorithm](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
## <a name="create-mining-model-statement"></a>Instrucción CREATE MINING MODEL  
 Para crear un modelo de minería de datos directamente y generar automáticamente la estructura de minería de datos subyacente, se utiliza el [CREATE MINING MODEL &#40;DMX&#41; ](/sql/dmx/create-mining-model-dmx) instrucción. El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Asignación de un nombre al modelo  
  
-   Definición de la marca de tiempo  
  
-   Definición de la columna de clave de la serie opcional  
  
-   Definición del atributo o atributos de predicción  
  
 A continuación, se incluye un ejemplo genérico de la instrucción CREATE MINING MODEL:  
  
```  
CREATE MINING MODEL [<Mining Structure Name>]  
(  
   <key columns>,  
   <predictable attribute columns>  
)  
USING <algorithm name>([parameter list])  
WITH DRILLTHROUGH  
```  
  
 En la primera línea del código se define el nombre del modelo de minería de datos:  
  
```  
CREATE MINING MODEL [Mining Model Name]  
```  
  
 Analysis Services genera un nombre para la estructura subyacente anexando "_structure" al nombre del modelo, con lo que se asegura de que el nombre de la estructura sea distinto del nombre del modelo. Para obtener información sobre la nomenclatura de un objeto en DMX, vea [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 La línea siguiente de código define la columna de clave para el modelo de minería de datos, que en el caso de un modelo de serie temporal identifica singularmente un incremento de tiempo en los datos del origen. El paso del tiempo se identifica con el `KEY TIME` palabras clave después de los tipos de datos y el nombre de columna. Si el modelo de serie temporal tiene una clave de serie independiente, se identifica con la palabra clave `KEY`.  
  
```  
<key columns>  
```  
  
 La línea siguiente del código se utiliza para definir las columnas del modelo que se predecirá. Puede tener varios atributos de predicción en un único modelo de minería de datos. Cuando hay varios atributos de predicción, el algoritmo de serie temporal de Microsoft genera un análisis independiente para cada serie:  
  
```  
<predictable attribute columns>  
```  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Crear una consulta en blanco  
  
-   Modificar la consulta para crear la el modelo de minería de datos  
  
-   Ejecutar la consulta  
  
## <a name="creating-the-query"></a>Crear la consulta  
 El primer paso es conectarse a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y crear una consulta DMX en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Para crear una consulta DMX mediante SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  En el **conectar al servidor** cuadro de diálogo para **tipo de servidor**, seleccione **Analysis Services**. En **nombre del servidor**, tipo `LocalHost`, o el nombre de la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que desea conectarse a esta lección. Haga clic en **Conectar**.  
  
3.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
## <a name="altering-the-query"></a>Modificar la consulta  
 El paso siguiente es modificar la instrucción CREATE MINING MODEL para crear el modelo de minería de datos que se usa para la predicción, junto con su estructura de minería de datos subyacente.  
  
#### <a name="to-customize-the-create-mining-model-statement"></a>Para personalizar la instrucción CREATE MINING MODEL  
  
1.  En el Editor de consultas, copie el ejemplo genérico de la instrucción CREATE MINING MODEL en la consulta en blanco.  
  
2.  Reemplace lo siguiente:  
  
    ```  
    [mining model name]   
    ```  
  
     por:  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <key columns>  
    ```  
  
     por:  
  
    ```  
    [Reporting Date] DATE KEY TIME,  
    [Model Region] TEXT KEY  
    ```  
  
     La palabra clave `TIME KEY` indica que la columna ReportingDate contiene los valores de incremento de tiempo utilizados para ordenar los valores. Los incrementos de tiempo pueden ser fechas y horas, números enteros o cualquier tipo de datos ordenado, siempre que los valores sean únicos y los datos estén ordenados.  
  
     Las palabras clave `TEXT` y `KEY` indican que la columna ModelRegion contiene una clave de serie adicional. Puede tener únicamente una clave de serie y los valores de la columna deben ser distintos.  
  
4.  Reemplace lo siguiente:  
  
    ```  
    < predictable attribute columns> )  
    ```  
  
     por:  
  
    ```  
    [Quantity] LONG CONTINUOUS PREDICT,  
    [Amount] DOUBLE CONTINUOUS PREDICT  
    )  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    USING <algorithm name>([parameter list])  
    WITH DRILLTHROUGH  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Time_Series(AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
    ```  
  
     El parámetro de algoritmo, `AUTO_DETECT_PERIODICITY` = 0.8, indica que desea que el algoritmo detecte los ciclos en los datos. Si se establece este valor más próximo a 1, se favorece la detección de muchos patrones pero puede desacelerar el procesamiento.  
  
     El parámetro de algoritmo, `FORECAST_METHOD`, indica si desea analizar los datos utilizando ARTXP, ARIMA o una combinación de ambos.  
  
     La palabra clave, `WITH DRILLTHROUGH`, especifica que desea poder ver estadísticas detalladas de los datos de origen cuando el modelo se complete. Debe agregar esta cláusula si desea examinar el modelo utilizando el Visor de series temporales de Microsoft. No se requiere para la predicción.  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    CREATE MINING MODEL [Forecasting_MIXED]  
         (  
        [Reporting Date] DATE KEY TIME,  
        [Model Region] TEXT KEY,  
        [Quantity] LONG CONTINUOUS PREDICT,  
        [Amount] DOUBLE CONTINUOUS PREDICT  
        )  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
  
    ```  
  
6.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
7.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Forecasting_MIXED.dmx`.  
  
## <a name="executing-the-query"></a>Ejecutar la consulta  
 El último paso es ejecutar la consulta. Después de crear y guardar una consulta, debe ejecutarse para crear el modelo y su estructura de minería de datos en el servidor. Para obtener más información acerca de cómo ejecutar consultas en el Editor de consultas, vea [Editor de consultas del motor de base de datos &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Para ejecutar la consulta  
  
-   En el Editor de consultas, en la barra de herramientas, haga clic en **Execute**.  
  
     El estado de la consulta se muestra en el **mensajes** en la parte inferior del Editor de consultas de una vez que finaliza la ejecución de la instrucción. En Mensajes, debe aparecer lo siguiente:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Una nueva estructura denominada **Forecasting_MIXED_Structure** ahora existe en el servidor, junto con el modelo de minería de datos relacionado **Forecasting_MIXED**.  
  
 En la siguiente lección, agregará un modelo de minería de datos para el **Forecasting_MIXED** estructura de minería de datos que acaba de crear.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de serie temporal](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo para los modelos de serie temporal de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)   
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
