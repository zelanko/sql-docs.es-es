---
title: "SystemGetCrossValidationResults (Analysis Services: minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SystemGetCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: f70c3337-c930-434a-b278-caf1ef0c3b3b
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 499e62070cb0ec0fed8e814c926d915f7e69bbe3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Particiones de la minería de datos de la estructura en el número especificado de secciones transversales, entrena un modelo para cada partición y, a continuación, devuelve métricas de precisión para cada partición.  
  
> [!NOTE]  
>  Este procedimiento almacenado no puede usarse para realizar una validación cruzada de los modelos de agrupación en clústeres ni de los modelos generados con el algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] o el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para realizar una validación cruzada de modelos de agrupación en clústeres, puede usar un procedimiento almacenado aparte, [SystemGetClusterCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estructura de minería de datos*  
 Nombre de una estructura de minería de datos en la base de datos actual.  
  
 (Obligatorio)  
  
 *lista de modelos de minería de datos*  
 Lista separada por comas de los modelos de minería de datos que van a validarse.  
  
 Si un nombre de modelo contiene caracteres que no son válidos para el nombre de un identificador, el nombre debe incluirse entre corchetes.  
  
 Si no se especifica una lista de modelos de minería de datos, la validación cruzada se realiza en todos los modelos que están asociados a la estructura especificada y que contienen un atributo de predicción.  
  
> [!NOTE]  
>  Para realizar una validación cruzada de modelos de agrupación en clústeres, debe usar un procedimiento almacenado aparte, [SystemGetClusterCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
 (opcional)  
  
 *recuento de plegamientos*  
 Entero que especifica el número de particiones en que debe separarse el conjunto de datos. El valor mínimo es 2. El número máximo de subconjuntos es **maximum integer** o el número de casos, el que sea más bajo.  
  
 Cada partición contendrá aproximadamente este número de casos: *número máximo de casos*/*recuento de plegamientos*.  
  
 No existe ningún valor predeterminado.  
  
> [!NOTE]  
>  El número de subconjuntos afecta significativamente al tiempo necesario para realizar la validación cruzada. Si selecciona un número demasiado alto, puede que la ejecución de la consulta dure mucho tiempo y, en algunos casos, es posible que el servidor deje de responder o que se agote el tiempo de espera.  
  
 (Obligatorio)  
  
 *número máximo de casos*  
 Entero que especifica el número máximo de casos que pueden probarse en todos los subconjuntos.  
  
 Un valor igual a 0 indica que se usarán todos los casos del origen de datos.  
  
 Si especifica un valor superior al número real de casos del conjunto de datos, se usarán todos los casos del origen de datos.  
  
 No existe ningún valor predeterminado.  
  
 (Obligatorio)  
  
 *atributo de destino*  
 Cadena que contiene el nombre del atributo de predicción. Un atributo de predicción puede ser una columna, una columna de tabla anidada o una columna de clave de tabla anidada de un modelo de minería de datos.  
  
> [!NOTE]  
>  La existencia del atributo de destino solamente se valida en tiempo de ejecución.  
  
 (Obligatorio)  
  
 *estado de destino*  
 Fórmula que especifica el valor que va a predecirse. Si se especifica un valor de destino, solo se recopilan las métricas para el valor especificado.  
  
 Si no se especifica ningún valor, o es **null**, se calculan las métricas del estado más probable para cada predicción.  
  
 El valor predeterminado es **null**.  
  
 Se produce un error durante la validación si el valor indicado no es válido para el atributo especificado o si la fórmula no es del tipo correcto para dicho atributo.  
  
 (opcional)  
  
 *umbral*  *de destino*  
 **Doble** mayor que 0 y menor que 1. Indica la puntuación de probabilidad mínima que debe obtenerse para que la predicción de estado del destino especificado se considere correcta.  
  
 Una predicción con una probabilidad menor o igual que este valor se considera incorrecta.  
  
 Si no se ha especificado ningún valor o si el valor es **null**, se usa el estado más probable, sin tener en cuenta su puntuación de probabilidad.  
  
 El valor predeterminado es **null**.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]no se producirá un error si se establece *umbral de estado* en 0,0, pero nunca se debe utilizar este valor. De hecho, un umbral de 0,0 significa que las predicciones con una probabilidad del cero por ciento se consideran correctas.  
  
 (opcional)  
  
 *lista de pruebas*  
 Cadena que especifica las opciones de prueba.  
  
 **Nota** : este parámetro se reserva para un uso futuro.  
  
 (opcional)  
  
## <a name="return-type"></a>Tipo devuelto  
 El conjunto de filas que se devuelve incluye puntuaciones para cada una de las particiones de cada modelo.  
  
 En la tabla siguiente se describen las columnas del conjunto de filas.  
  
|Nombre de la columna|Description|  
|-----------------|-----------------|  
|ModelName|Nombre del modelo probado.|  
|AttributeName|Nombre de la columna de predicción.|  
|AttributeState|Valor de destino especificado en la columna de predicción. Si este valor es **null**, significa que se ha utilizado la predicción más probable.<br /><br /> Si esta columna contiene un valor, la precisión del modelo solamente se evalúa en relación con este valor.|  
|PartitionIndex|Índice de base 1 que identifica la partición a la que se aplican los resultados.|  
|PartitionSize|Entero que indica el número de casos incluido en cada partición.|  
|Prueba|Categoría de la prueba realizada. Para obtener una descripción de las categorías y las pruebas incluidas en cada categoría, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Measure|Nombre de la medida que devuelve la prueba. Las medidas de cada modelo dependen del tipo del valor de predicción. Para obtener una definición de cada medida, vea [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Para obtener una lista de las medidas que se devuelven para cada tipo de predicción, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Valor|Valor de la medida de prueba especificada.|  
  
## <a name="remarks"></a>Notas  
 Para devolver métricas de precisión del conjunto de datos completo, use [SystemGetAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
 Si el modelo de minería de datos ya se ha particionado en subconjuntos, puede omitir el procesamiento y devolver solamente los resultados de la validación cruzada por medio de [SystemGetAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo particionar una estructura de minería de datos en dos subconjuntos de cara a la validación cruzada y cómo probar a continuación dos modelos de minería de datos asociados a la estructura de minería de datos `[v Target Mail]`.  
  
 La línea tres del código muestra los modelos de minería de datos que desea probar. Si no especifica la lista, se usan todos los modelos asociados a la estructura que no son de agrupación en clústeres. La línea cuatro del código especifica el número de particiones. Dado que no se especifica ningún valor para *max cases*, se usan todos los casos de la estructura de minería de datos y se distribuyen uniformemente en las particiones.  
  
 En la línea cinco se especifica el atributo de predicción, Bike Buyer, y en la línea seis se especifica el valor que va a predecirse, 1 (que significa que sí comprará).  
  
 El valor NULL de la línea siete indica que no hay ninguna barra de probabilidad mínima que deba alcanzarse. Por lo tanto, la primera predicción que tenga una probabilidad distinta de cero se usará para evaluar la precisión.  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 Resultados del ejemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Prueba|Medida|Valor|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|1|1|500|Clasificación|Verdadero positivo|144|  
|Target Mail DT|Bike Buyer|1|1|500|Clasificación|Falso positivo|105|  
|Target Mail DT|Bike Buyer|1|1|500|Clasificación|Verdadero negativo|186|  
|Target Mail DT|Bike Buyer|1|1|500|Clasificación|Falso negativo|65|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilidad|Logaritmo|-0.619042807138345|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilidad|Mejora respecto al modelo predictivo|0.0740963734002671|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilidad|Error cuadrático medio|0.346946279977653|  
|Target Mail DT|Bike Buyer|1|2|500|Clasificación|Verdadero positivo|162|  
|Target Mail DT|Bike Buyer|1|2|500|Clasificación|Falso positivo|86|  
|Target Mail DT|Bike Buyer|1|2|500|Clasificación|Verdadero negativo|165|  
|Target Mail DT|Bike Buyer|1|2|500|Clasificación|Falso negativo|87|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilidad|Logaritmo|-0.654117781086519|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilidad|Mejora respecto al modelo predictivo|0.038997399132084|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilidad|Error cuadrático medio|0.342721344892651|  
  
## <a name="requirements"></a>Requisitos  
 La validación cruzada solo está disponible en [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
