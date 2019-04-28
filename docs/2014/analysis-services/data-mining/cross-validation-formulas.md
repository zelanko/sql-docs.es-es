---
title: Fórmulas de validación cruzada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fd1ea582-29a1-4154-8de2-47bab3539b4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0f3d10776e661eaa15ed39a141fe06608d8dbde
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722637"
---
# <a name="cross-validation-formulas"></a>Fórmulas de validación cruzada
  Cuando se genera un informe de validación cruzada, contiene medidas de precisión para cada modelo según el tipo de modelo de minería de datos (es decir, el algoritmo utilizado para crear el modelo), el tipo de datos del atributo de predicción y el valor de atributo de predicción, si existe.  
  
 En esta sección se enumeran las medidas que se usan en el informe de validación cruzada y se describe el método de cálculo.  
  
 Para ver un desglose de las medidas de precisión por tipo de modelo, vea [Medidas en el informe de validación cruzada](measures-in-the-cross-validation-report.md).  
  
## <a name="formulas-used-for-cross-validation-measures"></a>Fórmulas utilizadas para las medidas de validación cruzada  
  
> [!NOTE]  
>  **Importante:** Estas medidas de precisión se calculan para cada atributo de destino. Para cada atributo, puede especificar u omitir un valor de destino. Si un caso del conjunto de datos no tiene ningún valor para el atributo de destino, el caso se trata como si tuviera un valor especial denominado *valor ausente*. Las filas que tienen valores ausentes no se cuentan al calcular la medida de precisión para un atributo de destino concreto. Observe que, dado que las puntuaciones se calculan para cada atributo individualmente, si los valores están presentes para el atributo de destino pero faltan para otros atributos, no afectan a la puntuación para el atributo de destino.  
  
|Measure|Se aplica a|Implementación|  
|-------------|----------------|--------------------|  
|**Verdadero positivo**|Atributo discreto, se especifica el valor.|Recuento de casos que cumplen estas condiciones:<br /><br /> El caso contiene el valor de destino.<br /><br /> El modelo predijo que ese caso contendría el valor de destino.|  
|**Verdadero negativo**|Atributo discreto, se especifica el valor.|Recuento de casos que cumplen estas condiciones:<br /><br /> El caso no contiene el valor de destino.<br /><br /> El modelo predijo que el caso no contendría el valor de destino.|  
|**Falso positivo**|Atributo discreto, se especifica el valor.|Recuento de casos que cumplen estas condiciones:<br /><br /> El valor real es igual al valor de destino.<br /><br /> El modelo predijo que ese caso contendría el valor de destino.|  
|**Falso negativo**|Atributo discreto, se especifica el valor.|Recuento de casos que cumplen estas condiciones:<br /><br /> El valor real no es igual al valor de destino.<br /><br /> El modelo predijo que el caso no contendría el valor de destino.|  
|**Sin errores/error**|Atributo discreto, sin destino especificado|Recuento de casos que cumplen estas condiciones:<br /><br /> Sin errores en caso de que el estado predicho con la máxima probabilidad es igual al estado de entrada y la probabilidad es mayor que el valor de **Umbral de estado**.<br /><br /> De lo contrario, se producirá un error.|  
|**Mejora respecto al modelo predictivo**|Atributo discreto. Se puede especificar el valor de destino pero no es necesario.|La probabilidad de logaritmo medio para todas las filas con valores para el atributo de destino, donde la probabilidad de logaritmo para cada caso se calcula como Log(ActualProbability/MarginalProbability). Para calcular la media, la suma de los valores de probabilidad logarítmica se divide entre el número de filas del conjunto de datos de entrada, excluidas las filas sin valores para el atributo de destino.<br /><br /> La mejora respecto al modelo predictivo puede ser un valor positivo o negativo. Un valor positivo indica que estamos ante un modelo eficaz que supera la estimación aleatoria.|  
|**Logaritmo**|Atributo discreto. Se puede especificar el valor de destino pero no es necesario.|Logaritmo de la probabilidad real de cada caso, sumada y después dividida entre el número de filas del conjunto de datos de entrada, excluidas las filas sin valores para el atributo de destino.<br /><br /> Como la probabilidad se representa como una fracción decimal, las puntuaciones del registro son siempre números negativos. Una puntuación más cercana a 0 es una puntuación mejor.|  
|**Probabilidad de casos**|Clúster|Suma de las puntuaciones de probabilidad de clúster para todos los casos, dividida entre el número de casos de la partición, excluidas las filas sin valores para el atributo de destino.|  
|**Desviación media**|Atributo continuo|Suma del error absoluto para todos los casos de la partición, dividida entre el número de casos de la partición.|  
|**Error cuadrático medio**|Atributo continuo|Raíz cuadrada del error cuadrático medio para la partición.|  
|**Error cuadrático medio**|Atributo discreto. Se puede especificar el valor de destino pero no es necesario.|Raíz cuadrada de la media de los cuadrados del complemento de la puntuación de probabilidad, dividida entre el número de casos de la partición, excluidas las filas sin valores para el atributo de destino.|  
|**Error cuadrático medio**|Atributo discreto, sin destino especificado.|Raíz cuadrada de la media de los cuadrados del complemento de la puntuación de probabilidad, dividida entre el número de casos de la partición, excluidos los casos sin valores para el atributo de destino.|  
  
## <a name="see-also"></a>Vea también  
 [Prueba y validación &#40;minería de datos&#41;](testing-and-validation-data-mining.md)   
 [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](cross-validation-analysis-services-data-mining.md)  
  
  
