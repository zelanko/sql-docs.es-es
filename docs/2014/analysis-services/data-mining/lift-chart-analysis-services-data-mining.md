---
title: Gráfico de elevación (Analysis Services-minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing data mining models
- accuracy, charting
- viewing mining accuracy
- lift charts [Analysis Services]
- profit charts [Analysis Services]
- accuracy testing [data mining]
ms.assetid: ab77eca1-bd48-4fef-b27f-ff5b648e0501
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: feba3688947362847a95aea2d800c1fc6f15f6cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174685"
---
# <a name="lift-chart-analysis-services---data-mining"></a>Gráfico de mejora respecto al modelo predictivo (Analysis Services - Minería de datos)
  Un **gráfico de elevación** representa gráficamente la mejora que proporciona un modelo de minería de datos en comparación con una estimación aleatoria y mide el cambio en términos de una puntuación de *elevación* . Al comparar las puntuaciones de mejora de las distintas partes del conjunto de datos y para los distintos modelos, puede determinar qué modelo es mejor y qué porcentaje de los casos del conjunto de datos se beneficiaría de aplicar las predicciones del modelo.

 Con un gráfico de mejora respecto al modelo predictivo, puede comparar la precisión de las predicciones para varios modelos que tienen el mismo atributo de predicción. También puede evaluar la exactitud de la predicción para un único resultado (un único valor del atributo de predicción) o para todos los resultados (todos los valores del atributo especificado).

 Un gráfico de beneficios es un tipo de gráfico relacionado que contiene la misma información que un gráfico de mejora respecto al modelo predictivo, pero que también muestra el aumento proyectado en los beneficios asociado al uso de cada modelo.

##  <a name="understanding-the-lift-chart"></a><a name="bkmk_Top"></a>Descripción del gráfico de elevación
 Puede resultar difícil entender los gráficos de mejora respecto al modelo predictivo como concepto abstracto. Por consiguiente, para ilustrar el uso de las herramientas del gráfico de mejora respecto al modelo predictivo y la información del gráfico, en esta sección se muestra un escenario en el que se usa un gráfico de mejora respecto al modelo predictivo para calcular la respuesta a una campaña de envío de correo directo.

 El departamento de marketing de este escenario sabe que las campañas de correo suelen tener más o menos una tasa de respuesta del 10 por ciento. Tienen una lista de 10.000 clientes potenciales almacenada en una tabla de la base de datos. Según el índice típico de respuesta, normalmente pueden esperar que solo respondan unos 1.000 clientes potenciales. Sin embargo, el dinero presupuestado para el proyecto no es suficiente para llegar a los 10.000 clientes de la base de datos, y desean mejorar la tasa de respuesta. Para este escenario, supongamos que el presupuesto solo les permite enviar un anuncio a 5.000 clientes. El departamento de marketing tiene dos opciones:

-   Seleccionar aleatoriamente 5.000 clientes como objetivo.

-   Usar un modelo de minería de datos para dirigirse a los 5.000 clientes con mayores probabilidades de respuesta.

 Mediante un gráfico de mejora respecto al modelo predictivo, puede comparar los resultados esperados de ambas opciones. Por ejemplo, si la compañía seleccionara de forma aleatoria 5.000 clientes, podrían esperar recibir solo 500 respuestas, según la tasa de respuesta típica. Este escenario es lo que representa la línea *aleatoria* del gráfico de elevación. Sin embargo, si el departamento de marketing usara un modelo de minería de datos para dirigir la distribución de correo, podría esperar un mejor índice de respuesta debido a que el modelo identificaría los clientes que tienen más probabilidades de responder. Si el modelo fuera perfecto, crearía predicciones infalibles y la empresa podría esperar recibir 1.000 respuestas con solo enviar la distribución de correo a los 1.000 clientes potenciales recomendados por el modelo. La línea *ideal* del gráfico de mejora respecto al modelo predictivo representa esta situación.

 La realidad es que el modelo de minería de datos probablemente se sitúa entre estos dos extremos, entre una estimación aleatoria y una predicción perfecta. Cualquier mejora con respecto a la estimación aleatoria se considera una "mejora respecto al modelo predictivo".

 Al crear un gráfico de mejora respecto al modelo predictivo, puede ponerse como objetivo un valor específico y medir la mejora respecto al modelo predictivo solo para ese resultado o puede crear una evaluación general del modelo que mida las mejoras respecto al modelo predictivo para todos los resultados posibles. Estas selecciones afectan al gráfico final, como se describe en las secciones siguientes.

 [Volver al principio](#bkmk_Top)

### <a name="lift-chart-with-target-value"></a>Gráfico de mejora respecto al modelo predictivo con un valor de destino
 El gráfico siguiente muestra un gráfico de mejora respecto al modelo predictivo para el modelo **Targeted Mailing** que se crea en el [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md). En este gráfico, el atributo de destino es [Bike Buyer] y el valor de destino es 1, lo que significa que se prevé que el cliente compre una bicicleta. El gráfico de mejora respecto al modelo predictivo muestra así la mejora proporcionada por el modelo al identificar a estos posibles clientes.

 Este gráfico contiene varios modelos basados en los mismos datos. Uno de ellos se ha personalizado para dirigirse a clientes concretos. Puede personalizar un modelo agregando filtros para los datos usados para entrenarlo. Este filtro restringe los casos que se usan tanto en el entrenamiento como en la evaluación a los clientes menores de 30 años. Observe que un efecto del filtrado es que el modelo básico y el modelo filtrado usan conjuntos de datos distintos, por lo que el número de casos usados para la evaluación en el gráfico de mejora respecto al modelo predictivo también es diferente. Es importante recordar este punto al interpretar los resultados de predicción y otras estadísticas.

 ![gráfico de elevación en el que se muestran dos modelos](../media/newliftchart-tm30-30.gif "gráfico de elevación en el que se muestran dos modelos")

 El eje X del gráfico representa el porcentaje del conjunto de datos de prueba que se usa para comparar las predicciones. El eje Y del gráfico representa el porcentaje de valores de predicción.

 La línea recta diagonal, mostrada aquí en azul, aparece en cada gráfico. Representa los resultados de la estimación aleatoria y es la línea base con la que evaluar la mejora respecto al modelo predictivo. Con cada modelo que agrega a un gráfico de mejora respecto al modelo predictivo, obtiene dos líneas adicionales: una muestra los resultados ideales para los conjuntos de datos de entrenamiento establecidos, si pudiera crear un modelo que siempre predijera perfectamente; y la segunda línea muestra la mejora respecto al modelo predictivo real, o mejora en los resultados, para el modelo.

 En este ejemplo, la línea ideal para el modelo filtrado se muestra en azul marino y la línea para la mejora respecto al modelo predictivo real en amarillo. Puede deducir del gráfico que la línea ideal alcanza el máximo cerca del 40 por ciento, lo que significa que si tuviera un modelo perfecto, podría llegar al 100 por ciento de los clientes de destino enviando correo únicamente al 40 por ciento de la población total. La mejora respecto al modelo predictivo real para el modelo filtrado al destinarse al 40 por ciento de la población está entre el 60 y el 70 por ciento, lo que significa que se podría llegar al 60 ó 70 por ciento de los clientes de destino enviando correo al 40 por ciento de la población total de clientes.

 La **Leyenda de minería de datos** contiene los valores reales de cualquier punto de las curvas. Puede cambiar el lugar que se mide haciendo clic en la barra gris vertical y moviéndola. En el gráfico, la línea gris se ha movido al 30 por ciento, porque se trata del punto donde tanto el modelo filtrado como el modelo sin filtrar parecen ser más eficientes, y después de este punto la cantidad de mejora respecto al modelo predictivo decae.

 La **Leyenda de minería de datos** también contiene puntuaciones y estadísticas que ayudan a interpretar el gráfico. Estos resultados representan la exactitud del modelo en la línea gris, que en este escenario está situada para que incluya el 30 por ciento de los casos de prueba totales.

|Serie y modelo|Puntuación|Población de destino|Probabilidad de predicción|
|-----------------------|-----------|-----------------------|-------------------------|
|Correo destinado a todos|0.71|47,40 %|61,38 %|
|Correo destinado a menores de 30|0.85|51,81 %|46.62 %|
|Modelo de estimación aleatoria||31.00 %||
|Modelo ideal para: correo destinado a todos||62.48 %||
|Modelo ideal para: correo destinado a menores de 30||65.28 %||

 [Volver al principio](#bkmk_Top)

#### <a name="interpreting-the-results"></a>Interpretación de los resultados
 En estos resultados puede ver que, cuando se mide en el 30 por ciento de todos los casos, el modelo general, [Correo destinado a todos], puede predecir el comportamiento de compra de bicicletas en el 47,40% de la población de destino. En otras palabras, si enviara correo directo solo al 30 por ciento de los clientes de la base de datos, podría llegar a algo menos de la mitad de los destinatarios pretendidos. Si usara el modelo filtrado, podría obtener resultados ligeramente mejores y llegar aproximadamente al 51 por ciento de los clientes de destino.

 El valor de **Probabilidad de predicción** representa el umbral necesario para incluir un cliente entre los casos "con probabilidad de comprar". Para cada caso, el modelo calcula la exactitud de cada predicción y almacena ese valor, que puede utilizar para filtrar o elegir clientes. Por ejemplo, para identificar los clientes del modelo básico que son compradores probables, utilizaría una consulta para recuperar los casos con una probabilidad de predicción de al menos el 61 por ciento. Para obtener los clientes de destino del modelo filtrado, crearía una consulta que recuperara los casos que cumplieran todos los criterios: la edad y un valor de `PredictProbability` de al menos el 46 por ciento.

 Es interesante comparar los modelos. El modelo filtrado parece capturar más clientes potenciales, pero al elegir a los clientes con una puntuación de probabilidad de predicción del 46 por ciento, también tiene una posibilidad del 53 por ciento de enviar correo a alguien que no va a comprar una bicicleta. Por consiguiente, si estuviera decidiendo qué modelo es mejor, sería conveniente equilibrar la mayor precisión y el menor tamaño de destino del modelo filtrado con respecto a la capacidad de selección del modelo básico.

 El valor de **Puntuación** ayuda a comparar los modelos calculando la efectividad del modelo a través de una población normalizada. Una mayor puntuación es mejor, de modo que en este caso podría decidir que seleccionar a los clientes menores de 30 años es la estrategia más eficiente, a pesar de la menor probabilidad de predicción.

 [Volver al principio](#bkmk_Top)

### <a name="lift-chart-for-model-with-no-target-value"></a>Gráfico de mejora respecto al modelo predictivo para un modelo sin valor de destino
 Si no especifica el estado de la columna de predicción, puede crear el tipo de gráfico que se muestra en el diagrama siguiente. Este gráfico muestra el modo en que el modelo se comporta para todos los estados del atributo de predicción. Por ejemplo, este gráfico le indicaría hasta qué punto el modelo predice bien tanto los clientes que es probable que compren una bicicleta como los que no es probable que la compren.

 El eje X es el mismo que en el gráfico con la columna de predicción especificada, pero ahora el eje Y representa el porcentaje de predicciones correctas. Por consiguiente, la línea ideal es la línea diagonal, que muestra que en el 50 por ciento de los datos, el modelo predice correctamente el 50 por ciento de los casos, el máximo que se puede esperar.

 ![Gráfico de elevación en el que se muestran predicciones correctas](../media/lift1.gif "Gráfico de elevación en el que se muestran predicciones correctas")

 Puede hacer clic en el gráfico para mover la barra gris vertical y la **Leyenda de minería de datos** muestra el porcentaje de casos total y el porcentaje de casos que se predijeron correctamente. Por ejemplo, si coloca la barra deslizante gris en la marca del 50 por ciento, la **Leyenda de minería de datos** muestra las puntuaciones de precisión siguientes. Estas cifras se basan en el modelo TM_Decision Tree creado en el Tutorial básico de minería de datos.

|Serie, Modelo|Puntuación|Población de destino|Probabilidad de predicción|
|-------------------|-----------|-----------------------|-------------------------|
|TM_Decision Tree|0.77|40.50 %|72.91 %|
|Modelo ideal||50.00%||

 En esta tabla se indica que, en el 50 por ciento de la población, el modelo que creó predice correctamente el 40 por ciento de los casos. Podría considerar este un modelo bastante preciso. Sin embargo, recuerde que este modelo determinado predice todos los valores del atributo de predicción. Por consiguiente, el modelo podría ser preciso para predecir que el 90 por ciento de los clientes no comprarán una bicicleta.

 [Volver al principio](#bkmk_Top)

### <a name="restrictions-on-lift-charts"></a>Restricciones de los gráficos de mejora respecto al modelo predictivo
 Los gráficos de mejora respecto al modelo predictivo requieren que el atributo de predicción sea un valor discreto. Es decir, no puede usar gráficos de mejora respecto al modelo predictivo para medir la exactitud de los modelos que predicen valores numéricos continuos.

 La exactitud de la predicción para todos los valores discretos del atributo de predicción se muestra en una única línea. Si desea ver las líneas de exactitud de la predicción para cualquier valor individual del atributo de predicción, debe crear un gráfico de mejora respecto al modelo predictivo independiente para cada valor de destino.

 Puede agregar varios modelos a un gráfico de mejora respecto al modelo predictivo, siempre que todos los modelos tengan el mismo atributo de predicción. Los modelos que no compartan el atributo no estarán disponibles para la selección en la pestaña **Entrada** .

 No puede mostrar modelos de serie temporal en un gráfico de mejora respecto al modelo predictivo ni en un gráfico de beneficios. Una práctica común para medir la precisión de las predicciones de series temporales consiste en reservar una parte de los datos históricos y comparar estos datos con las predicciones. Para más información, consulte [Microsoft Time Series Algorithm](microsoft-time-series-algorithm.md).

### <a name="related-content"></a>Contenido relacionado
 [Volver al principio](#bkmk_Top)

## <a name="see-also"></a>Consulte también
 [Prueba y validación &#40;minería de datos&#41;](testing-and-validation-data-mining.md)


