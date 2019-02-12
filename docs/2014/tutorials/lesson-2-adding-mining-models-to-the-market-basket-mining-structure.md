---
title: 'Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos Market Basket | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041456"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>Lección 2: Agregar modelos de minería a la estructura de minería cesta de la compra
  En esta lección, agregará dos modelos de minería de datos a la estructura de minería de datos Market Basket que creó en [lección 1: Creación de la estructura de minería de datos Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md). Estos modelos de minería de datos le permitirán crear predicciones.  
  
 Para predecir los tipos de productos que los clientes tienden a comprar al mismo tiempo, creará dos modelos de minería de datos mediante el [Microsoft Association Algorithm](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md) y dos valores diferentes para el *MINIMUM_PROBABILTY* parámetro.  
  
 *MINIMUM_PROBABILTY* es un [!INCLUDE[msCoName](../includes/msconame-md.md)] parámetro de algoritmo de asociación que ayuda a determinar el número de reglas que contendrá un modelo de minería de datos mediante la especificación de la probabilidad mínima que debe tener una regla. Por ejemplo, al establecer este valor en 0,4 se especifica que se puede generar una regla solo si la combinación de productos que la regla describe tiene al menos una probabilidad del 40 por ciento de que esto ocurra.  
  
 Verá el efecto de cambiar la *MINIMUM_PROBABILTY* parámetro en una lección posterior.  
  
## <a name="alter-mining-structure-statement"></a>Instrucción ALTER MINING STRUCTURE  
 Para agregar un modelo de minería de datos que contiene una tabla anidada a una estructura de minería de datos, use el [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) instrucción. El código de la instrucción se puede dividir en las partes siguientes:  
  
-   Identificación de la estructura de minería de datos  
  
-   Asignación de un nombre al modelo de minería de datos  
  
-   Definición de la columna de clave  
  
-   Definición de las columnas de entrada y de predicción  
  
-   Definición de las columnas de la tabla anidada  
  
-   Identificación de los cambios de parámetros y el algoritmo  
  
 El siguiente es un ejemplo genérico de la instrucción `ALTER MINING STRUCTURE` que agrega un modelo de minería de datos a una estructura que incluye columnas de tabla anidada:  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 La primera línea del código identifica la estructura de minería de datos existente a la que se agregará el modelo de minería de datos:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 La siguiente línea de código asigna un nombre al modelo de minería de datos que se agregará a la estructura de minería de datos:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Para obtener información sobre la nomenclatura de un objeto en extensiones de minería de datos (DMX), consulte [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 Las líneas siguientes del código definen las columnas de la estructura de minería de datos que usará el modelo de minería de datos:  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 Solo puede usar columnas que ya existen en la estructura de minería de datos.  
  
 La primera columna de la lista de columnas del modelo de minería de datos debe ser la columna de clave en la estructura de minería de datos. Sin embargo, no es necesario escribir `KEY` después de la columna de clave para especificar el uso. Eso se debe a que ya ha definido la columna como una clave cuando creó la estructura de minería de datos.  
  
 Las líneas restantes especifican el uso de las columnas en el nuevo modelo de minería de datos. Puede especificar que una columna en el modelo de minería de datos se usará para la predicción mediante la sintaxis siguiente:  
  
```  
<column name> PREDICT,  
```  
  
 Si no especifica el uso, no tiene que incluir una columna de la estructura de minería de datos en la lista. Todas las columnas que se usan por la estructura de minería de datos a la que se hace referencia están disponibles automáticamente para su uso por parte de los modelos de minería de datos que se basan en dicha estructura. Sin embargo, el modelo no usará las columnas para entrenamiento a menos que especifique el uso.  
  
 En la última línea del código se define el algoritmo y los parámetros del algoritmo que se utilizarán para generar el modelo de minería de datos.  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Agregar un modelo de minería de datos de asociación a la estructura con la probabilidad predeterminada  
  
-   Agregar un modelo de minería de datos de asociación a la estructura con una probabilidad modificada  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimumprobability"></a>Agregar un modelo de minería de datos de asociación a la estructura con el valor predeterminado de MINIMUM_PROBABILITY  
 La primera tarea consiste en Agregar un nuevo modelo de minería de datos a la estructura de minería de datos Market Basket basado en el [!INCLUDE[msCoName](../includes/msconame-md.md)] con el valor predeterminado para el algoritmo de asociación *MINIMUM_PROBABILITY*.  
  
#### <a name="to-add-an-association-mining-model"></a>Agregar un modelo de minería de datos de asociación  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
    > [!NOTE]  
    >  Para crear una consulta de DMX frente a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] concreta, haga clic con el botón secundario en la base de datos en lugar de la instancia.  
  
2.  Copie el ejemplo genérico de la instrucción `ALTER MINING STRUCTURE` en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Market Basket]  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    [Default Association]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     por:  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     En este caso, la tabla `[Products]` se ha designado como la columna de predicción`.` Además, la columna `[Model]` está incluida en la lista de columnas de tabla anidada porque es la columna de clave de la tabla anidada.  
  
    > [!NOTE]  
    >  Recuerde que una clave anidada es diferente de una clave de caso. Una clave de caso es un identificador único del caso, mientras que la clave anidada es un atributo que desea usar como modelo.  
  
6.  Reemplace lo siguiente:  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     por:  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     Ahora, la instrucción resultante debería ser como sigue:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
8.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Default_Association_Model.dmx`.  
  
9. En la barra de herramientas, haga clic en el **Execute** botón.  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimumprobability"></a>Agregar un modelo de minería de datos de asociación a la estructura cambiando el valor predeterminado de MINIMUM_PROBABILITY  
 La siguiente tarea es agregar un nuevo modelo de minería de datos a la estructura de minería de datos Market Basket basado en el algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)] y, después, cambiar el valor predeterminado de MINIMUM_PROBABILITY a 0,01. Al cambiar el parámetro, el algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)] creará más reglas.  
  
#### <a name="to-add-an-association-mining-model"></a>Agregar un modelo de minería de datos de asociación  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción `ALTER MINING STRUCTURE` en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    Market Basket  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    [Modified Association]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     por:  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     En este caso, la tabla `[Products]` se ha designado como la columna de predicción. Además, la columna `[MODEL]` está incluida en la lista porque es la columna de clave de la tabla anidada.  
  
6.  Reemplace lo siguiente:  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     Ahora, la instrucción resultante debería ser como sigue:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
8.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Modified Association_Model.dmx`.  
  
9. En la barra de herramientas, haga clic en el **Execute** botón.  
  
 En esta siguiente lección procesará la estructura de minería de datos Market Basket junto con sus modelos de minería de datos asociados.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Procesar la estructura de minería de datos Market Basket](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
