---
title: 'Lección 5: Ejecutar consultas de predicción | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0037bd2f-aa2d-464b-bf86-b0210f0438b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a5f4d6dd79f62541e207df688349f694680e2421
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822317"
---
# <a name="lesson-5-executing-prediction-queries"></a>Lección 5: Ejecución de consultas de predicción
  En esta lección, usará el [SELECT FROM \<modelo > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) del modelo que ha creado en el formulario de la instrucción SELECT para crear dos tipos diferentes de predicciones basadas en el árbol de decisión [ Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de asociación](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md). Estos tipos de predicciones se definen a continuación.  
  
 Consulta singleton  
 Use una consulta singleton para proporcionar valores ad hoc al realizar predicciones. Por ejemplo, puede determinar si es probable que un cliente sea un comprador de bicicletas pasando entradas a la consulta, como la distancia al lugar de trabajo, el prefijo telefónico o el número de hijos del cliente. La consulta singleton devuelve un valor que indica la probabilidad de que la persona compre una bicicleta basándose en esas entradas.  
  
 Consulta por lotes  
 Utilice una consulta por lotes para determinar qué clientes potenciales incluidos en una tabla es probable que adquieran una bicicleta. Por ejemplo, si el departamento de marketing le proporciona una lista de clientes y atributos de clientes, puede utilizar una predicción por lotes para determinar qué clientes de la tabla es probable que adquieran una bicicleta.  
  
 El [SELECT FROM \<modelo > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) formulario de la instrucción SELECT consta de tres partes:  
  
-   Una lista de las funciones de predicción y las columnas del modelo de minería de datos devueltas en los resultados. Los resultados también pueden incluir columnas de entrada de los datos de origen.  
  
-   La consulta de origen que define los datos que se utilizan para crear una predicción. Por ejemplo, en una consulta por lotes, podría ser una lista de clientes.  
  
-   Una asignación entre las columnas del modelo de minería de datos y los datos de origen. Si los nombres coinciden, puede utilizar la sintaxis NATURAL y no incluir las asignaciones de columnas.  
  
 La consulta se puede mejorar aún más si se utilizan funciones de predicción. Las funciones de predicción proporcionan información adicional como, por ejemplo, la probabilidad de que se produzca una predicción, y ofrecen compatibilidad con la predicción en el conjunto de datos de entrenamiento. Para obtener más información acerca de las funciones de predicción, vea [funciones &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
 Las predicciones de este tutorial se basan en la tabla ProspectiveBuyer de la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. La tabla ProspectiveBuyer contiene una lista de clientes potenciales y de sus características asociadas. Los clientes de esta tabla son independientes de los clientes utilizados para crear el modelo de minería de datos del árbol de decisión.  
  
 También se pueden crear predicciones usando el generador de consultas de predicción de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 En esta lección realizará las tareas siguientes:  
  
-   Crear una consulta singleton para determinar si es probable que un cliente específico adquiera una bicicleta.  
  
-   Crear una consulta por lotes para determinar qué clientes de los incluidos en una tabla es probable que adquieran una bicicleta.  
  
## <a name="singleton-query"></a>Consulta singleton  
 El primer paso consiste en usar el [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) en una consulta de predicción de singleton. A continuación, se incluye un ejemplo genérico de la instrucción singleton:  
  
```  
SELECT <select list> FROM [<mining model name>]   
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
```  
  
 En la primera línea del código se definen las columnas del modelo de minería de datos que debe devolver la consulta y se especifica el modelo de minería de datos usado para generar la predicción:  
  
```  
SELECT <select list> FROM [<mining model name>]   
```  
  
 En las líneas siguientes del código se definen las características del cliente que se utilizan para crear una predicción:  
  
```  
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
ORDER BY <expression>  
```  
  
 Si especifica NATURAL PREDICTION JOIN, el servidor compara los nombres de cada columna del modelo con los nombres de las columnas de los datos de entrada. Si los nombres de columna no coinciden, las columnas se omiten.  
  
#### <a name="to-create-a-singleton-prediction-query"></a>Para crear una consulta de predicción singleton  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción singleton en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer] AS Buyer, PredictHistogram([Bike Buyer]) AS Statistics  
    ```  
  
     La instrucción AS se utiliza para asignar un alias a las columnas devueltas por la consulta. El [PredictHistogram](/sql/dmx/predicthistogram-dmx) función devuelve estadísticas sobre la predicción, incluidas la probabilidad y el soporte técnico. Para obtener más información sobre las funciones que puede usarse en una instrucción de predicción, vea [funciones &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
4.  Reemplace lo siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    (SELECT '<value>' AS [<column name>], ...)  AS t  
    ```  
  
     por:  
  
    ```  
    (SELECT 35 AS [Age],  
      '5-10 Miles' AS [Commute Distance],  
      '1' AS [House Owner Flag],  
      2 AS [Number Cars Owned],  
      2 AS [Total Children]) AS t  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT  
       [Bike Buyer] AS Buyer,  
       PredictHistogram([Bike Buyer]) AS Statistics  
    FROM  
       [Decision Tree]  
    NATURAL PREDICTION JOIN  
    (SELECT 35 AS [Age],  
       '5-10 Miles' AS [Commute Distance],  
       '1' AS [House Owner Flag],  
       2 AS [Number Cars Owned],  
       2 AS [Total Children]) AS t  
    ```  
  
6.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
7.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Singleton_Query.dmx`.  
  
8.  En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve una predicción acerca de si un cliente con las características especificadas adquirirá una bicicleta, así como estadísticas acerca de la predicción.  
  
## <a name="batch-query"></a>Consulta por lotes  
 El paso siguiente consiste en usar el [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) en una consulta de predicción por lotes. A continuación, se incluye un ejemplo genérico de una instrucción por lotes:  
  
```  
SELECT TOP <number> <select list>   
FROM [<mining model name>]  
PREDICTION JOIN  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
ON <on clause, mapping,>  
WHERE <where clause, boolean expression,>  
ORDER BY <expression>  
```  
  
 Como en la consulta singleton, en las dos primeras líneas del código se definen las columnas del modelo de minería de datos devueltas por la consulta, así como el nombre del modelo de minería de datos utilizado para generar la predicción. La parte superior \<número > instrucción especifica que la consulta sólo devolverá el número o los resultados especificados por \<número >.  
  
 En las líneas siguientes del código se definen los datos de origen en los que se basan las predicciones:  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
```  
  
 En cuanto al método utilizado para recuperar los datos de origen, hay varias opciones, pero en este tutorial se usará OPENQUERY. Para obtener más información sobre las opciones disponibles, consulte [ &#60;consulta de origen de datos&#62;](/sql/dmx/source-data-query).  
  
 En la línea siguiente se definen la asignación entre las columnas de origen del modelo de minería de datos y las columnas de los datos de origen:  
  
```  
ON <column mappings>  
```  
  
 La cláusula WHERE filtra los resultados devueltos por la consulta de predicción:  
  
```  
WHERE <where clause, boolean expression,>  
```  
  
 En la última línea del código, que es opcional, se especifica la columna por la cual se ordenarán los resultados:  
  
```  
ORDER BY <expression> [DESC|ASC]  
```  
  
 Usar ORDER BY en combinación con la parte superior \<número > instrucción para filtrar los resultados que se devuelven. Por ejemplo, en esta predicción se devolverán los diez principales compradores de bicicletas, ordenados por la probabilidad de que la predicción sea correcta. Puede utilizar la sintaxis [DESC|ASC] para controlar el orden en el que aparecen los resultados.  
  
#### <a name="to-create-a-batch-prediction-query"></a>Para crear una consulta de predicción por lotes  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción por lotes en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    ```  
  
     La cláusula TOP 10 especifica que la consulta solo devolverá los diez primeros resultados. La instrucción ORDER BY de esta consulta ordena los resultados según la probabilidad de que la predicción sea correcta, por lo que solo se devolverán los diez resultados más probables.  
  
4.  Reemplace el marcador de posición siguiente:  
  
    ```  
    [<mining model>]   
    ```  
  
     Con el nombre del modelo:  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  Reemplace la instrucción OPENQUERY genérica siguiente:  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     Con una instrucción que haga referencia al almacenamiento de datos Adventureworks actual, por ejemplo:  
  
    ```  
    OPENQUERY([Adventure Works DW 2014],  
      'SELECT  
        [LastName],  
        [FirstName],  
        [MaritalStatus],  
        [Gender],  
        [YearlyIncome],  
        [TotalChildren],  
        [NumberChildrenAtHome],  
        [Education],  
        [Occupation],  
        [HouseOwnerFlag],  
        [NumberCarsOwned]  
      FROM  
        [dbo].[ProspectiveBuyer]  
      ') AS t  
    ```  
  
6.  Reemplace la sintaxis genérica siguiente:  
  
    ```  
    <ON clause, mapping,>   
    WHERE <where clause, boolean expression,>  
    ORDER BY <expression>  
    ```  
  
     Con las asignaciones de columna necesarias para este modelo y conjunto de datos de entrada:  
  
    ```  
    [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
     Especifique `DESC` para que los resultados con la probabilidad más alta aparezcan primero en la lista.  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    FROM  
      [Decision Tree]  
    PREDICTION JOIN  
      OPENQUERY([Adventure Works DW 2014],  
        'SELECT  
          [LastName],  
          [FirstName],  
          [MaritalStatus],  
          [Gender],  
          [YearlyIncome],  
          [TotalChildren],  
          [NumberChildrenAtHome],  
          [Education],  
          [Occupation],  
          [HouseOwnerFlag],  
          [NumberCarsOwned]  
        FROM  
          [dbo].[ProspectiveBuyer]  
        ') AS t  
    ON  
      [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
7.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
8.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Batch_Prediction.dmx`.  
  
9. En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve una tabla que contiene nombres de cliente, una predicción acerca de si cada cliente adquirirá una bicicleta y la probabilidad de la predicción.  
  
 Éste es el último paso del tutorial de Bike Buyer. Ahora dispone de un conjunto de modelos de minería de datos que puede utilizar para explorar las similitudes entre sus clientes y predecir si los clientes potenciales adquirirán una bicicleta.  
  
 Para aprender a utilizar DMX en un escenario de cesta, consulte [Tutorial DMX de Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md).  
  
  
