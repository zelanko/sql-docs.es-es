---
title: Cálculo de predicción (herramientas de análisis de tabla para Excel) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining model, regression
- Table Analysis tools
- scorecard
- logistic regression
- prediction calculator
ms.assetid: 8bb8c318-e85f-4fd6-b32b-4cdfb13ca1b5
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ac962304d0870c3f0882a02a0a97eb3f266aaa9a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113693"
---
# <a name="prediction-calculator-table-analysis-tools-for-excel"></a>Cálculo de predicción (Herramientas de análisis de tabla para Excel)
  ![Herramienta de cálculo de predicción](media/tat-predcal.gif "herramienta cálculo de predicción")  
  
 El **cálculo de predicción** herramienta le ayuda a crear un cuadro de mandos que puede utilizarse para analizar los nuevos datos y evaluar las opciones o riesgo. Por ejemplo, si tiene datos históricos y demográficos sobre los clientes, el **cálculo de predicción** herramienta puede ayudarle con dos tareas fundamentales:  
  
-   Generar un análisis subyacente de los datos demográficos, los hábitos de compra y otros factores.  
  
-   Crear una tarjeta de puntuación operativa que le permita evaluar a los miembros y proponer recomendaciones para nuevos productos u ofertas de servicios.  
  
 El asistente también crea una hoja de cálculo que almacena todos los cálculos subyacentes para que pueda interactuar con el modelo y comprobar cómo afectan a la puntuación final los distintos valores de entrada.  
  
 Si lo desea, el asistente también puede crear una versión impresa de la hoja de cálculo que podrá usar para la puntuación sin conexión. No puede interactuar con el modelo de la misma forma que con el libro de Excel en línea, pero la versión impresa proporciona todos los cálculos necesarios para introducir valores y calcular una puntuación final.  
  
## <a name="using-the-prediction-calculator-tool"></a>Usar la herramienta Cálculo de predicción  
  
1.  Abra la tabla de Excel que contiene los datos que desea analizar.  
  
2.  Haga clic en **cálculo de predicción** en el **analizar** ficha.  
  
3.  En el **cálculo de predicción** cuadro de diálogo, como el destino, elija la columna que desea predecir, como hábitos de compra.  
  
4.  Especifique el valor deseado. Si el valor es numérico, utilice la opción **en intervalo**y, a continuación, escriba los valores mínimos y máximo para el intervalo deseado. Si el valor es discreto, seleccione la **exactamente** opción y, a continuación, seleccione el valor en la lista desplegable.  
  
5.  Haga clic en **elegir las columnas que se usarán para el análisis**.  
  
6.  En el **selección avanzada de columnas** cuadro de diálogo, seleccione las columnas que contengan información útil. Quite las columnas que no sean relevantes para el análisis. Haga clic en **Aceptar**.  
  
     Para evitar sesgar los resultados, también conviene que quite las columnas con información duplicada. Por ejemplo, si tiene una columna de ingresos que contiene datos numéricos, y una columna de grupo de ingresos que contiene las etiquetas Alto, Medio y Bajo, no debe incluir ambas columnas en el mismo modelo. En su lugar, puede crear un modelo independiente para cada columna.  
  
7.  En el **opciones de salida** sección, seleccione **cálculos operativos** para crear el análisis y la tarjeta de puntuación en un libro de Excel. Seleccione **cálculos listos para impresión** para crear el análisis y generar un informe que puede imprimir y usar para puntuar manualmente.  
  
8.  Haga clic en **Ejecutar**.  
  
     La herramienta crea nuevas hojas de cálculo que contienen los informes y las tarjetas de puntuación.  
  
### <a name="requirements"></a>Requisitos  
 El **cálculo de predicción** herramienta utiliza el algoritmo de regresión logística de Microsoft, que puede trabajar con valores discretos, así como datos numéricos discretos y continuos.  
  
## <a name="understanding-the-scoring-reports"></a>Descripción de los informes de puntuación  
 Si selecciona ambas opciones de salida, la herramienta Cálculo de predicción crea las tres hojas de cálculo nuevas siguientes dentro del libro actual:  
  
-   A **informe de predicción**que contiene los resultados del análisis, junto con tablas interactivas y gráficos que le permiten experimentar con interacciones y beneficios.  
  
-   Interactivo **cálculo de predicción** que le ayuda a crear puntuaciones.  
  
-   A **cálculo imprimible** con instrucciones y coeficientes que usar para determinar la puntuación.  
  
-   En esta sección se describe la información incluida en cada informe y cómo usar las distintas opciones de informe.  
  
### <a name="prediction-report-with-graphs"></a>Informe de predicción con gráficos  
 El primer informe de predicción se denomina **informe del cálculo de predicción para el \<estado de destino > de \<atributo de destino >**. Contiene una tabla de factores derivados del análisis, junto con herramientas que le permiten evaluar el impacto financiero de un análisis determinado.  
  
#### <a name="table-for-specifying-costs-and-profits"></a>Tabla para especificar costos y beneficios  
 La primera herramienta de este informe, situada en el lado superior izquierdo del informe, es una tabla donde puede especificar los costos y beneficios asociados al predecir correcta o incorrectamente un valor.  Estos costos y beneficios son necesarios para calcular el umbral de puntuación óptimo del cálculo de predicción.  
  
|Elemento|Descripción y ejemplo|  
|----------|-----------------------------|  
|Costo de falso positivo|El costo de asumir que el modelo predijo un resultado positivo correctamente cuando realmente la predicción está equivocada.<br /><br /> Por ejemplo, el modelo predice que un cliente comprará algo, y basándose en ello crea una campaña dirigida a ese cliente. Aquí podría escribir el costo de darse a conocer al cliente.|  
|Costo de falso negativo|El costo de asumir que el modelo predijo un resultado negativo correctamente cuando realmente la predicción está equivocada.<br /><br /> Por ejemplo, el modelo podría predecir que es improbable que los clientes de mayor edad compren una bicicleta, pero descubre que el modelo estaba sesgado y que, en consecuencia, ha perdido una oportunidad para dirigirse a dichos clientes. Aquí podría asignar un costo de oportunidad perdida.|  
|Beneficio de verdadero positivo|El beneficio de predecir correctamente un resultado positivo. Por ejemplo, si el objetivo son los clientes adecuados y los resultados de una venta, aquí escribiría el beneficio por cliente.|  
|Beneficio de verdadero negativo|El beneficio de predecir correctamente un resultado negativo.<br /><br /> Por ejemplo, si puede identificar correctamente los clientes a los que no debe dirigirse, aquí podría escribir la cantidad de dólares de publicidad por cliente.|  
  
#### <a name="chart-for-viewing-maximum-profit"></a>Gráfico para ver el beneficio máximo  
 A medida que escribe los valores en la tabla, los gráficos relacionados se actualizan automáticamente para mostrarle el mejor punto para maximizar el beneficio en el modelo actual. El gráfico de líneas situado a la derecha de esta tabla muestra el beneficio para varios umbrales de puntuación. El beneficio se calcula usando las cifras de beneficio y de costo que ha introducido en la tabla, basándose en las predicciones y probabilidades del modelo.  
  
 Por ejemplo, si es, en la tabla superior izquierda, la celda de **umbral sugerido para maximizar el beneficio** muestra el valor 500, el gráfico en el lado derecho mostrará 500 como el punto más alto del gráfico de líneas. Lo que este valor significa es que, para maximizar los beneficios, debe usar las 500 recomendaciones superiores del modelo de minería de datos, ordenadas por probabilidad.  
  
#### <a name="table-listing-scores-for-each-attribute-and-value"></a>Tabla que incluye las puntuaciones para cada atributo y valor  
 La tabla situada en el lado inferior izquierdo del informe muestra un análisis detallado de los valores que se detectaron, y cómo afecta cada uno de ellos al resultado. No se pueden cambiar los valores de esta tabla; aparecen aquí para ayudarle a comprender la predicción.  
  
 Por ejemplo, la tabla siguiente muestra un ejemplo de los resultados cuando el resultado de destino es que un cliente compra una bicicleta. La tabla incluye cada una de las columnas de entrada usadas en el modelo, independientemente de si la entrada afectó a éste. La tabla también contiene los valores discretos y los valores discretizados si la columna de entrada incluía datos numéricos continuos.  
  
 Los valores de la **impacto relativo** columna son probabilidades, representadas como porcentajes. La celda aparece sombreada para representar visualmente el impacto de este valor en los resultados.  
  
|Attribute|Valor|Impacto relativo|  
|---------------|-----------|---------------------|  
|Marital Status|Married|0|  
|Marital Status|Único|71|  
|Sexo|Female|13|  
|Sexo|Male|0|  
  
 Puede interpretar estos factores de la siguiente manera:  
  
-   El estar casado no afecta a la posibilidad de que el cliente compre una bicicleta.  
  
-   Sin embargo, estar soltero es un claro indicador (70 por ciento) de que el cliente probablemente compre una bicicleta.  
  
-   El género del cliente sólo tiene un efecto marginal (13 por ciento) en el comportamiento de compras de bicicletas predicho si el cliente es una mujer, y no tiene ningún efecto en dicho comportamiento si el cliente es un hombre.  
  
#### <a name="chart-of-cumulative-misclassification-cost"></a>Gráfico de costo de clasificaciones incorrectas acumulativas  
 El gráfico de áreas situado en lado inferior derecho del informe muestra el costo de clasificaciones incorrectas acumulativas para varios umbrales de puntuación. Este gráfico también usa las cifras de costo y beneficio especificadas para los falsos positivos, los verdaderos positivos, los falsos negativos y los falsos positivos.  
  
 A diferencia del gráfico situado en el lado superior derecho del informe, que se centra en maximizar el beneficio, este gráfico incorpora el costo de realizar la predicción equivocada. Este gráfico es especialmente útil en escenarios como la prevención, donde el costo de tomar la decisión equivocada supera ampliamente al costo de realizar la predicción correcta.  
  
 Por ejemplo, aunque el primer gráfico sugiere que dirigirse a los 500 clientes superiores predichos por el modelo es la manera de conseguir el máximo beneficio, después de examinar este segundo gráfico podría decidir que los costos de dirigirse a los clientes equivocados son demasiado grandes, y optar por reducir la campaña de marketing a los primeros 400 clientes.  
  
### <a name="interactive-prediction-calculator"></a>Cálculo de predicción interactivo  
 La segunda hoja de cálculo creada por la herramienta de cálculo de predicción se denomina **cálculo de predicción para el \<estado de destino > de \<atributo de destino >**. Es una hoja de cálculo interactiva que puede usar para calcular puntuaciones individuales. Dado que esta hoja de cálculo utiliza los patrones y las estadísticas almacenadas en el modelo, puede experimentar con valores diferentes y ver cómo afectan a la puntuación predicha. Este informe también incluye dos secciones: una es interactiva y la otra se proporciona como referencia.  
  
#### <a name="first-table"></a>Primera tabla  
 Puede seleccionar o escribir un nuevo valor en el **valor** columna de la tabla para ver cómo afecta el cambio del valor a la puntuación.  
  
 Por ejemplo, si el informe contiene los valores siguientes, podría disminuir el valor de Cars a 1 y, a continuación, a 0 para comprobar cómo afecta esto a los hábitos de compra de los clientes. A medida que cambia el valor de **automóviles** en 0, la predicción en la parte inferior cambia a TRUE.  
  
|Attribute|Valor|Impacto relativo|  
|---------------|-----------|---------------------|  
|Marital Status|Married|0|  
|Sexo|Male|0|  
|Income|39050 - 71062|117|  
|Children|0|157|  
|Education|Bachelors|22|  
|Occupation|Skilled Manual|33|  
|Home Owner|Sí|8|  
|Cars|2|50|  
|Commute Distance|0-1 Miles|99|  
|Region|North America|0|  
|Age|37 - 46|5|  
|Total||491|  
|Prediction for 'Yes'||FALSE|  
  
 Cuando se escribe en el nuevo valor, la puntuación mostrada en la celda Prediction for Yes cambia a TRUE y el **impacto relativo** puntuaciones para los distintos atributos también se actualizan.  
  
> [!NOTE]  
>  Incluso si modifica un solo valor, como el número de coches, es posible que los valores e impactos de otros atributos cambien también al hacerlo. Esto es debido a que los modelos de minería de datos suelen encontrar relaciones complejas entre los datos, y la modificación de una variable puede tener efectos imprevistos. Por esta razón, recomendamos que use el cálculo de predicción interactivo para experimentar con distintos valores, o que examine el modelo de minería de datos para entender mejor las interacciones. Para obtener más información, consulte [examinar modelos](prediction-calculator-table-analysis-tools-for-excel.md).  
  
#### <a name="score-breakdown"></a>Desglose de puntuación  
 En esta tabla se muestran las puntuaciones individuales para cada posible estado de las columnas de entrada, así como el impacto relativo que dichas puntuaciones tienen en los resultados. Esta tabla es estática y solo se usa como referencia.  
  
### <a name="printable-prediction-calculator"></a>Cálculo de predicción imprimible  
 La tercera hoja de cálculo creada por la herramienta de cálculo de predicción se denomina **PrintablePrediction calculadora para la \<estado de destino > de \<atributo de destino >**. Esta tarjeta de puntuación está concebida para su impresión, de tal forma que pueda calcular manualmente las puntuaciones cuando no esté cerca de su equipo.  
  
##### <a name="to-print-and-use-the-scoring-report-generated-by-the-prediction-calculator"></a>Para imprimir y usar el informe de puntuación generado por la herramienta Cálculo de predicción  
  
1.  Haga clic en la pestaña que se denomina **imprimible para \<atributo >**.  
  
2.  En el menú archivo de Excel, seleccione **vista previa de impresión**.  
  
3.  Cambie la orientación de la página, los márgenes y otras opciones de impresión hasta que la tarjeta de puntuación quepa en la página de la forma deseada.  
  
     Esta tarjeta de puntuación no es dinámica y no está conectada al modelo en forma alguna, por lo que puede mover columnas o filas para mejorar el formato sin afectar a los datos subyacentes.  
  
4.  Imprima la tarjeta de puntuación.  
  
5.  Elija un único valor para cada atributo. Para el valor elija, coloque una marca de verificación en el cuadro y escriba el número correspondiente el **puntuación** columna.  
  
6.  Rellene tantos atributos como sea posible para garantizar la precisión.  
  
7.  Calcular la suma de las puntuaciones para cada atributo y escriba ese número en el **Total** fila.  
  
8.  Convierta la puntuación en un resultado de predicción mediante los criterios que se imprimen en la hoja inmediatamente después de la **Total** fila.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona el algoritmo de regresión logística de Microsoft para su uso en este tipo de análisis. Si ya está familiarizado con la regresión logística, puede crear fácilmente los modelos de regresión logística usando la **avanzadas** opción del cliente de minería de datos para Excel. Para obtener más información, consulte [avanzadas de modelado &#40;complementos minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md). Para obtener más información acerca de las opciones y parámetros para los modelos de regresión logística, vea el tema "Algoritmo de regresión logística de Microsoft" en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)  
  
  