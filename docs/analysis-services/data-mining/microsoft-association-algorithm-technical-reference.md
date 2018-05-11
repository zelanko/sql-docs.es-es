---
title: Referencia técnica del algoritmo de asociación de Microsoft | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dfc939956a4c79b2b7c0fb45ce70499b7121937f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="microsoft-association-algorithm-technical-reference"></a>Referencia técnica del algoritmo de asociación de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El algoritmo Reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una implementación sencilla del conocido algoritmo Apriori.  
  
 Tanto el algoritmo Árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] como el algoritmo Reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] se pueden usar para analizar asociaciones, pero las reglas encontradas por cada uno de ellos pueden diferir. En un modelo de árboles de decisión, las divisiones que conducen a reglas específicas están basadas en la obtención de información, mientras que en un modelo de asociación, las reglas están basadas totalmente en la confianza. Por tanto, en un modelo de asociación, una regla segura, o una que tenga una confianza alta, puede que no tenga ningún interés, dado que no proporciona nueva información.  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Implementación del algoritmo de asociación de Microsoft  
 El algoritmo Apriori no analiza patrones, sino que genera y después cuenta *conjuntos de elementos candidatos*. Un elemento puede representar un evento, un producto o el valor de un atributo, dependiendo del tipo de datos que se analice.  
  
 En el tipo más común de modelo de asociación, las variables booleanas, que representan un valor Sí/No o Falta/Existe, se asignan a cada atributo, como un nombre de producto o evento. Un análisis de cesta de la compra es un ejemplo de un modelo de reglas de asociación que utiliza variables booleanas para representar la presencia o ausencia de determinados productos en la cesta de la compra de un cliente.  
  
 Para cada conjunto de elementos, el algoritmo crea puntuaciones que representan el soporte y la confianza. Estas puntuaciones se pueden usar para clasificar y derivar reglas interesantes de los conjuntos de elementos.  
  
 Los modelos de asociación se pueden crear también para atributos numéricos. Si los atributos son continuos, los números se pueden *discretizar* o agruparse en depósitos. A continuación, los valores de datos discretos se pueden tratar como booleanos o como pares atributo-valor.  
  
### <a name="support-probability-and-importance"></a>Soporte, probabilidad e importancia  
 *Soporte*, también denominado *frecuencia*, es el número de casos que contiene el elemento o la combinación de elementos de destino. Solo se pueden incluir en el modelo los elementos que tienen al menos el soporte especificado.  
  
 Se denomina *conjunto de elementos frecuente* a una colección de elementos cuya combinación de elementos también admite cantidades superiores al umbral definido por el parámetro MINIMUM_SUPPORT. Por ejemplo, si el conjunto de elementos es {A,B,C} y el valor de MINIMUM_SUPPORT es 10, cada uno de los elementos individuales A, B y C debe hallarse en al menos 10 casos para ser incluido en el modelo, y la combinación de elementos {A,B,C} debe hallarse también en al menos 10 casos.  
  
 **Nota** : también puede controlar el número de conjuntos de elementos de un modelo de minería de datos especificando la longitud máxima, es decir, el número de elementos, que puede tener un conjunto de elementos.  
  
 De forma predeterminada, el soporte para cualquier elemento o conjunto de elementos determinado representa un recuento de los casos que contienen dichos elementos. Sin embargo, también se puede expresar MINIMUM_SUPPORT como un porcentaje de los casos totales en el conjunto de datos, escribiendo el número como un valor decimal inferior a 1. Por ejemplo, si especifica un valor MINIMUM_SUPPORT de 0,03, significa que al menos el 3% del total de casos del conjunto de datos debe contener este elemento o conjunto de elementos para su inclusión en el modelo. Experimente con el modelo para determinar si resulta más apropiado usar un recuento o un porcentaje.  
  
 Por el contrario, el umbral para las reglas no se expresa como un recuento o un porcentaje, sino como una probabilidad, también denominada a veces *confianza*. Por ejemplo, si el conjunto de elementos {A,B,C} aparece en 50 casos, pero los conjuntos de elementos {A,B,D} y {A,B} aparecen también en 50 casos, resulta obvio que {A,B} no es un elemento de predicción confiable de {C}. Por lo tanto, para ponderar un resultado determinado en relación con todos los resultados conocidos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcula la probabilidad de la regla individual (como If {A,B} Then {C}) dividiendo el soporte del conjunto de elementos {A,B,C} por el soporte de todos los conjuntos de elementos relacionados.  
  
 Puede restringir el número de reglas que produce un modelo estableciendo un valor para MINIMUM_PROBABILITY.  
  
 Para cada regla creada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera una puntuación que indica su *importancia*, también denominada *elevación*. La importancia de la elevación se calcula de forma diferente para los conjuntos de elementos y para las reglas.  
  
 La importancia de un conjunto de elementos se calcula como la probabilidad de dicho conjunto dividida entre la probabilidad compuesta de los elementos individuales del conjunto. Por ejemplo, si un conjunto de elementos contiene {A, B}, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuenta primero todos los casos que contienen esta combinación A y B, divide dicho número entre el número total de casos y, a continuación, normaliza la probabilidad.  
  
 La importancia de una regla se calcula mediante la probabilidad de registro del lado derecho de la regla, dado el lado izquierdo de la regla. Por ejemplo, en la regla `If {A} Then {B}`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcula la proporción entre los casos con A y B y los casos con B pero sin A y, a continuación, normaliza dicha proporción mediante una escala logarítmica.  
  
### <a name="feature-selection"></a>Selección de características  
 El algoritmo Reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no realiza ningún tipo de selección automática de características. En su lugar, proporciona parámetros que controlan los datos utilizados por el algoritmo. Esto puede incluir límites en cuanto al tamaño de cada conjunto de elementos, o el establecimiento del soporte máximo y mínimo necesarios para agregar un conjunto de elementos al modelo.  
  
-   Para filtrar elementos y eventos muy comunes y, por lo tanto, poco interesantes, reduzca el valor de MAXIMUM_SUPPORT para quitar los conjuntos de elementos muy frecuentes del modelo.  
  
-   Para filtrar elementos y conjuntos de elementos poco frecuentes, aumente el valor de MINIMUM_SUPPORT.  
  
-   Para filtrar reglas, aumente el valor de MINIMUM_PROBABILITY.  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>Personalizar el algoritmo Reglas de asociación de Microsoft  
 El algoritmo Reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite varios parámetros que influyen en el comportamiento, el rendimiento y la precisión del modelo de minería de datos resultante.  
  
### <a name="setting-algorithm-parameters"></a>Establecer parámetros del algoritmo  
 Puede cambiar los parámetros para un modelo de minería de datos en cualquier momento mediante el Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede cambiarlos mediante programación utilizando la <xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A> colección en AMO, o mediante el [miningmodels, elemento &#40;ASSL&#41; ](../../analysis-services/scripting/collections/miningmodels-element-assl.md) en XMLA. Estos parámetros se describen en la tabla siguiente.  
  
> [!NOTE]  
>  No se pueden cambiar los parámetros en un modelo existente usando una instrucción de DMX; se deben especificar los parámetros en las instrucciones DMX CREATE MODEL o ALTER STRUCTURE… ADD MODEL cuando se crea el modelo.  
  
 *MAXIMUM_ITEMSET_COUNT*  
 Especifica el número máximo de conjuntos de elementos que se van a generar. Si no se especifica ningún número, se usa el valor predeterminado.  
  
 El valor predeterminado es 200000.  
  
> [!NOTE]  
>  Los conjuntos de elementos se clasifican según el soporte. Entre los conjuntos de elementos que tienen el mismo soporte, la ordenación es arbitraria.  
  
 *MAXIMUM_ITEMSET_SIZE*  
 Especifica el número máximo de elementos que se admiten en un conjunto de elementos. Si este valor se establece en 0, indica que no hay límite para el tamaño del conjunto de elementos.  
  
 El valor predeterminado es 3.  
  
> [!NOTE]  
>  Si se reduce este valor, es posible que se reduzca el tiempo necesario para crear el modelo, ya que el procesamiento de éste se detiene al alcanzar el límite.  
  
 *MAXIMUM_SUPPORT*  
 Especifica el número máximo de casos de los que dispone un conjunto de elementos para el soporte. Este parámetro se puede usar para eliminar elementos que aparecen frecuentemente y que, por lo tanto, son poco significativos.  
  
 Si este valor es menor que 1, el valor representa un porcentaje del total de casos. Los valores mayores que 1 representan el número absoluto de casos que puede contener el conjunto de elementos.  
  
 El valor predeterminado es 1.  
  
 *MINIMUM_ITEMSET_SIZE*  
 Especifica el número mínimo de elementos que se admiten en un conjunto de elementos. Si se aumenta este número, es posible que el modelo contenga menos conjuntos de elementos. Esto puede ser útil si, por ejemplo, se desea omitir conjuntos de elementos con un único elemento.  
  
 El valor predeterminado es 1.  
  
> [!NOTE]  
>  No se puede reducir el tiempo de procesamiento del modelo aumentando el valor mínimo, ya que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe calcular de todas formas las probabilidades para los elementos individuales como parte del procesamiento. Sin embargo, si se establece un valor mayor, se pueden filtrar conjuntos de elementos más pequeños.  
  
 *MINIMUM_PROBABILITY*  
 Especifica la probabilidad mínima de que se cumpla una regla.  
  
 Por ejemplo, si se establece este valor en 0,5, significa que no se puede generar ninguna regla con menos del cincuenta por ciento de probabilidad.  
  
 El valor predeterminado es 0.4.  
  
 *MINIMUM_SUPPORT*  
 Especifica el número mínimo de casos que debe contener el conjunto de elementos antes de que el algoritmo genere una regla.  
  
 Si se establece este valor en un número menor que 1, el número mínimo de casos se calcula como un porcentaje del total de casos.  
  
 Si se establece en un número entero mayor que 1, se especifica que el número mínimo de casos se calcula como el recuento de los casos que deben contener el conjunto de elementos. Si la memoria es limitada, el algoritmo puede aumentar automáticamente el valor de este parámetro.  
  
 El valor predeterminado es 0.03. Esto significa que para que un conjunto de elementos se incluya en el modelo, dicho conjunto debe hallarse en al menos el 3% de los casos.  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 Define el número de elementos que se van a almacenar en caché para optimizar la predicción.  
  
 El valor predeterminado es 0. Cuando se utiliza el valor predeterminado, el algoritmo produce tantas predicciones como se soliciten en la consulta.  
  
 Si especifica un valor distinto de cero para *OPTIMIZED_PREDICTION_COUNT* , las consultas de predicción pueden devolver como máximo el número especificado de elementos, aunque se soliciten predicciones adicionales. Sin embargo, el rendimiento de la predicción se puede mejorar estableciendo un valor.  
  
 Por ejemplo, si el valor se establece en 3, el algoritmo almacena en caché únicamente tres elementos para la predicción. No podrá ver predicciones adicionales que serán igualmente probables para los tres elementos devueltos.  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 El algoritmo Reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las siguientes marcas de modelado.  
  
 NOT NULL  
 Indica que la columna no puede contener un valor NULL. Se producirá un error si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encuentra un valor NULL durante el entrenamiento del modelo.  
  
 Se aplica a la columna de estructura de minería de datos.  
  
 MODEL_EXISTENCE_ONLY  
 Significa que la columna se tratará como si tuviera dos estados posibles: **Missing** y **Existing**. Un valor NULL es un valor ausente.  
  
 Se aplica a la columna de modelo de minería de datos.  
  
## <a name="requirements"></a>Requisitos  
 Un modelo de asociación debe contener una columna de clave, columnas de entrada y una sola columna de predicción.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo Reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se incluyen en la tabla siguiente. Para más información sobre el significado de los tipos de contenido en un modelo de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Cyclical, Discrete, Discretized, Key, Table y Ordered|  
|Atributo de predicción|Cyclical, Discrete, Discretized, Table, Ordered|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido Cyclical y Ordered, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de asociación de Microsoft](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Ejemplos de consultas de modelo de asociación](../../analysis-services/data-mining/association-model-query-examples.md)   
 [Contenido del modelo de minería de datos para modelos de asociación & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
