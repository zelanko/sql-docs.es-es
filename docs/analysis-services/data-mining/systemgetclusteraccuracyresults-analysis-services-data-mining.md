---
title: "SystemGetClusterAccuracyResults (Analysis Services: minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetClusterAccuracyResults
- cross-validation [data mining]
ms.assetid: e1701738-50d5-46b4-b406-f1e800545abb
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e31548023acfa5ef3c202b978d7be3c46d788a0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults (Analysis Services - Minería de datos)
  Devuelve métricas de precisión de validación cruzada para una estructura de minería de datos y los modelos de agrupación en clústeres relacionados.  
  
 Este procedimiento almacenado devuelve métricas para todo el conjunto de datos como partición única. Para particionar el conjunto de datos en secciones transversales y devolver métricas para cada partición, use [SystemGetClusterCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Este procedimiento almacenado solamente funciona para los modelos de agrupación en clústeres. Para los modelos que no sean de agrupación en clústeres, use [SystemGetAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estructura de minería de datos*  
 Nombre de una estructura de minería de datos en la base de datos actual.  
  
 (Requerido)  
  
 *lista de modelos de minería de datos*  
 Lista separada por comas de los modelos que se van a validar.  
  
 El valor predeterminado es **null**, lo que significa que se utilizan todos los modelos aplicables. Cuando se utiliza el valor predeterminado, los modelos que no son de agrupación en clústeres se excluyen automáticamente de la lista de candidatos para el procesamiento.  
  
 (Opcional)  
  
 *conjunto de datos*  
 Valor entero que indica la partición de la estructura de minería de datos que se va a utilizar para realizar pruebas. El valor se deriva de una máscara de bits que representa la suma de los valores siguientes, donde cualquier valor individual es opcional:  
  
|||  
|-|-|  
|Casos de entrenamiento|0x0001|  
|Casos de prueba|0x0002|  
|Filtro de modelo|0x0004|  
  
 Para obtener una lista completa de los posibles valores, vea la sección Comentarios de este tema.  
  
 (Requerido)  
  
 *lista de pruebas*  
 Cadena que especifica las opciones de prueba. Este parámetro se reserva para uso futuro.  
  
 (Opcional)  
  
## <a name="return-type"></a>Tipo devuelto  
 Tabla que contiene puntuaciones para cada partición individual y agregados para todos los modelos.  
  
 En la tabla siguiente se muestran las columnas que devuelve **SystemGetClusterAccuracyResults**. Para obtener más información sobre cómo interpretar la información que devuelve el procedimiento almacenado, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
|Nombre de la columna|Description|  
|-----------------|-----------------|  
|ModelName|Nombre del modelo probado. **Todos** indica que el resultado es un agregado para todos los modelos.|  
|AttributeName|No aplicable a los modelos de agrupación en clústeres.|  
|AttributeState|No aplicable a los modelos de agrupación en clústeres.|  
|PartitionIndex|Número que indica la partición.<br /><br /> Para este procedimiento almacenado, el número siempre es 0.|  
|PartitionCases|Entero que indica el número de casos que se han probado.|  
|Prueba|Tipo de prueba que se realizó.|  
|Measure|Nombre de la medida que devuelve la prueba. Las medidas para cada modelo dependen del tipo de modelo, y el tipo del valor de predicción.<br /><br /> Para obtener una lista de las medidas que se devuelven para cada tipo de predicción, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Para obtener una definición de cada medida, vea [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Value|Puntuación de probabilidad que indica la probabilidad del caso de clúster.|  
  
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
 En este ejemplo se devuelven medidas de precisión para dos modelos de agrupación en clústeres, denominados `Cluster 1` y `Cluster 2`, que están asociados a la estructura de minería de datos vTargetMail. El código de la línea cuatro indica que los resultados deben basarse solamente en los casos de prueba, sin utilizar ningún filtro que pueda estar asociado a cada modelo.  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 Resultados del ejemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Prueba|Measure|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Clúster 1|||0|5545|Agrupación en clústeres|Probabilidad de casos|0.796514342249313|  
|Clúster 2|||0|5545|Agrupación en clústeres|Probabilidad de casos|0.732122471228572|  
  
## <a name="requirements"></a>Requisitos  
 La validación cruzada solo está disponible en [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  

