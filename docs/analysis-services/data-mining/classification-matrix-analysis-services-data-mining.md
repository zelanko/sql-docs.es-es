---
title: 'Matriz de clasificación (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad46eb4691def73c33b9b5a421de48e36c288b5b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="classification-matrix-analysis-services---data-mining"></a>Matriz de clasificación (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una *matriz de clasificación* ordena todos los casos del modelo en categorías, determinando si el valor de predicción coincide con el valor real. A continuación, se cuentan todos los casos de cada categoría y los totales se muestran en la matriz. La matriz de clasificación es una herramienta estándar de evaluación de modelos estadísticos a la que a veces se denomina *matriz de confusión*.  
  
 El gráfico que se crea cuando se elige la opción **Matriz de clasificación** compara los valores reales con los valores de predicción para cada estado de predicción especificado. Las filas de la matriz representan los valores de predicción para el modelo, mientras que las columnas representan los valores reales. Las categorías usadas en el análisis son *falso positivo*, *verdadero positivo*, *falso negativo*y *verdadero negativo*.  
  
 Una matriz de clasificación es una herramienta importante para evaluar los resultados de la predicción, ya que hace que resulte fácil entender y explicar los efectos de las predicciones erróneas. Al ver la cantidad y los porcentajes en cada celda de la matriz, podrá saber rápidamente en cuántas ocasiones ha sido exacta la predicción del modelo.  
  
 En esta sección se explica cómo se crea una matriz de clasificación y cómo se interpretan los resultados.  
  
## <a name="understanding-the-classification-matrix"></a>Descripción de la matriz de clasificación  
 Considere el modelo que creó como parte del Tutorial básico de minería de datos. El modelo [TM_DecisionTree] se usa para crear una campaña de distribución de correo directo y se puede usar para predecir qué clientes tienen más probabilidad de comprar una bicicleta. Para probar esta utilidad esperada del modelo, se usa un conjunto de datos para el que ya se conocen los valores del atributo de resultados, [Bike Buyer]. Normalmente, se usa el conjunto de datos de prueba que se reservó al crear la estructura de minería de datos que se usa para entrenar el modelo.  
  
 Solo hay dos resultados posibles: sí (es probable que el cliente compre una bicicleta) y no (no es probable que el cliente compre una bicicleta). Por consiguiente, la matriz de clasificación resultante es relativamente sencilla.  
  
## <a name="interpreting-the-results"></a>Interpretación de los resultados  
 En la tabla siguiente se muestra la matriz de clasificación para el modelo TM_DecisionTree. Recuerde que para este atributo de predicción, 0 significa No y 1 significa Sí.  
  
|Previsto|0 (real)|1 (real)|  
|---------------|------------------|------------------|  
|0|362|144|  
|1|121|373|  
  
 La primera celda de resultados, que contiene el valor 362, indica el número de *verdaderos positivos* para el valor 0. Dado que 0 indica que el cliente no compró una bicicleta, esta estadística indica que el modelo predijo el valor correcto para quienes no compraron bicicleta en 362 casos.  
  
 La celda situada directamente debajo de esa, que contiene el valor 121, indica el número de *falsos positivos*, o número de veces que el modelo predijo que alguien compraría una bicicleta cuando en realidad no lo hizo.  
  
 La celda que contiene el valor 144 indica el número de *falsos positivos* para el valor 1. Dado que 1 significa que el cliente compró una bicicleta, esta estadística indica que, en 144 casos, el modelo predijo que alguien no compraría una bicicleta cuando sí lo hizo.  
  
 Finalmente, la celda que contiene el valor 373 indica el número de verdaderos positivos para el valor de destino 1. En otras palabras, en 373 casos el modelo predijo correctamente que alguien compraría una bicicleta.  
  
 Sumando los valores de las celdas contiguas diagonalmente, se puede determinar la exactitud total del modelo. Una diagonal indica el número total de predicciones exactas y la otra indica el número total de predicciones erróneas.  
  
### <a name="using-multiple-predictable-values"></a>Usar varios valores de predicción  
 El caso [Bike Buyer] es especialmente fácil de interpretar porque hay solo dos valores posibles. Cuando el atributo de predicción tiene varios valores posibles, la matriz de clasificación agrega una columna nueva por cada valor real posible y, a continuación, cuenta el número de coincidencias para cada valor predicho. En la tabla siguiente se muestran los resultados en un modelo diferente, donde hay tres valores (0, 1, 2) posibles.  
  
|Previsto|0 (real)|1 (real)|2 (Real)|  
|---------------|------------------|------------------|------------------|  
|0|111|3|5|  
|1|2|123|17|  
|2|19|0|20|  
  
 Aunque la existencia de columnas adicionales hace que el informe parezca más complejo, el detalle adicional puede ser muy útil cuando se desea evaluar el costo acumulativo de realizar una predicción errónea. Para sumar las diagonales o comparar los resultados de combinaciones diferentes de filas, puede hacer clic en el botón **Copiar** que se proporciona en la pestaña **Matriz de clasificación** y pegar el informe en Excel. También puede usar un cliente como el Cliente de minería de datos para Excel, que admite [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, para crear directamente un informe de clasificación en Excel que incluya recuentos y porcentajes. Para obtener más información, vea [Minería de datos de SQL Server](http://go.microsoft.com/fwlink/?LinkID=77733).  
  
## <a name="restrictions-on-the-classification-matrix"></a>Restricciones en la matriz de clasificación  
 Una matriz de clasificación solo se puede usar con atributos de predicción discretos.  
  
 Aunque puede agregar varios modelos mientras selecciona modelos en la pestaña **Selección de entrada** del diseñador **Gráfico de precisión de minería de datos** , la pestaña **Matriz de clasificación** mostrará una matriz independiente para cada modelo.  
  
## <a name="related-content"></a>Contenido relacionado  
 Los temas siguientes contienen más información acerca de cómo puede crear y usar las matrices de clasificación y otros gráficos.  
  
|Temas|Vínculos|  
|------------|-----------|  
|Incluye una visita guiada que explica cómo se crea un gráfico de mejora respecto al modelo predictivo para el modelo de distribución de correo directo.|[Tutorial de minería de datos básicos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)<br /><br /> [Probar la exactitud con gráficos de elevación & #40; Tutorial de minería de datos básicos & #41;](http://msdn.microsoft.com/library/822d414b-4a39-473f-80c3-53476e30655a)|  
|Explica los tipos de gráficos relacionados.|[Gráfico de elevación & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de beneficios & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de dispersión & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Describe los usos de la validación cruzada en los modelos y estructuras de minería de datos.|[La validación cruzada & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Describe los pasos necesarios para crear gráficos de mejora respecto al modelo predictivo y otros gráficos de precisión.|[Pruebas y las tareas de validación y procedimientos & #40; minería de datos & #41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Vea también  
 [Prueba y validación & #40; minería de datos & #41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
