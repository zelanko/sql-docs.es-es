---
title: 'Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de Bike Buyer | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 03fe44c5-6452-4ed0-95f6-9682670c0f52
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: de65fb7a85154f607cd8f266faec4621cdc41476
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131746"
---
# <a name="lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure"></a>Lección 2: Adición de modelos de minería de datos a la estructura de minería de datos de Bike Buyer
  En esta lección, agregará dos modelos de minería de datos a la estructura de minería de datos de Bike Buyer que creó [lección 1: Creación de la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md). Estos modelos de minería de datos le permitirán explorar los datos usando un modelo y crear predicciones usando otro modelo.  
  
 Para explorar cómo los clientes potenciales se pueden clasificar según sus características, creará un modelo de minería de datos basado en la [Microsoft Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md). En una lección posterior, explorará cómo este algoritmo encuentra clústeres de clientes que comparten características parecidas. Por ejemplo, podría averiguar que ciertos clientes tienden a vivir cerca unos de otros, van al trabajo en bicicleta y tienen una formación parecida. Puede utilizar estos clústeres para comprender mejor cómo están relacionados distintos clientes y para utilizar la información para crear una estrategia de marketing dirigida a clientes concretos.  
  
 Para predecir si un cliente potencial es probable que compren una bicicleta, creará un modelo de minería de datos basado en la [Microsoft Decision Trees Algorithm](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md). Este algoritmo examina la información asociada a cada cliente potencial y encuentra características útiles para predecir si adquirirá una bicicleta. A continuación, compara los valores de las características de compradores de bicicletas anteriores con los nuevos clientes potenciales para determinar si es probable que éstos adquieran una bicicleta.  
  
## <a name="alter-mining-structure-statement"></a>Instrucción ALTER MINING STRUCTURE  
 Para agregar un modelo de minería de datos a la estructura de minería de datos, se utiliza el [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) instrucción. El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Identificación de la estructura de minería de datos  
  
-   Asignación de un nombre al modelo de minería de datos  
  
-   Definición de la columna de clave  
  
-   Definición de las columnas de entrada y de predicción  
  
-   Identificación de los cambios de parámetros y el algoritmo  
  
 A continuación, se incluye un ejemplo genérico de la instrucción ALTER MINING MODEL:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
(  
    [<key column>],  
    <mining model columns>,  
) USING <algorithm name>( <algorithm parameters> )  
WITH FILTER (<expression>)  
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
[<key column>],  
<mining model columns>  
```  
  
 Solo puede utilizar columnas que ya existan en la estructura de minería de datos, y la primera columna de la lista debe ser la columna de clave de la estructura.  
  
 La siguiente línea de código define el algoritmo de minería de datos que genera el modelo de minería de datos y los parámetros de algoritmo que pueden establecerse:  
  
```  
) USING <algorithm name>( <algorithm parameters> )  
```  
  
 Para obtener más información acerca de los parámetros del algoritmo que puede ajustar, vea [Microsoft Decision Trees Algorithm](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) y [Microsoft Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md).  
  
 Puede especificar que una columna del modelo de minería de datos se utilice para la predicción mediante la sintaxis siguiente:  
  
```  
<mining model column> PREDICT  
```  
  
 La última línea de código, que es opcional, define un filtro que se aplica durante el aprendizaje y prueba del modelo. Para obtener más información acerca de cómo aplicar filtros a los modelos de minería de datos, vea [filtros para modelos de minería de datos de &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Agregar un modelo de minería de datos del árbol de decisión a la estructura Bike Buyer mediante el algoritmo Árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   Agregar un modelo de minería de datos de agrupación en clústeres a la estructura Bike Buyer mediante el algoritmo de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   Dado que desean verse los resultados para todos los casos, todavía no se agrega un filtro a ningún modelo.  
  
## <a name="adding-a-decision-tree-mining-model-to-the-structure"></a>Agregar un modelo de minería de datos del árbol de decisión a la estructura  
 El primer paso es agregar un modelo de minería de datos basado en el algoritmo Árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
#### <a name="to-add-a-decision-tree-mining-model"></a>Para agregar un modelo de minería de datos del árbol de decisión  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX** para abrir el Editor de consultas y una nueva consulta en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción ALTER MINING STRUCTURE en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    Decision Tree  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    <mining model columns>,  
    ```  
  
     por:  
  
    ```  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ```  
  
     En este caso, la columna `[Bike Buyer]` se ha designado como columna PREDICT.  
  
6.  Reemplace lo siguiente:  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )   
    ```  
  
     por:  
  
    ```  
    Using Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
     La instrucción WITH DRILLTHROUGH permite explorar los casos utilizados para generar el modelo de minería de datos.  
  
     Ahora, la instrucción resultante debería ser como sigue:  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Decision Tree]  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ) USING Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
7.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
8.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `DT_Model.dmx`.  
  
9. En la barra de herramientas, haga clic en el **Execute** botón.  
  
## <a name="adding-a-clustering-mining-model-to-the-structure"></a>Agregar un modelo de minería de datos de agrupación en clústeres a la estructura  
 A continuación, podrá agregar un modelo de minería de datos a la estructura de minería de datos Bike Buyer basado en el algoritmo de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)]. Puesto que el modelo de minería de datos de agrupación en clústeres utilizará todas las columnas definidas en la estructura de minería de datos, puede utilizar un acceso directo para agregar el modelo a la estructura sin incluir la definición de las columnas de minería de datos.  
  
#### <a name="to-add-a-clustering-mining-model"></a>Para agregar un modelo de minería de datos de agrupación en clústeres  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX** para abrir una consulta en blanco y se abre el Editor de consultas.  
  
2.  Copie el ejemplo genérico de la instrucción ALTER MINING STRUCTURE en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining model>   
    ```  
  
     por:  
  
    ```  
    Clustering Model  
    ```  
  
5.  Elimine lo siguiente:  
  
    ```  
    (  
        [<key column>],  
        <mining model columns>,  
    )  
    ```  
  
6.  Reemplace lo siguiente:  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Clustering  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Clustering]  
    USING Microsoft_Clustering   
    ```  
  
7.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
8.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Clustering_Model.dmx`.  
  
9. En la barra de herramientas, haga clic en el **Execute** botón.  
  
 En la siguiente lección procesará los modelos y la estructura de minería de datos.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Procesar la estructura de minería de datos de Bike Buyer](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
  
  
