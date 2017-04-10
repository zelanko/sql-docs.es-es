---
title: "Medidas en el informe de validaci&#243;n cruzada | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error cuadrático medio [minería de datos]"
  - "validación cruzada [minería de datos]"
  - "error absoluto medio [minería de datos]"
  - "puntuación de registro [minería de datos]"
  - "probabilidad [minería de datos]"
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 28
---
# Medidas en el informe de validaci&#243;n cruzada
  Durante la validación cruzada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] divide los datos de una estructura de minería de datos en varias secciones transversales y, a continuación, va probando de forma iterativa la estructura y los modelos de minería de datos asociados. En función de este análisis, genera un conjunto de medidas estándar de precisión para la estructura y para cada modelo.  
  
 El informe contiene cierta información básica acerca del número de subconjuntos de los datos y de la cantidad de datos en cada subconjunto, además de un conjunto de métricas generales que describen la distribución de los datos. Si compara las métricas generales para cada sección transversal, puede evaluar la confiabilidad de la estructura o el modelo.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también muestra un conjunto de medidas detalladas para los modelos de minería de datos. Estas medidas dependen del tipo de modelo y del tipo de atributo que se está analizando: por ejemplo, si es discreto o continuo.  
  
 En esta sección se proporciona una lista de las medidas contenidas en el informe de **Validación cruzada** y su significado. Para más información sobre cómo se calcula cada medida, vea [Fórmulas de validación cruzada](../../analysis-services/data-mining/cross-validation-formulas.md).  
  
## Lista de medidas del informe de validación cruzada  
 En la tabla siguiente se enumeran las medidas que aparecen en el informe de validación cruzada. Las medidas se agrupan según el *tipo de prueba*, que se indica en la columna izquierda de la tabla siguiente. La columna de la derecha contiene el nombre de la medida tal como aparece en el informe, junto con una breve explicación de lo que significa.  
  
|Tipo de prueba|Medidas y descripciones|  
|---------------|-------------------------------|  
|Agrupación en clústeres|Medidas relacionadas con los modelos de agrupación en clústeres|  
||**Probabilidad de casos**:<br />                      Esta medida suele indicar la probabilidad de que un caso pertenezca a un clúster determinado. Para la validación cruzada, las puntuaciones se suman y luego se dividen entre el número de casos, de modo que aquí la puntuación es una media de la probabilidad de los casos.|  
|Clasificación|Medidas relacionadas con los modelos de clasificación|  
||**Verdadero positivo**/**Verdadero negativo**/**Falso positivo**/**Falso negativo**:<br /><br /> Recuento de filas o valores de la partición cuyo estado predicho coincide con el estado de destino y cuya probabilidad de predicción es mayor que el umbral de estado especificado.<br /><br /> Se excluyen los casos a los que les faltan valores para el atributo de destino, lo que significa que los recuentos de todos los valores pueden no coincidir.|  
||**Sin errores/error**:<br />                      Recuento de filas o valores de la partición cuyo estado de predicción coincide con el estado de destino y cuyo valor de probabilidad de predicción es mayor que 0.|  
|Probabilidad|Las medidas de probabilidad se aplican a varios tipos de modelos.|  
||**Elevación**:<br />                      La proporción entre la probabilidad de predicción real y la probabilidad marginal en los casos de prueba. Se excluyen las filas a las que les falta el valor para el atributo de destino.<br /><br /> Esta medida normalmente muestra la mejora de la probabilidad del resultado de destino cuando se usa el modelo.|  
||**Error cuadrático medio**:<br />                      La raíz cuadrada del error promedio para todos los casos de partición, dividido por el número de casos en la partición, excluidas las filas que tienen valores ausentes para el atributo de destino.<br /><br /> RMSE es un estimador popular para los modelos predictivos. La puntuación calcula el promedio de los valores residuales para cada caso con objeto de producir un único indicador del error del modelo.|  
||**Puntuación del registro**:<br />                      El logaritmo de la probabilidad real de cada caso, sumada y después dividida por el número de filas del conjunto de datos de entrada, excluidas las filas que tienen valores ausentes para el atributo de destino.<br /><br /> Como la probabilidad se representa como una fracción decimal, las puntuaciones del registro son siempre números negativos. Un número más próximo a 0 es una puntuación mejor. Mientras que las puntuaciones sin formato pueden tener distribuciones muy irregulares o sesgadas, un logaritmo es similar a un porcentaje.|  
|Estimación|Medidas que solo se aplican a los modelos de estimación, que predicen un atributo numérico continuo.|  
||**Error cuadrático medio**:<br />                      El error promedio cuando el valor predicho se compara con el valor real.<br /><br /> RMSE es un estimador popular para los modelos predictivos. La puntuación calcula el promedio de los valores residuales para cada caso con objeto de producir un único indicador del error del modelo.|  
||**Desviación media**:<br />                      El error promedio cuando los valores predichos se comparan con los valores reales, calculado como el promedio de la suma absoluta de los errores.<br /><br /> La desviación media es útil para comprender lo cercanas que se encontraban las predicciones globales de los valores reales. Una puntuación menor significa que las predicciones fueron más precisas.|  
||**Log Score**:<br />                      El logaritmo de la probabilidad real de cada caso, sumada y después dividida por el número de filas del conjunto de datos de entrada, excluidas las filas que tienen valores ausentes para el atributo de destino.<br /><br /> Como la probabilidad se representa como una fracción decimal, las puntuaciones del registro son siempre números negativos. Un número más próximo a 0 es una puntuación mejor. Mientras que las puntuaciones sin formato pueden tener distribuciones muy irregulares o sesgadas, un logaritmo es similar a un porcentaje.|  
|Agregados|Las medidas agregadas proporcionan una indicación acerca de la varianza en los resultados para cada partición.|  
||**Promedio**:<br />                      La media de los valores de la partición para una medida determinada.|  
||**Desviación estándar**:<br />                      La media de la desviación desde el promedio para una medida concreta, para todas las particiones de un modelo.<br /><br /> Para la validación cruzada, un valor mayor para esta puntuación implica una variación sustancial entre los subconjuntos.|  
  
## Vea también  
 [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  