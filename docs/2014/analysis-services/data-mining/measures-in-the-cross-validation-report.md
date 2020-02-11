---
title: Medidas en el informe de validación cruzada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- root mean square error [data mining]
- cross-validation [data mining]
- mean absolute error [data mining]
- log score [data mining]
- likelihood [data mining]
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30f8daab91172863ba18c6b75529063555b61afc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084158"
---
# <a name="measures-in-the-cross-validation-report"></a>Medidas en el informe de validación cruzada
  Durante la validación cruzada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] divide los datos de una estructura de minería de datos en varias secciones transversales y, a continuación, va probando de forma iterativa la estructura y los modelos de minería de datos asociados. En función de este análisis, genera un conjunto de medidas estándar de precisión para la estructura y para cada modelo.  
  
 El informe contiene cierta información básica acerca del número de subconjuntos de los datos y de la cantidad de datos en cada subconjunto, además de un conjunto de métricas generales que describen la distribución de los datos. Si compara las métricas generales para cada sección transversal, puede evaluar la confiabilidad de la estructura o el modelo.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también muestra un conjunto de medidas detalladas para los modelos de minería de datos. Estas medidas dependen del tipo de modelo y del tipo de atributo que se está analizando: por ejemplo, si es discreto o continuo.  
  
 En esta sección se proporciona una lista de las medidas contenidas en el informe de **Validación cruzada** y su significado. Para más información sobre cómo se calcula cada medida, vea [Fórmulas de validación cruzada](cross-validation-formulas.md).  
  
## <a name="list-of-measures-in-the-cross-validation-report"></a>Lista de medidas del informe de validación cruzada  
 En la tabla siguiente se enumeran las medidas que aparecen en el informe de validación cruzada. Las medidas se agrupan según el *tipo de prueba*, que se indica en la columna izquierda de la tabla siguiente. La columna de la derecha contiene el nombre de la medida tal como aparece en el informe, junto con una breve explicación de lo que significa.  
  
|tipo de prueba|Medidas y descripciones|  
|---------------|-------------------------------|  
|agrupación en clústeres|Medidas que se aplican a los modelos de agrupación en clústeres:<br /><br /> **Probabilidad de caso**: esta medida suele indicar la probabilidad de que un caso pertenezca a un clúster determinado. <br />                      Para la validación cruzada, las puntuaciones se suman y luego se dividen entre el número de casos, de modo que aquí la puntuación es una media de la probabilidad de los casos.|  
|clasificación|Medidas que se aplican a los modelos de clasificación:<br /><br /> **Verdadero positivo**/<br />                      **Verdadero negativo**/ **falso positivo**/ **falso positivo**: recuento de filas o valores de la partición en la que el estado de predicción coincide con el estado de destino y la probabilidad de predicción es mayor que el umbral especificado. Se excluyen los casos que tienen valores ausentes para el atributo de destino, lo que significa que es posible que los recuentos de todos los valores no se agreguen|  
||**Pass/Fail**: recuento de filas o valores de la partición en la que el estado de predicción coincide con el estado de destino, y donde el valor de la probabilidad de predicción es mayor que 0.|  
|Probabilidad|Las medidas de probabilidad se aplican a varios tipos de modelos:<br /><br /> **Levantar**: la relación entre la probabilidad de predicción real y la probabilidad marginal en los casos de prueba. Se excluyen las filas a las que les falta el valor para el atributo de destino. Esta medida normalmente muestra la mejora de la probabilidad del resultado de destino cuando se usa el modelo.<br /><br /> **Error medio cuadrado raíz**: raíz cuadrada del error promedio para todos los casos de partición, dividido por el número de casos de la partición, excluidas las filas que tienen valores ausentes para el atributo de destino. RMSE es un estimador popular para los modelos predictivos. La puntuación calcula el promedio de los valores residuales para cada caso con objeto de producir un único indicador del error del modelo.<br /><br /> **Puntuación de registro**: logaritmo de la probabilidad real de cada caso, sumada y después dividida entre el número de filas del conjunto de datos de entrada, excluidas las filas que tienen valores ausentes para el atributo de destino. Como la probabilidad se representa como una fracción decimal, las puntuaciones del registro son siempre números negativos. Un número más próximo a 0 es una puntuación mejor. Mientras que las puntuaciones sin formato pueden tener distribuciones muy irregulares o sesgadas, un logaritmo es similar a un porcentaje.|  
|Estimación|Medidas que se aplican solo a los modelos de estimación, que predicen un atributo numérico continuo:<br /><br /> **Error medio cuadrado raíz**: error promedio cuando el valor predicho se compara con el valor real. RMSE es un estimador popular para los modelos predictivos. La puntuación calcula el promedio de los valores residuales para cada caso con objeto de producir un único indicador del error del modelo.<br /><br /> **Error medio absoluto**: error promedio cuando los valores predichos se comparan con los valores reales, calculado como la media de la suma absoluta de los errores. La desviación media es útil para comprender lo cercanas que se encontraban las predicciones globales de los valores reales. Una puntuación menor significa que las predicciones fueron más precisas.<br /><br /> **Puntuación de registro**: logaritmo de la probabilidad real de cada caso, sumada y después dividida entre el número de filas del conjunto de datos de entrada, excluidas las filas que tienen valores ausentes para el atributo de destino. Como la probabilidad se representa como una fracción decimal, las puntuaciones del registro son siempre números negativos. Un número más próximo a 0 es una puntuación mejor. Mientras que las puntuaciones sin formato pueden tener distribuciones muy irregulares o sesgadas, un logaritmo es similar a un porcentaje.|  
|Agregados|Las medidas de agregado proporcionan una indicación de la varianza en los resultados para cada partición:<br /><br /> **Average: promedio**de los valores de partición para una medida determinada.<br /><br /> **Desviación estándar**: promedio de la desviación de la media para una medida específica, en todas las particiones de un modelo. Para la validación cruzada, un valor mayor para esta puntuación implica una variación sustancial entre los subconjuntos.|  
  
## <a name="see-also"></a>Consulte también  
 [Pruebas y validación &#40;&#41;de minería de datos](testing-and-validation-data-mining.md)  
  
  
