---
title: SELECCIONAR una &lt;combinación&gt; de predicción de modelo (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b592aef0ba3831c5513e039ee4552d826468e819
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928330"
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>Seleccionar de &lt;la&gt; combinación de predicción de modelo (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Usa un modelo de minería de datos para predecir los estados de las columnas de un origen de datos externo. La instrucción de **combinación de predicción** coincide con cada caso de la consulta de origen con el modelo.  
  
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
  
 *seleccionar lista de expresiones*  
 Lista delimitada por comas de expresiones o identificadores de columna derivados del modelo de minería de datos.  
  
 *model*  
 Identificador de modelo.  
  
 *Subselección*  
 Instrucción SELECT incrustada.  
  
 *consulta de datos de origen*  
 Consulta de origen.  
  
 *lista de asignación de combinación*  
 Opcional. Expresión lógica que compara columnas del modelo con columnas de la consulta de origen.  
  
 *expresión de condición*  
 Opcional. Condición para restringir los valores que devuelve la lista de columnas.  
  
 *Expresiones*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 La cláusula ON define la asignación entre las columnas de la consulta de origen y las columnas del modelo de minería. Esta asignación sirve para unir columnas de la consulta de origen con columnas del modelo de minería de datos de forma que las columnas se puedan usar como entradas para crear las predicciones. Las columnas de \<la *lista de asignación de combinación*> están relacionadas mediante el uso de un signo igual (=), como se muestra en el ejemplo siguiente:  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 Si va a enlazar una tabla anidada de la cláusula ON, asegúrese de enlazar la columna de clave con las columnas sin clave para que el algoritmo pueda identificar correctamente el caso al que pertenece el registro de la columna anidada.  
  
 La columna de origen de la combinación de predicción puede ser una tabla o una consulta singleton.  
  
 Puede especificar funciones de predicción que no devuelven una expresión de tabla \<en la *lista de expresiones SELECT*> y la \< *expresión de condición*>.  
  
 La **combinación de predicción natural** asigna automáticamente nombres de columna de la consulta de origen que coinciden con los nombres de columna del modelo. Si usa la **predicción natural**, puede omitir la cláusula ON.  
  
 La condición WHERE solo se puede aplicar a columnas de predicción o relacionadas.  
  
 La cláusula ORDER BY solo puede aceptar una columna como argumento; es decir, no puede ordenar por más de una columna.  
  
## <a name="example-1-singleton-query"></a>Ejemplo 1: consulta singleton  
 El ejemplo siguiente muestra cómo crear una consulta para predecir si una persona determinada comprará una bicicleta en tiempo real. En esta consulta los datos no están almacenados en una tabla u otro origen de datos, sino que se especifican directamente en la consulta. La persona de la consulta tiene el siguiente perfil:  
  
-   35 años  
  
-   Tiene una casa de propiedad  
  
-   Tiene dos coches  
  
-   Tiene dos hijos que viven en casa  
  
 Con el modelo de minería de datos TM decision Tree y las características conocidas sobre el sujeto, la consulta devuelve un valor booleano que describe si la persona compró la bicicleta y un conjunto de valores tabulares, devueltos por la función [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) , que describen cómo se realizó la predicción.  
  
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
 En el ejemplo siguiente se muestra cómo crear una consulta de predicción por lotes mediante una lista de clientes potenciales almacenados en un conjunto de elementos externo. Dado que la tabla forma parte de una vista del origen de datos que se ha definido en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]una instancia de, la consulta puede utilizar [OPENQUERY](../dmx/source-data-query-openquery.md) para recuperar los datos. Dado que los nombres de las columnas de la tabla son distintos de los del modelo de minería de datos, se debe usar la cláusula **on** para asignar las columnas de la tabla a las columnas del modelo.  
  
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
  
 La función [PREDICT &#40;DMX&#41;](../dmx/predict-dmx.md) es polimórfica y se puede usar con todos los tipos de modelo. El valor de value3 se usa como argumento para la función con el fin de limitar el número de elementos que devuelve la consulta. La lista de **selección** que sigue a la cláusula de combinación de predicción natural proporciona los valores que se usarán como entrada para la predicción.  
  
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
  
 Resultados de ejemplo:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 Dado que la columna que contiene el atributo de predicción, `[v Assoc Seq Line Items]`, es una columna de la tabla, la consulta devuelve una única columna que contiene una tabla anidada. De forma predeterminada, la columna de tabla anidada se denomina `Expression`. Si el proveedor no admite conjuntos de filas jerárquicos, puede utilizar la palabra clave **Aplanad** tal como se muestra en este ejemplo para que los resultados sean más fáciles de ver.  
  
## <a name="see-also"></a>Consulte también  
 [SELECCIONE &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
