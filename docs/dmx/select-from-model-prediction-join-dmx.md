---
title: SELECT FROM &lt;modelo&gt; PREDICTION JOIN (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICTION
- PREDICTION_JOIN
- SELECT
- join
- FROM
- PREDICTION JOIN
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- PREDICTION JOIN statement
- natural prediction joins [DMX]
- open query predictions
- singleton query predictions [DMX]
- SELECT FROM <model> PREDICTION JOIN statement
ms.assetid: 7ca37fec-4a50-4d79-b1d6-1c7c12176946
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7caf239374a174cc26c2bee349c1a52c805f4de4
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM &lt;modelo&gt; PREDICTION JOIN (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usa un modelo de minería de datos para predecir los estados de las columnas de un origen de datos externo. El **PREDICTION JOIN** instrucción coincide con cada caso de la consulta de origen para el modelo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *Seleccione la lista de expresiones*  
 Lista delimitada por comas de expresiones o identificadores de columna derivados del modelo de minería de datos.  
  
 *model*  
 Identificador de modelo.  
  
 *Seleccione Sub*  
 Instrucción SELECT incrustada.  
  
 *consulta de origen de datos*  
 Consulta de origen.  
  
 *lista de asignación de combinación*  
 Opcional. Expresión lógica que compara columnas del modelo con columnas de la consulta de origen.  
  
 *expresión de condición*  
 Opcional. Condición para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 La cláusula ON define la asignación entre las columnas de la consulta de origen y las columnas del modelo de minería. Esta asignación sirve para unir columnas de la consulta de origen con columnas del modelo de minería de datos de forma que las columnas se puedan usar como entradas para crear las predicciones. Las columnas de la \< *lista de asignación de combinación*> están relacionadas con un signo igual (=), tal como se muestra en el ejemplo siguiente:  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 Si va a enlazar una tabla anidada de la cláusula ON, asegúrese de enlazar la columna de clave con las columnas sin clave para que el algoritmo pueda identificar correctamente el caso al que pertenece el registro de la columna anidada.  
  
 La columna de origen de la combinación de predicción puede ser una tabla o una consulta singleton.  
  
 Puede especificar funciones de predicción que no devuelven una expresión de tabla en la \< *lista de expresiones select*> y la \< *expresión de condición*>.  
  
 **NATURAL PREDICTION JOIN** asigna automáticamente juntos los nombres de columna de la consulta de origen que coinciden con los nombres de columna en el modelo. Si usa **cláusula NATURAL PREDICTION**, puede omitir la cláusula ON.  
  
 La condición WHERE solo se puede aplicar a columnas de predicción o relacionadas.  
  
 La cláusula ORDER by puede aceptar una sola columna como argumento; es decir, no se puede ordenar por más de una columna.  
  
## <a name="example-1-singleton-query"></a>Ejemplo 1: consulta singleton  
 El ejemplo siguiente muestra cómo crear una consulta para predecir si una persona determinada comprará una bicicleta en tiempo real. En esta consulta los datos no están almacenados en una tabla u otro origen de datos, sino que se especifican directamente en la consulta. La persona de la consulta tiene el siguiente perfil:  
  
-   35 años  
  
-   Tiene una casa de propiedad  
  
-   Tiene dos coches  
  
-   Tiene dos hijos que viven en casa  
  
 Con el modelo de minería de datos TM Decision Tree y las características conocidas del sujeto, la consulta devuelve un valor booleano que describe si la persona compró la bicicleta y un conjunto de valores de tabla, devuelto por la [PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md) función, que describen cómo se realizó la predicción.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>Ejemplo 2: usar OPENQUERY  
 En el ejemplo siguiente se muestra cómo crear una consulta de predicción por lotes mediante una lista de clientes potenciales almacenada en un conjunto de datos externo. Dado que la tabla forma parte de una vista del origen de datos que se ha definido en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede usar la consulta [OPENQUERY](../dmx/source-data-query-openquery.md) para recuperar los datos. Dado que los nombres de las columnas de la tabla son diferentes de los del modelo de minería de datos, el **ON** cláusula debe usarse para asignar las columnas de la tabla a las columnas del modelo.  
  
 La consulta devuelve nombre y el apellido de cada persona de la tabla, junto con una columna booleana que indica si es probable que cada persona compre una bicicleta, donde 0 significa que "probablemente no comprará una bicicleta" y 1 significa que "probablemente comprará una bicicleta". La última columna contiene la probabilidad del resultado predicho.  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
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
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 Para restringir el conjunto de datos únicamente a los clientes de los que se ha predicho que comprarán una bicicleta y, a continuación, ordenar la lista por el nombre del cliente, puede agregar una cláusula WHERE y una cláusula ORDER BY al ejemplo anterior:  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>Ejemplo 3: predecir las asociaciones  
 En el ejemplo siguiente se muestra cómo crear una predicción usando un modelo generado a partir del algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)]. Las predicciones en un modelo de asociación se pueden utilizar para recomendar productos relacionados. Por ejemplo, la consulta siguiente devuelve los tres productos que es más probable que se compren juntos:  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 El [Predict &#40; DMX &#41;](../dmx/predict-dmx.md) función es polimórfica y puede utilizarse con todos los tipos de modelo. El valor de value3 se usa como argumento para la función con el fin de limitar el número de elementos que devuelve la consulta. El **seleccione** lista que sigue a la cláusula NATURAL PREDICTION JOIN proporciona los valores que se usará como entrada para la predicción.  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 Dado que la columna que contiene el atributo de predicción, `[v Assoc Seq Line Items]`, es una columna de la tabla, la consulta devuelve una única columna que contiene una tabla anidada. De forma predeterminada, la columna de tabla anidada se denomina `Expression`. Si el proveedor no admite conjuntos de filas jerárquicos, puede usar el **FLATTENED** palabra clave tal y como se muestra en este ejemplo para que sea más fácil ver los resultados.  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

