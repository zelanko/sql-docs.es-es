---
title: 'SystemGetClusterCrossValidationResults (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: beb42d42e471b628d3985d4cf5ae9b3537a80d1f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="systemgetclustercrossvalidationresults-analysis-services---data-mining"></a>SystemGetClusterCrossValidationResults (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Particiona la estructura de minería de datos en el número especificado de secciones transversales, entrena un modelo para cada partición y, a continuación, devuelve métricas de precisión para cada partición.  
  
 **Nota** : este procedimiento almacenado solamente se puede utilizar con una estructura de minería de datos que contiene al menos un modelo de agrupación en clústeres. Para realizar una validación cruzada de modelos que no son de agrupación en clústeres, hay que usar [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estructura de minería de datos*  
 Nombre de una estructura de minería de datos en la base de datos actual.  
  
 (Obligatorio)  
  
 *lista de modelos de minería de datos*  
 Lista separada por comas de los modelos de minería de datos que van a validarse.  
  
 Si no se especifica una lista de modelos de minería de datos, la validación cruzada se realiza en todos los modelos de agrupación en clústeres asociados a la estructura especificada.  
  
> [!NOTE]  
>  Para realizar una validación cruzada de modelos que no son de agrupación en clústeres, hay que usar un procedimiento almacenado aparte, [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
 (opcional)  
  
 *recuento de plegamientos*  
 Entero que especifica el número de particiones en que debe separarse el conjunto de datos. El valor mínimo es 2. El número máximo de subconjuntos es **maximum integer** o el número de casos, el que sea más bajo.  
  
 Cada partición contendrá aproximadamente este número de casos: *número máximo de casos*/*recuento de plegamientos*.  
  
 No existe ningún valor predeterminado.  
  
> [!NOTE]  
>  El número de subconjuntos afecta enormemente al tiempo necesario para realizar la validación cruzada. Si selecciona un número demasiado alto, puede que la consulta se ejecute durante mucho tiempo y, en algunos casos, es posible que el servidor deje de responder o que se agote el tiempo de espera.  
  
 (Obligatorio)  
  
 *número máximo de casos*  
 Entero que especifica el número máximo de casos que se pueden probar.  
  
 Un valor igual a 0 indica que se usarán todos los casos del origen de datos.  
  
 Si especifica un número superior al número real de casos del conjunto de datos, se utilizarán todos los casos del origen de datos.  
  
 (Obligatorio)  
  
 *lista de pruebas*  
 Cadena que especifica las opciones de prueba.  
  
 **Nota** : este parámetro se reserva para un uso futuro.  
  
 (opcional)  
  
## <a name="return-type"></a>Tipo devuelto  
 La tabla Tipo devuelto contiene puntuaciones para cada partición individual y agregados para todos los modelos.  
  
 En la tabla siguiente se describen las columnas que devuelve.  
  
|Nombre de la columna|Description|  
|-----------------|-----------------|  
|ModelName|Nombre del modelo probado.|  
|AttributeName|Nombre de la columna de predicción. Para los modelos de clústeres, siempre es **null**.|  
|AttributeState|Valor de destino especificado en la columna de predicción. Para los modelos de clústeres, siempre es **null.**|  
|PartitionIndex|Índice basado en 1 que identifica a qué partición se aplican los resultados.|  
|PartitionSize|Entero que indica el número de casos incluido en cada partición.|  
|Prueba|Tipo de prueba que se realizó.|  
|Measure|Nombre de la medida que devuelve la prueba. Las medidas de cada modelo dependen del tipo del valor de predicción. Para obtener una definición de cada medida, vea [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Para obtener una lista de las medidas que se devuelven para cada tipo de predicción, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Value|Valor de la medida de prueba especificada.|  
  
## <a name="remarks"></a>Comentarios  
 Para devolver métricas de precisión de todo el conjunto de datos, use [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
 Además, si el modelo de minería de datos ya se ha particionado en subconjuntos, puede omitir el procesamiento y devolver solamente los resultados de la validación cruzada por medio de [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo particionar una estructura de minería de datos en tres subconjuntos y probar, a continuación, dos modelos de agrupación en clústeres asociados a la estructura de minería de datos.  
  
 La línea tres del código muestra los modelos específicos de minería de datos que desea probar. Si no especifica la lista, se utilizan todos los modelos de agrupación en clústeres asociados a la estructura.  
  
 La línea cuatro del código especifica el número de subconjuntos y la línea cinco especifica el número máximo de casos que deben utilizarse.  
  
 Dado que se trata de modelos de agrupación en clústeres, no es necesario especificar un atributo o valor de predicción.  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 Resultados del ejemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Prueba|Medida|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Clúster 1|||1|3025|Agrupación en clústeres|Probabilidad de casos|0.930524511864121|  
|Clúster 1|||2|3025|Agrupación en clústeres|Probabilidad de casos|0.919184178430778|  
|Clúster 1|||3|3024|Agrupación en clústeres|Probabilidad de casos|0.929651120490248|  
|Clúster 2|||1|1289|Agrupación en clústeres|Probabilidad de casos|0.922789726933607|  
|Clúster 2|||2|1288|Agrupación en clústeres|Probabilidad de casos|0.934865535691068|  
|Clúster 2|||3|1288|Agrupación en clústeres|Probabilidad de casos|0.924724595688798|  
  
## <a name="requirements"></a>Requisitos  
 La validación cruzada solo está disponible en [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services: minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
