---
title: "SystemGetAccuracyResults (Analysis Services: minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetAccuracyResults
- cross-validation [data mining]
ms.assetid: 54ff584c-c6ce-4c31-9515-0a645719bd1a
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6b2eca528b40afd905661e2508e93529159b8627
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults (Analysis Services - Minería de datos)
  Devuelve métricas de precisión de validación cruzada para una estructura de minería de datos y todos los modelos relacionados, excluidos los modelos de agrupación en clústeres.  
  
 Este procedimiento almacenado devuelve métricas para todo el conjunto de datos como una partición única. Para particionar el conjunto de datos en secciones transversales y devolver métricas para cada partición, use [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Este procedimiento almacenado no se admite para los modelos generados mediante el algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] o el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Además, para los modelos de agrupación en clústeres, use el procedimiento almacenado independiente [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estructura de minería de datos*  
 Nombre de una estructura de minería de datos en la base de datos actual.  
  
 (Requerido)  
  
 *lista de modelos*  
 Lista separada por comas de los modelos que se van a validar.  
  
 El valor predeterminado es **null**. Esto significa que se usan todos los modelos aplicables. Cuando se usa el valor predeterminado, los modelos de agrupación en clústeres se excluyen automáticamente de la lista de candidatos para el procesamiento.  
  
 (Opcional)  
  
 *conjunto de datos*  
 Valor entero que indica la partición de la estructura de minería de datos que se utiliza para realizar pruebas. El valor se deriva de una máscara de bits que representa la suma de los valores siguientes, donde cualquier valor individual es opcional:  
  
|||  
|-|-|  
|Casos de entrenamiento|0x0001|  
|Casos de prueba|0x0002|  
|Filtro de modelo|0x0004|  
  
 Para obtener una lista completa de los posibles valores, vea la sección Comentarios de este tema.  
  
 (Requerido)  
  
 *atributo de destino*  
 Cadena que contiene el nombre de un objeto de predicción. Un objeto de predicción puede ser una columna, una columna de tabla anidada o una columna de clave de tabla anidada de un modelo de minería de datos.  
  
 (Requerido)  
  
 *estado de destino*  
 Cadena que contiene un valor específico que va a predecirse.  
  
 Si se especifica un valor, se recopilan las métricas para ese estado específico.  
  
 Si no se especifica ningún valor, o se especifica null, se calculan las métricas del estado más probable para cada predicción.  
  
 El valor predeterminado es **null**.  
  
 (Opcional)  
  
 *umbral de destino*  
 Número comprendido entre 0,0 y 1 que especifica la probabilidad mínima en la que el valor de predicción se considera correcto.  
  
 El valor predeterminado es **null**, que significa que todas las predicciones se consideran correctas.  
  
 (Opcional)  
  
 *lista de pruebas*  
 Cadena que especifica las opciones de prueba. Este parámetro se reserva para uso futuro.  
  
 (Opcional)  
  
## <a name="return-type"></a>Tipo devuelto  
 El conjunto de filas que se devuelve incluye puntuaciones para cada partición y agregados para todos los modelos.  
  
 En la tabla siguiente se muestran las columnas que devuelve **GetValidationResults**.  
  
|Nombre de la columna|Description|  
|-----------------|-----------------|  
|Modelo|Nombre del modelo probado. **Todos** indica que el resultado es un agregado para todos los modelos.|  
|AttributeName|Nombre de la columna de predicción.|  
|AttributeState|Valor de destino de la columna de predicción.<br /><br /> Si esta columna contiene un valor, solo se recopilan las métricas para el estado especificado.<br /><br /> Si no se especifica este valor, o es null, se calculan las métricas del estado más probable para cada predicción.|  
|PartitionIndex|Indica la partición a la que se aplica el resultado.<br /><br /> Para este procedimiento, siempre es 0.|  
|PartitionCases|Un entero que indica el número de filas del conjunto de casos, tomando como base la  *\<conjunto de datos >* parámetro.|  
|Prueba|Tipo de prueba que se realizó.|  
|Measure|Nombre de la medida que devuelve la prueba. Las medidas para cada modelo dependen del tipo de modelo, y el tipo del valor de predicción.<br /><br /> Para obtener una lista de las medidas que se devuelven para cada tipo de predicción, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Para obtener una definición de cada medida, vea [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Value|Valor de la medida especificada.|  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se proporcionan ejemplos de los valores que puede utilizar para especificar los datos de la estructura de minería de datos que se usan para la validación cruzada. Si desea utilizar casos de prueba para la validación cruzada, la estructura de minería de datos ya debe contener un conjunto de datos de prueba. Para obtener información sobre cómo definir un conjunto de datos de prueba al crear una estructura de minería de datos, vea [Conjuntos de datos de entrenamiento y de prueba](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
|Valor entero|Description|  
|-------------------|-----------------|  
|1|Solo se utilizan casos de entrenamiento.|  
|2|Solo se utilizan casos de prueba.|  
|3|Se utilizan casos de entrenamiento y de prueba.|  
|4|Combinación no válida.|  
|5|Solo se utilizan casos de entrenamiento y se aplica el filtro de modelo.|  
|6|Solo se utilizan casos de prueba y se aplica el filtro de modelo.|  
|7|Se utilizan casos de entrenamiento y de prueba y se aplica el filtro de modelo.|  
  
 Para obtener más información sobre los escenarios en los que se usaría la validación cruzada, vea [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se devuelven medidas de precisión para un único modelo de árbol de decisión, `v Target Mail DT`, asociado a la estructura de minería de datos `vTargetMail` . El código de la línea cuatro indica que los resultados deben basarse en los casos de prueba, filtrados para cada modelo con el filtro específico de dicho modelo.  `[Bike Buyer]` especifica la columna que va a predecirse, y el 1 que aparece en la línea siguiente indica que el modelo solamente va a evaluarse para el valor específico 1, que significa que sí comprará.  
  
 La línea final del código especifica que el valor del umbral de estado es 0,5. Esto significa que las predicciones que tienen una probabilidad superior al 50 por ciento deben considerarse predicciones "buenas" a la hora de calcular la precisión.  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 Resultados del ejemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Prueba|Measure|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|1|0|1638|Clasificación|Verdadero positivo|605|  
|v Target Mail DT|Bike Buyer|1|0|1638|Clasificación|Falso positivo|177|  
|v Target Mail DT|Bike Buyer|1|0|1638|Clasificación|Verdadero negativo|501|  
|v Target Mail DT|Bike Buyer|1|0|1638|Clasificación|Falso negativo|355|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilidad|Logaritmo|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilidad|Mejora respecto al modelo predictivo|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilidad|Error cuadrático medio|0.361630800104946|  
  
## <a name="requirements"></a>Requisitos  
 La validación cruzada solo está disponible en [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  

