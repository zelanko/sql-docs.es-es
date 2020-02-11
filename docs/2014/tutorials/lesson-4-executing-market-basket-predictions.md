---
title: 'Lección 4: ejecutar predicciones de la cesta de la compra | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b3238f1b-ea04-4253-ade2-838a806b62fe
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3b49fc242eb8b2242269c5af33cc094937bbe0de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63312109"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>Lección 4: Ejecutar predicciones de cesta de la compra
  En esta lección, usará la instrucción DMX `SELECT` para crear predicciones basadas en los modelos de asociación que creó en la [Lección 2: agregar modelos de minería de datos a la estructura de minería de datos Market Basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md). Para crear una consulta de predicción se usa la instrucción `SELECT` de DMX y se agrega una cláusula `PREDICTION JOIN`. Para obtener más información sobre la sintaxis de una combinación de predicción, vea [seleccionar desde &#60;modelo&#62; combinación de predicción &#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx).  
  
 El formulario **seleccionar \<del modelo> combinación de predicción** de `SELECT` la instrucción contiene tres partes:  
  
-   Una lista de las funciones de predicción y las columnas del modelo de minería de datos devueltas en el conjunto de resultados. Esta lista también puede incluir columnas de entrada de los datos de origen.  
  
-   Una consulta de origen que define los datos que se usan para crear una predicción. Por ejemplo, si está creando muchas predicciones en un lote, la consulta de origen podría recuperar una lista de clientes.  
  
-   Una asignación entre las columnas del modelo de minería de datos y los datos de origen. Si los nombres de las columnas coinciden, puede usar la sintaxis `NATURAL PREDICTION JOIN` y omitir las asignaciones de columna.  
  
 La consulta se puede mejorar si se usan funciones de predicción. Las funciones de predicción proporcionan información adicional, como la probabilidad de que se produzca una predicción o la existencia de compatibilidad con una predicción en el conjunto de datos de entrenamiento. Para obtener más información sobre las funciones de predicción, consulte [funciones &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
 También puede usar el generador de consultas de predicción de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para crear consultas de predicción.  
  
## <a name="singleton-prediction-join-statement"></a>Instrucción singleton PREDICTION JOIN  
 El primer paso es crear una consulta singleton, mediante la sintaxis **Select from \<Model> join join** y proporcionar un único conjunto de valores como entrada. A continuación, se incluye un ejemplo genérico de la instrucción singleton:  
  
```  
SELECT <select list>  
    FROM [<mining model>]   
[NATURAL] PREDICTION JOIN  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
AS [<input alias>]  
```  
  
 En la primera línea del código se definen las columnas del modelo de minería de datos que devuelve la consulta y se especifica el nombre del modelo de minería de datos usado para generar la predicción:  
  
```  
SELECT <select list> FROM [<mining model>]   
```  
  
 La línea del código siguiente indica la operación que se va a realizar. Dado que se especificarán valores para cada una de las columnas y se escribirán los nombres de columna exactamente de manera que coincidan con el modelo, puede usar la sintaxis `NATURAL PREDICTION JOIN`. Sin embargo, si los nombres de columna fueran diferentes, tendría que especificar las asignaciones entre las columnas del modelo y las columnas de los nuevos datos agregando una cláusula `ON`.  
  
```  
[NATURAL] PREDICTION JOIN  
```  
  
 En las líneas siguientes del código se definen los artículos del carro de la compra que se utilizarán para predecir artículos adicionales que un cliente agregará:  
  
```  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
```  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Cree una consulta que prediga qué otros elementos probablemente comprará un cliente, en función de los elementos ya existentes en el carro de la compra. Creará esta consulta mediante el modelo de minería de datos con el *MINIMUM_PROBABILITY*predeterminado.  
  
-   Crear una consulta que prediga qué otros artículos podría adquirir un cliente en función de los artículos que ya se están en su carro de la compra. Esta consulta se basa en un modelo diferente, en el que *MINIMUM_PROBABILITY* se ha establecido en 0,01. Dado que el valor predeterminado para *MINIMUM_PROBABILITY* en los modelos de asociación es 0,3, la consulta de este modelo debe devolver más elementos posibles que la consulta del modelo predeterminado.  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimum_probability"></a>Crear una predicción usando un modelo con el valor de MINIMUM_PROBABILITY predeterminado  
  
#### <a name="to-create-an-association-query"></a>Para crear una consulta de asociación  
  
1.  En **Explorador de objetos**, haga clic con el botón secundario [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]en la instancia de, seleccione **nueva consulta**y, a continuación, haga clic en **DMX** para abrir el editor de consultas.  
  
2.  Copie el ejemplo genérico de la instrucción `PREDICTION JOIN` en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     Podría incluir simplemente el nombre de columna [Products], pero mediante la función [PREDICT &#40;DMX&#41;](/sql/dmx/predict-dmx) , puede limitar el número de productos que devuelve el algoritmo a tres. También puede usar `INCLUDE_STATISTICS`, que devuelve la compatibilidad, la probabilidad y la probabilidad ajustada para cada producto. Estas estadísticas ayudan a valorar la precisión de la predicción.  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Default Association]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     por:  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     Esta instrucción utiliza la instrucción `UNION` para especificar tres productos que se deben incluir en el carro de la compra junto con los artículos previstos. La columna Model de la instrucción `SELECT` corresponde a la columna de modelo incluida en la tabla de productos anidada.  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT  
      PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Default Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  En el menú **archivo** , haga clic en **Guardar DMXQuery1. DMX como**.  
  
7.  En el cuadro de diálogo **Guardar como** , vaya a la carpeta correspondiente y asigne el nombre `Association Prediction.dmx`al archivo.  
  
8.  En la barra de herramientas, haga clic en el botón **Ejecutar** .  
  
     La consulta devuelve una tabla que contiene tres productos: HL Mountain Tire, Fender Set - Mountain y ML Mountain Tire. En la tabla se enumeran estos productos devueltos por orden de probabilidad. En la parte superior de la tabla aparece el producto devuelto con mayor probabilidad de estar incluido en el mismo carro de la compra que los tres productos especificados en la consulta. Los dos productos siguientes son los de mayor probabilidad de estar incluidos en el carro de la compra. La tabla también contiene estadísticas que describen la precisión de la predicción.  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimum_probability-of-001"></a>Crear una predicción usando un modelo con el valor 0,01 para MINIMUM_PROBABILITY  
  
#### <a name="to-create-an-association-query"></a>Para crear una consulta de asociación  
  
1.  En **Explorador de objetos**, haga clic con el botón secundario [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]en la instancia de, seleccione **nueva consulta**y, a continuación, haga clic en **DMX** para abrir el editor de consultas.  
  
2.  Copie el ejemplo genérico de la instrucción `PREDICTION JOIN` en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Modified Association]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     por:  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     Esta instrucción utiliza la instrucción `UNION` para especificar tres productos que se deben incluir en el carro de la compra junto con los artículos previstos. La columna `[Model]` de la instrucción `SELECT` corresponde a la columna incluida en la tabla de artículos anidada.  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT  
      PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Modified Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  En el menú **archivo** , haga clic en **Guardar DMXQuery1. DMX como**.  
  
7.  En el cuadro de diálogo **Guardar como** , vaya a la carpeta correspondiente y asigne el nombre `Modified Association Prediction.dmx`al archivo.  
  
8.  En la barra de herramientas, haga clic en el botón **Ejecutar** .  
  
     La consulta devuelve una tabla que contiene tres artículos: HL Mountain Tire, Water Bottle y Fender Set - Mountain. En la tabla se enumeran estos productos por orden de probabilidad. El producto que aparece al principio de la tabla es el producto con mayor probabilidad de estar incluido en el mismo carro de la compra que los tres artículos especificados en la consulta. Los productos restantes son los siguientes con mayor probabilidad de estar incluidos en el carro de la compra. La tabla también contiene estadísticas que describen la precisión de la predicción.  
  
     Puede ver en los resultados de esta consulta que el valor del parámetro *MINIMUM_PROBABILITY* afecta a los resultados devueltos por la consulta.  
  
 Éste es el último paso del tutorial de Market Basket. Ahora dispone de un conjunto de modelos que puede usar para predecir los artículos que los clientes pueden adquirir simultáneamente.  
  
 Para obtener información sobre cómo usar DMX en otro escenario predictivo, consulte el [tutorial de Bike Buyer DMX](../../2014/tutorials/bike-buyer-dmx-tutorial.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de consultas de modelos de asociación](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [Interfaces de consultas de minería de datos](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
