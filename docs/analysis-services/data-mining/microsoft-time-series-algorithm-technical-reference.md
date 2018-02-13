---
title: "Referencia técnica del algoritmo de serie temporal de Microsoft | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ARTXP
- HISTORICAL_MODEL_GAP parameter
- AUTO_DETECT_PERIODICITY parameter
- time series algorithms [Analysis Services]
- ARIMA
- INSTABILITY_SENSITIVITY parameter
- PERIODICITY_HINT parameter
- MAXIMUM_SERIES_VALUE parameter
- time series [Analysis Services]
- MINIMUM_SUPPORT parameter
- HISTORIC_MODEL_COUNT parameter
- FORECAST_METHOD parameter
- MISSING_VALUE_SUBSTITUTION parameter
- MINIMUM_SERIES_VALUE parameter
- COMPLEXITY_PENALTY parameter
- PREDICTION_SMOOTHING parameter
ms.assetid: 7ab203fa-b044-47e8-b485-c8e59c091271
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 40d0c34ea4bb7e95d77ff6aa37695da4080c20ac
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Referencia técnica del algoritmo de serie temporal de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
El algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluye dos algoritmos independientes para analizar series de tiempo:  
  
-   El algoritmo ARTXP, que se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se ha optimizado para predecir el siguiente valor probable de una serie.  
  
-   El algoritmo ARIMA se ha agregado en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para mejorar la exactitud de la predicción a largo plazo.  
  
 De forma predeterminada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza cada algoritmo por separado para entrenar el modelo y, a continuación, combina los resultados para obtener la mejor predicción de un número variable de predicciones. También puede decidir utilizar solo uno de los algoritmos, dependiendo de los datos y los requisitos de la predicción. En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], también puede personalizar el punto límite que controla la combinación de algoritmos durante la predicción.  
  
 En este tema se proporciona información adicional sobre cómo se implementa cada algoritmo y cómo se puede personalizar el algoritmo estableciendo los parámetros para ajustar el análisis y los resultados de la predicción.  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Implementación del algoritmo de serie temporal de Microsoft  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research desarrolló el algoritmo ARTXP original que se usaba en SQL Server 2005 y basó la implementación en el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Por consiguiente, el algoritmo ARTXP se puede describir como un modelo de árbol con regresión automática que permite representar datos de series temporales periódicas. Este algoritmo relaciona un número variable de elementos pasados con cada elemento actual que se predice. El nombre, ARTXP, deriva del hecho de que el método de árbol de regresión automática (un algoritmo ART) se aplica a varios estados anteriores desconocidos. Para obtener una explicación detallada del algoritmo ARTXP, vea [Autoregressive Tree Models for Time-Series Analysis](http://go.microsoft.com/fwlink/?LinkId=45966)(Modelos de árbol de regresión automática para el análisis de series temporales).  
  
 El algoritmo ARIMA se ha agregado al algoritmo de serie temporal de Microsoft en SQL Server 2008 para mejorar la exactitud de la predicción a largo plazo. Se trata de una implementación del proceso para calcular medias móviles integradas autorregresivas descrito por Box y Jenkins. La metodología ARIMA permite determinar las dependencias en las observaciones tomadas secuencialmente en el tiempo y puede incorporar impactos aleatorios como parte del modelo. El método ARIMA también admite la estacionalidad multiplicativa. Se aconseja a los lectores que deseen aprender más acerca del algoritmo ARIMA que lean el trabajo fundamental de Box y Jenkins; esta sección pretende proporcionar detalles específicos sobre cómo se ha implementado la metodología ARIMA en el algoritmo de serie temporal de Microsoft.  
  
 De forma predeterminada, el algoritmo de serie temporal de Microsoft usa ambos métodos, ARTXP y ARIMA, y mezcla los resultados para mejorar la precisión de la predicción. Si desea usar solo un método concreto, puede especificar los parámetros del algoritmo para usar únicamente ARTXP o únicamente ARIMA, o para controlar el modo en que se combinan los resultados de los algoritmos. Observe que el algoritmo ARTXP admite la predicción cruzada, mientras que el algoritmo ARIMA no la admite. Por consiguiente, la predicción cruzada solo está disponible cuando se usa una combinación de algoritmos o cuando se configura el modelo para usar solo ARTXP.  
  
## <a name="understanding-arima-difference-order"></a>Descripción del orden de diferencia de ARIMA  
 En esta sección se explica la terminología necesaria para entender el modelo ARIMA y la implementación concreta de las *diferencias* en el algoritmo de serie temporal de Microsoft. Para obtener una explicación completa de estos términos y conceptos, se recomienda revisar el trabajo de Box y Jenkins.  
  
-   Un término es un componente de una ecuación matemática. Por ejemplo, un término de una ecuación polinómica podría incluir una combinación de variables y constantes.  
  
-   La fórmula de ARIMA que se incluye en el algoritmo de serie temporal de Microsoft usa los dos términos: *regresión automática* y *media móvil* .  
  
-   Los modelos de serie temporal pueden ser *estacionarios* o *no estacionarios*. Los*modelos estacionarios* son aquellos que revierten a una media, aunque podrían tener ciclos, mientras que los *no estacionarios* no tienen un centro de equilibrio y están sujetos a mayores variaciones o cambios introducidos por los *impactos*o variables externas.  
  
-   El objetivo de la *diferenciación* es hacer que una serie temporal se estabilice y se convierta en estacionaria.  
  
-   El  *orden de diferencia* representa el número de veces que se toma la diferencia entre los valores para una serie temporal.  
  
 El algoritmo de serie temporal de Microsoft toma los valores de una serie de datos e intenta ajustarlos a un patrón. Si la serie de datos todavía no es estacionaria, el algoritmo aplica un orden de diferencia. Cada incremento en el orden de diferencia tiende a hacer que la serie temporal sea más estacionaria.  
  
 Por ejemplo, si tiene la serie temporal (z1, z2, …, zn) y realiza cálculos con un orden de diferencia, obtendrá una nueva serie (y1, y2,…., yn-1), donde `yi = zi+1-zi`. Cuando el orden de diferencia es 2, el algoritmo genera otra serie \`(x1, x2, …, xn-2)`, basada en la serie y que se derivó de la ecuación del primer orden. El grado correcto de diferencia depende de los datos. Un solo orden de diferencia es más común en los modelos que muestran una tendencia constante; un segundo orden de diferencia puede indicar una tendencia que varía con el tiempo.  
  
 De forma predeterminada, el orden de diferencia que se usa en el algoritmo de serie temporal de Microsoft es -1, lo que significa que el algoritmo detectará automáticamente el mejor valor para el orden de diferencia. Generalmente, el mejor valor es 1 (cuando se requiere una diferencia) pero, en ciertas circunstancias, el algoritmo aumentará el valor hasta un máximo de 2.  
  
 El algoritmo de serie temporal de Microsoft determina el orden de diferencia óptimo de ARIMA mediante los valores de regresión automática. El algoritmo examina los valores de AR y establece un parámetro oculto, ARIMA_AR_ORDER, que representa el orden de los términos de AR. Este parámetro oculto, ARIMA_AR_ORDER, tiene un intervalo de valores comprendido entre -1 y 8. Con el valor predeterminado -1, el algoritmo seleccionará automáticamente el orden de diferencia apropiado.  
  
 Siempre que el valor de ARIMA_AR_ORDER sea mayor que 1, el algoritmo multiplica la serie temporal por un término polinómico. Si un término de la fórmula polinómica se resuelve con una raíz de uno o con un valor cercano a 1, el algoritmo intenta conservar la estabilidad del modelo quitando el término e incrementando el orden de diferencia en 1. Si el orden de diferencia ya es el máximo, el término se quita y el orden de diferencia no cambia.  
  
 Por ejemplo, si el valor de AR es igual a 2, el término polinómico de AR podría ser similar a este: `1 – 1.4B + .45B^2 = (1- .9B) (1- 0.5B)`. Observe el término `(1- .9B)` que tiene una raíz de aproximadamente 0,9. El algoritmo elimina este término de la fórmula polinómica pero no puede incrementar el orden de diferencia en uno porque ya tiene el valor máximo de 2.  
  
 Es importante observar que el único modo en que puede **exigir** un cambio en el orden de diferencia es mediante el parámetro no admitido ARIMA_DIFFERENCE_ORDER. Este parámetro oculto controla el número de veces en que el algoritmo realiza la diferenciación de la serie temporal y puede establecerse escribiendo un parámetro del algoritmo personalizado. Sin embargo, no se recomienda cambiar este valor a menos que esté en disposición de experimentar y conozca los cálculos implicados. Tenga en cuenta igualmente que no hay ningún mecanismo, ni siquiera los parámetros ocultos, que le permita controlar el umbral en el que se activa el orden de diferencia.  
  
 Finalmente, observe que la fórmula descrita anteriormente es el caso simplificado y no tiene sugerencias de estacionalidad. Si se proporcionan sugerencias de estacionalidad, se agrega un término polinómico de AR diferente a la izquierda de la ecuación para cada sugerencia de estacionalidad y se aplica la misma estrategia para eliminar los términos que podrían desestabilizar las series diferenciadas.  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>Personalizar el algoritmo de serie temporal de Microsoft  
 El algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite los parámetros siguientes que afectan al comportamiento, rendimiento y precisión del modelo de minería de datos resultante.  
  
> [!NOTE]  
>  El algoritmo de serie temporal de Microsoft está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; sin embargo, algunas características avanzadas, como los parámetros para personalizar el análisis de series temporales, solo se admiten en ediciones concretas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
### <a name="detection-of-seasonality"></a>Detección de la estacionalidad  
 Los algoritmos ARTXP y ARIMA admiten la detección de la estacionalidad o periodicidad. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa la transformación rápida de Fourier para detectar la estacionalidad antes de realizar el entrenamiento. Sin embargo, es posible afectar a la detección de la estacionalidad y a los resultados del análisis de la serie temporal estableciendo los parámetros del algoritmo.  
  
-   Al cambiar el valor de *AUTODETECT_SEASONALITY*, puede influir en el número de posibles segmentos de tiempo que se generan.  
  
-   Al establecer un valor o varios valores para *PERIODICITY_HINT*, puede proporcionar información al algoritmo sobre los ciclos que se espera encontrar en los datos y posiblemente aumentar la exactitud de la detección.  
  
> [!NOTE]  
>  Los algoritmos ARTXP y ARIMA son muy sensibles a las sugerencias de estacionalidad. Por consiguiente, si se proporciona una sugerencia equivocada, los resultados pueden verse afectados de forma adversa.  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>Elegir un algoritmo y especificar la combinación de algoritmos  
 De forma predeterminada, o al seleccionar la opción MIXED, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] combina los algoritmos y les asigna el mismo peso. Sin embargo, en Enterprise Edition, puede especificar un algoritmo determinado, o puede personalizar la proporción de cada algoritmo en los resultados estableciendo un parámetro que pondere los resultados hacia la predicción a corto o a largo plazo. De forma predeterminada, el parámetro *FORECAST_METHOD* se establece en MIXED y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa ambos algoritmos para, luego, ponderar sus valores con el fin de obtener el máximo partido de cada algoritmo.  
  
-   Para controlar la elección de algoritmo, establezca el parámetro *FORECAST_METHOD* .  
  
-   Si desea utilizar la predicción cruzada, debe utilizar la opción ARTXP o MIXED, porque ARIMA no la admite.  
  
-   Establezca *FORECAST_METHOD* en ARTXP si quiere favorecer la predicción a corto plazo.  
  
-   Establezca *FORECAST_METHOD* en ARIMA si quiere mejorar la predicción a largo plazo.  
  
 En Enterprise Edition, también puede personalizar el modo en que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] realiza la combinación de los algoritmos ARIMA y ARTXP. Puede controlar tanto el punto inicial para la combinación como la tasa de cambio estableciendo el parámetro *PREDICTION_SMOOTHING* :  
  
-   Si establece *PREDICTION_SMOOTHING* en 0, el modelo solo usa ARTXP.  
  
-   Si establece *PREDICTION_SMOOTHING* en 1, el modelo solo usa ARIMA.  
  
-   Si establece *PREDICTION_SMOOTHING* en un valor entre 0 y 1, el modelo pondera el algoritmo ARTXP como una función exponencialmente decreciente de los pasos de predicción. Al mismo tiempo, el modelo también pondera el algoritmo ARIMA como complemento a uno del peso de ARTXP. El modelo usa la normalización y una constante de estabilización para suavizar las curvas.  
  
 En general, si predice hasta cinco intervalos de tiempo, ARTXP casi siempre es la mejor opción. Sin embargo, cuando aumenta el número de intervalos de tiempo que predecir, ARIMA suele funcionar mejor.  
  
 En el diagrama siguiente se muestra cómo el modelo combina los algoritmos cuando *PREDICTION_SMOOTHING* se establece en el valor predeterminado, 0,5. ARIMA y ARTXP se ponderan equitativamente al principio, pero a medida que el número de pasos de predicción aumenta, la ponderación de ARIMA es mayor.  
  
 ![curva predeterminada de la combinación de algoritmos de serie temporal](../../analysis-services/data-mining/media/time-series-mixing-default.gif "curva predeterminada de la combinación de algoritmos de serie temporal")  
  
 Por el contrario, el diagrama siguiente ilustra la combinación de los algoritmos cuando *PREDICTION_SMOOTHING* se establece en 0,2. En el paso [!INCLUDE[tabValue](../../includes/tabvalue-md.md)], el modelo pondera ARIMA como 0,2 y ARTXP como 0,8. Posteriormente, el peso de ARIMA aumenta exponencialmente y el de ARTXP disminuye exponencialmente.  
  
 ![curva de mezcla del modelo de serie tiempo caída](../../analysis-services/data-mining/media/time-series-blending-curve.gif "curva de mezcla del modelo de serie tiempo caída")  
  
### <a name="setting-algorithm-parameters"></a>Establecer parámetros del algoritmo  
 En la tabla siguiente se describen los parámetros que se pueden utilizar con el algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|Especifica un valor numérico entre [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] y 1 que detecta la periodicidad. El valor predeterminado es 0,6.<br /><br /> Si el valor está más próximo a [!INCLUDE[tabValue](../../includes/tabvalue-md.md)], la periodicidad solo se detecta en datos con una periodicidad muy marcada.<br /><br /> Cuando este valor está más próximo a 1, se favorece la detección de varios patrones que son casi periódicos y la generación automática de sugerencias de periodicidad.<br /><br /> Nota: Un gran número de sugerencias de periodicidad puede aumentar significativamente el tiempo de entrenamiento de los modelos, pero puede proporcionar modelos más precisos.|  
|*COMPLEXITY_PENALTY*|Controla el crecimiento del árbol de decisión. El valor predeterminado es 0,1.<br /><br /> Al disminuir este valor, aumenta la posibilidad de una división. Al aumentar este valor, disminuye la posibilidad de una división.<br /><br /> Nota: Este parámetro solo está disponible en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*FORECAST_METHOD*|Especifica qué algoritmo se ha de utilizar para el análisis y la predicción. Los valores posibles son ARTXP, ARIMA o MIXED. El valor predeterminado es MIXED.|  
|*HISTORIC_MODEL_COUNT*|Especifica el número de modelos históricos que se generarán. El valor predeterminado es 1.<br /><br /> Nota: Este parámetro solo está disponible en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*HISTORICAL_MODEL_GAP*|Especifica el intervalo temporal entre dos modelos históricos consecutivos. El valor predeterminado es 10. El valor representa varias unidades de tiempo, donde el modelo define la unidad.<br /><br /> Por ejemplo, si establece este valor en g, se generarán modelos históricos para datos truncados por segmentos temporales a intervalos de g, 2*g, 3\*g, etc.<br /><br /> Nota: Este parámetro solo está disponible en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*INSTABILITY_SENSITIVITY*|Controla el punto en el que la varianza de la predicción supera un cierto umbral, momento en el cual y el algoritmo ARTXP suprime las predicciones. El valor predeterminado es 1.<br /><br /> Nota: Este parámetro no se aplica a modelos que solo utilizan ARIMA.<br /><br /> El valor predeterminado (1) proporciona el mismo comportamiento que en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supervisa la desviación estándar normalizada para cada predicción. En cuanto este valor supera el umbral para cualquier predicción, el algoritmo de serie temporal devuelve un valor NULL y detiene el proceso de predicción.<br /><br /> El valor [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] detiene la detección de inestabilidad. Esto significa que puede crear un número infinito de predicciones, independientemente de la varianza.<br /><br /> Nota: Este parámetro solo se puede modificar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza solo el valor predeterminado 1.|  
|*MAXIMUM_SERIES_VALUE*|Especifica el valor máximo que se debe usar para las predicciones. Este parámetro se usa, junto con *MINIMUM_SERIES_VALUE*, para restringir las predicciones a un intervalo esperado. Por ejemplo, puede especificar que la predicción de la cantidad de ventas diaria nunca supere el número de productos en inventario.<br /><br /> Nota: Este parámetro solo está disponible en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*MINIMUM_SERIES_VALUE*|Especifica el valor mínimo que se puede predecir. Este parámetro se usa, junto con *MAXIMUM_SERIES_VALUE*, para restringir las predicciones a un intervalo esperado. Por ejemplo, puede especificar que la cantidad de ventas previstas nunca debe ser un número negativo.<br /><br /> Nota: Este parámetro solo está disponible en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*MINIMUM_SUPPORT*|Especifica el número mínimo de segmentos de tiempo necesarios para generar una división en cada árbol de serie temporal. El valor predeterminado es 10.|  
|*MISSING_VALUE_SUBSTITUTION*|Especifica cómo se llenan los espacios en los datos históricos. De forma predeterminada, no se permiten espacios en los datos. En la siguiente tabla se muestran los posibles valores para este parámetro.<br /><br /> **Previous**: repite el valor de la porción de tiempo anterior.<br /><br /> **Mean**: utiliza un promedio móvil de las porciones de tiempo que se usan para el entrenamiento.<br /><br /> Numeric constant: utiliza el número especificado para reemplazar todos los valores que faltan.<br /><br /> **None**: predeterminado. Reemplaza los valores que faltan por los valores trazados a lo largo de la curva del modelo entrenado.<br /><br /> <br /><br /> Tenga en cuenta que, si los datos contienen varias series, estas tampoco pueden tener bordes irregulares. Es decir, todas las series deben tener los mismos puntos inicial y final. <br />                    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también usa el valor de este parámetro para rellenar los espacios en los datos nuevos cuando se realiza una operación **PREDICTION JOIN** en el modelo de serie temporal.|  
|*PERIODICITY_HINT*|Proporciona una sugerencia al algoritmo en cuanto a la periodicidad de los datos. Por ejemplo, si las ventas varían por año y la unidad de medida en la serie son los meses, la periodicidad es 12. Este parámetro toma el formato de {n [, n]}, donde n es un número positivo.<br /><br /> La n de los corchetes [] es opcional y puede repetirse con la frecuencia que sea necesaria. Por ejemplo, para proporcionar varias sugerencias de periodicidad para los datos suministrados mensualmente, se puede escribir {12, 3, 1} para detectar patrones durante un año, trimestre o mes. Sin embargo, la periodicidad influye significativamente en la calidad del modelo. Si la sugerencia que se proporciona difiere de la periodicidad real, los resultados pueden verse afectados negativamente.<br /><br /> El valor predeterminado es \{1\}.<br /><br /> Tenga en cuenta que las llaves son obligatorias. Además, este parámetro tiene un tipo de datos de cadena. Por consiguiente, si se escribe este parámetro como parte de una instrucción de Extensiones de minería de datos (DMX), el número y las llaves se deben poner entre comillas.|  
|*PREDICTION_SMOOTHING*|Especifica cómo se debe combinar el modelo para optimizar el pronóstico. Se puede escribir cualquier valor entre [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] y 1, o utilizar uno de los valores siguientes:<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]:<br />                          Especifica que la predicción solo utiliza ARTXP. El pronóstico se optimiza para un menor número de predicciones.<br /><br /> 1: especifica que la predicción solo utiliza ARIMA. El pronóstico se optimiza para un gran número de predicciones.<br /><br /> 0.5: valor predeterminado. Especifica que se deben utilizar ambos algoritmos y combinar los resultados para la predicción.<br /><br /> <br /><br /> Al realizar el suavizado de predicción, use el parámetro *FORECAST_METHOD* para controlar el entrenamiento.   Tenga en cuenta que este parámetro solo está disponible en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 El algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las marcas de modelado siguientes. Al crear la estructura o el modelo de minería de datos, se definen las marcas de modelado que especifican cómo se tratan los valores de cada columna durante el análisis. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Marca de modelado|Description|  
|-------------------|-----------------|  
|NOT NULL|Indica que la columna no puede contener un valor NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.<br /><br /> Se aplica a las columnas de la estructura de minería de datos.|  
|MODEL_EXISTENCE_ONLY|Significa que la columna se tratará como si tuviera dos estados posibles: ausente y existente. Un valor NULL es un valor ausente.<br /><br /> Se aplica a las columnas del modelo de minería de datos.|  
  
## <a name="requirements"></a>Requisitos  
 Un modelo de serie temporal debe contener una columna de clave temporal que contenga valores únicos, columnas de entrada y al menos una columna de predicción.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite los tipos de contenido de columna de entrada, tipos de contenido de columna de predicción y marcas de modelado específicas que se indican en esta tabla.  
  
|Columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Continuous ,Key, Key Time y Table|  
|Atributo de predicción|Continuous y Table|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido Cyclical y Ordered, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Ejemplos de consultas de modelo de serie temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Contenido del modelo de minería de datos para modelos de serie temporal &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
