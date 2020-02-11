---
title: Validación cruzada (complementos de minería de datos SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cross-validation
- partitioning data [data mining]
- mining models, testing
ms.assetid: bf9483b3-4099-41c4-bbc5-da7005e07bcd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc3a132792cca8ecdf5a33a2fe4e4d40116c497
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086648"
---
# <a name="cross-validation-sql-server-data-mining-add-ins"></a>Validación cruzada (Complementos de minería de datos de SQL Server)
  ![Botón Validación cruzada, cinta Minería de datos](media/dmc-xvalid.gif "Botón Validación cruzada, cinta Minería de datos")  
  
 La validación cruzada es una herramienta estándar de análisis que resulta muy útil a la hora de desarrollar y ajustar modelos de minería de datos. La validación cruzada se usa después de crear un modelo de minería de datos para determinar la validez del modelo y comparar sus resultados con otros modelos de minería de datos relacionados.  
  
 La validación cruzada consta de dos fases, entrenamiento y generación de informes. Deberá completar los pasos siguientes:  
  
-   Seleccionar una estructura o un modelo de minería de datos de destino.  
  
-   Especificar el valor de destino, si procede.  
  
-   Especifique el número de secciones transversales, o *pliegues*, en las que se van a particionar los datos de la estructura.  
  
 A continuación, el Asistente para **validaciones cruzadas** crea un nuevo modelo en cada uno de los subconjuntos, prueba el modelo en los demás pliegues y, a continuación, informa de la precisión del modelo. Al finalizar, el Asistente para **validación cruzada** crea un informe que muestra las métricas de cada plegamiento y proporciona un resumen del modelo en agregado. Esta información se puede usar para determinar la idoneidad de los datos subyacentes para un determinado modelo, o para comparar modelos distintos generados a partir de los mismos datos.  
  
## <a name="using-the-cross-validation-wizard"></a>Usar el Asistente para validaciones cruzadas  
 Puede usar la validación cruzada tanto en modelos temporales como en modelos almacenados en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
#### <a name="to-create-a-cross-validation-report"></a>Para crear un informe de validación cruzada  
  
1.  En el grupo **precisión y validación** de la cinta de opciones **minería de datos** , haga clic en **validación cruzada**.  
  
2.  En el cuadro de diálogo **seleccionar estructura o modelo** , seleccione una estructura o un modelo de minería de datos existente. Si selecciona una estructura, el asistente usará la validación cruzada en todos los modelos basados en esa estructura que tengan el mismo atributo de predicción. Si selecciona un modelo, el asistente usará la validación cruzada solo en ese modelo.  
  
3.  En el cuadro de diálogo **especificar parámetros de validación cruzada** , en el cuadro **recuento de plegamientos** , elija el número de plegamientos entre los que se va a dividir el conjunto de datos. Un plegamiento es una sección transversal de los datos seleccionada de forma aleatoria.  
  
4.  Opcionalmente, establezca el número máximo de filas que se van a usar en la validación cruzada escribiendo un número en el cuadro de texto **máximo de filas** .  
  
    > [!NOTE]  
    >  Cuántas más filas use, más precisos serán los resultados. Sin embargo, el tiempo de proceso también puede aumentar de forma significativa. El número que elija dependerá de los datos pero, en general, debe elegir el mayor número posible sin sacrificar el rendimiento. Para mejorar el rendimiento, también puede especificar menos plegamientos.  
  
5.  Seleccione una columna en la lista desplegable **atributo de destino** . La lista solo muestra aquellas columnas que se configuraron como atributos de predicción al crear el modelo. El modelo puede contener varios atributos de predicción, pero solo se puede elegir uno.  
  
6.  Seleccione un valor en la lista desplegable **Estado de destino** .  
  
     Si la columna de predicción contiene datos numéricos continuos, esta opción no está disponible.  
  
7.  Opcionalmente, especifique un valor para usarlo como **umbral de destino** en el recuento de predicciones como preciso. Este valor se expresa como una probabilidad, que es un número entre 0 y 1, donde 1 significa que la predicción será correcta sin ninguna duda, 0 significa que no hay ninguna probabilidad de que la predicción sea correcta y 0,5 equivale a una estimación aleatoria.  
  
     Si la columna de predicción contiene datos numéricos continuos, esta opción no está disponible.  
  
8.  Haga clic en **Finalizar** Se crea una nueva hoja de cálculo, denominada **validación cruzada**.  
  
    > [!NOTE]  
    >  Es posible que Microsoft Excel deje de responder temporalmente mientras el modelo se particiona en plegamientos y se prueba cada uno de éstos.  
  
### <a name="requirements"></a>Requisitos  
 Para crear un informe de validación cruzada, ya debe de haber creado una estructura de minería de datos y los modelos relacionados. El asistente incluye un cuadro de diálogo para ayudarle a elegir entre las estructuras y los modelos existentes.  
  
 Si elige una estructura de minería de datos que admite varios modelos de minería de datos, y estos modelos usan atributos de predicción distintos, el Asistente para validaciones cruzadas solo probará aquellos modelos que compartan el mismo atributo de predicción.  
  
 Si elige una estructura que admite tanto modelos de agrupación en clústeres como otros tipos de modelos, los primeros no se probarán.  
  
## <a name="understanding-cross-validation-results"></a>Descripción de los resultados de la validación cruzada  
 Los resultados de la validación cruzada se muestran en una nueva hoja de cálculo, denominada **Informe de validación \<cruzada para el nombre de atributo>**. La nueva hoja de cálculo contiene varias secciones: la primera sección es un resumen que proporciona metadatos importantes sobre el modelo que se probó para que pueda saber a qué modelo o estructura corresponden los resultados.  
  
 La segunda sección del informe proporciona un resumen estadístico que indica el grado de eficacia del modelo original. En este Resumen, se analizan las diferencias entre los modelos creados para cada plegamiento para tres medidas clave: *error cuadrado medio*, error medio *absoluto*y *puntuación del registro*. Éstas son medidas estadísticas estándar que se usan no solo en la minería de datos, sino también en la mayoría de los análisis estadísticos.  
  
 Para cada una de estas medidas, el Asistente para validaciones cruzadas calcula la media y la desviación estándar en todo el modelo. Esto indica la coherencia del modelo al realizar predicciones en distintos subconjuntos de datos. Por ejemplo, si la desviación estándar es muy grande, esto indica que los modelos creados para cada plegamiento tienen resultados muy diferentes y, por lo tanto, es posible que el modelo se haya entrenado para un grupo muy determinado de datos y no se pueda aplicar a otros conjuntos de datos.  
  
 En la sección siguiente se explican las medidas que se usan para evaluar los modelos.  
  
### <a name="tests-and-measures"></a>Pruebas y medidas  
 Además de cierta información básica acerca del número de plegamientos en los datos y de la cantidad de datos en cada plegamiento, la hoja de cálculo muestra un conjunto de métricas sobre cada modelo, clasificadas por tipo de prueba. Por ejemplo, la precisión de un modelo de agrupación en clústeres se evalúa mediante pruebas distintas de las usadas para un modelo de pronóstico.  
  
 La tabla siguiente muestra una lista con las pruebas y las métricas, junto con una explicación del significado de las métricas.  
  
#### <a name="aggregates-and-general-statistical-measures"></a>Agregados y medidas estadísticas generales  
 Las medidas agregadas incluidas en el informe indican cómo difieren entre sí los plegamientos creados en los datos.  
  
-   Media y desviación estándar.  
  
-   La media de la desviación desde el promedio para una medida concreta, para todas las particiones de un modelo.  
  
#### <a name="classification-passfail"></a>Clasificación: Pass/Fail  
 Esta medida se usa en modelos de clasificación cuando no se especifica un valor de destino para el atributo de predicción. Por ejemplo, si crea un modelo que predice varias posibilidades, esta medida le indica el grado de eficiencia del modelo a la hora de predecir todos los valores posibles.  
  
 Pass/Fail se calcula contando los casos que cumplen las condiciones siguientes: **Pass** si el estado de predicción con la probabilidad más alta es el mismo que el estado de entrada y la probabilidad es mayor que el valor especificado para el **umbral de estado**; de lo contrario, **producirá un error**.  
  
#### <a name="classification-true-or-false-positives-and-negatives"></a>Clasificación: verdaderos o falsos positivos y negativos  
 Esta prueba se usa para todos los modelos de clasificación que tienen un destino especificado. Esta medida indica cómo se clasifica cada caso en respuesta a estas preguntas: qué predijo el modelo y cuál fue el resultado real.  
  
|Measure|Descripción|  
|-------------|-----------------|  
|Verdadero positivo|Recuento de casos que cumplen estas condiciones:<br /><br /> El caso contiene el valor de destino.<br /><br /> El modelo predijo que ese caso contendría el valor de destino.|  
|Falso positivo|Recuento de casos que cumplen estas condiciones:<br /><br /> El valor real es igual al valor de destino.<br /><br /> El modelo predijo que ese caso contendría el valor de destino.|  
|Verdadero negativo|Recuento de casos que cumplen estas condiciones:<br /><br /> El caso no contiene el valor de destino.<br /><br /> El modelo predijo que el caso no contendría el valor de destino.|  
|Falso negativo|Recuento de casos que cumplen estas condiciones:<br /><br /> El valor real no es igual al valor de destino.<br /><br /> El modelo predijo que el caso no contendría el valor de destino.|  
  
#### <a name="lift"></a>Mejora respecto al modelo predictivo  
 La *elevación* es una medida que está asociada a la probabilidad. Si un resultado es más probable cuando se usa el modelo que cuando se realiza una estimación aleatoria, se dice que el modelo proporciona una *elevación positiva*. Sin embargo, si el modelo realiza predicciones que son menos probables que la posibilidad aleatoria, la puntuación de elevación es *negativa*. Por consiguiente, esta métrica indica la cantidad de mejoras que se pueden lograr usando el modelo, donde una puntuación más alta es mejor.  
  
 La mejora respecto al modelo predictivo se calcula como la proporción entre la probabilidad de predicción real y la probabilidad marginal en los casos de prueba.  
  
#### <a name="log-score"></a>Logaritmo  
 La *puntuación del registro*, también denominada *puntuación de probabilidad de registro* para la predicción, representa la relación entre dos probabilidades, convertida en una escala logarítmica. Como las probabilidades se representan como una fracción decimal, el logaritmo es siempre un número negativo. Una puntuación más cercana a 0 es una puntuación mejor.  
  
 Mientras que las puntuaciones sin formato pueden tener distribuciones muy irregulares o sesgadas, un logaritmo es similar a un porcentaje.  
  
#### <a name="root-mean-square-error"></a>Error cuadrático medio  
 *Error medio cuadrado raíz* (RMSE) es un método estándar en las estadísticas para ver cómo se comparan los diferentes conjuntos de datos y suavizar las diferencias que se pueden introducir en la escala de las entradas.  
  
 RMSE representa el error promedio del valor de predicción al compararlo con el valor real. Se calcula como la raíz cuadrada del error promedio para todos los casos de partición, dividido por el número de casos en la partición, excluidas las filas que tienen valores ausentes para los atributos de destino.  
  
#### <a name="mean-absolute-error"></a>Error medio absoluto  
 El *error absoluto* medio es el promedio de error del valor de predicción para el valor real. Se calcula obteniendo la suma absoluta de los errores y buscando la media de esos errores.  
  
 Este valor le ayuda a entender en qué medida varían las puntuaciones con relación a la media.  
  
#### <a name="case-likelihood"></a>Probabilidad de casos  
 Esta medida solo se usa en modelos de agrupación en clústeres, e indica la probabilidad de que un nuevo caso pertenezca a un clúster determinado.  
  
 En los modelos de agrupación en clústeres hay dos tipos de pertenencia al clúster, dependiendo del método usado para crear el modelo. En algunos modelos, basados en el algoritmo mediana-K, se espera que un nuevo caso pertenezca únicamente a un clúster. Sin embargo, de forma predeterminada el algoritmo de clústeres de Microsoft usa el método de agrupación en clústeres EM (Maximization Expectation), que presupone que un nuevo caso puede pertenecer potencialmente a cualquier clúster. Por lo tanto, en estos modelos un caso puede tener varios valores de `CaseLikelihood`, pero el establecido de forma predeterminada es la probabilidad de que el caso pertenezca al clúster más adecuado para el nuevo caso.  
  
## <a name="see-also"></a>Consulte también  
 [Validar modelos y usar modelos para la predicción &#40;complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
