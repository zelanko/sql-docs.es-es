---
title: 'Contenido del modelo para los modelos de serie temporal de minería de datos (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4661c13dd33b8b0c329f93297475fc4185fcbe0a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="mining-model-content-for-time-series-models-analysis-services---data-mining"></a>Contenido del modelo de minería de datos para los modelos de serie temporal (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Todos los modelos de minería de datos utilizan la misma estructura para almacenar su contenido. Esta estructura se define según el conjunto de filas de esquema de contenido de minería de datos. Sin embargo, dentro de esa estructura estándar, los nodos que contienen información están organizados de maneras diferentes que representan varios tipos de árboles. En este tema se describe cómo se organizan los nodos, y lo que significa cada uno de ellos, para los modelos de minería de datos basados en el algoritmo de serie temporal [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Para obtener una explicación del contenido general del modelo de minería de datos que se aplica a todos los tipos de modelos, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 Al revisar este tema, puede resultarle útil explorar al mismo tiempo el contenido de un modelo de serie temporal. Puede crear un modelo de serie temporal completando el Tutorial básico de minería de datos. El modelo que se crea en el tutorial es un modelo mixto que entrena los datos utilizando los algoritmos ARIMA y ARTXP. Para más información sobre cómo visualizar el contenido de un modelo de minería de datos, vea [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md).  
  
## <a name="understanding-the-structure-of-a-time-series-model"></a>Descripción de la estructura de un modelo de serie temporal  
 Un modelo de serie temporal tiene un nodo primario único que representa el modelo y sus metadatos. Debajo ese nodo primario, hay uno o dos árboles de serie temporal, según el algoritmo que se haya utilizado para crearlo.  
  
 Si se crea un modelo mixto, se agregan al modelo dos árboles independientes, uno para ARIMA y otro para ARTXP. Si se ha elegido utilizar únicamente un algoritmo, ARTXP o ARIMA, tendremos un solo árbol correspondiente a ese algoritmo. Para especificar el algoritmo que se debe usar, establezca el parámetro FORECAST_METHOD. Para más información sobre qué modelo usar (ARTXP, ARIMA o mixto), vea [Algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
 En el siguiente diagrama se muestra un ejemplo de un modelo de minería de datos de serie temporal creado con la configuración predeterminada (modelo mixto). Para que pueda comparar más fácilmente las diferencias entre los dos modelos, en este caso se muestra el modelo ARTXP en el lado izquierdo del diagrama y el modelo ARIMA en el lado derecho.  Si bien ARTXP es una estructura de árbol que se divide bifurcaciones cada vez más pequeñas, la estructura creada por el algoritmo ARIMA se parece más a una pirámide erigida a partir de componentes más pequeños.  
  
 ![Estructura del contenido del modelo para los modelos de serie temporal](../../analysis-services/data-mining/media/modelcontentstructure-ts.gif "estructura del contenido del modelo para los modelos de serie temporal")  
  
 Lo que es importante recordar es que la información está organizada dentro de los árboles ARTXP y ARIMA de maneras completamente diferentes, de modo que los dos árboles se deben considerar relacionados exclusivamente en el nodo raíz. Aunque las dos representaciones se presentan en un solo modelo por comodidad, se deben tratar como dos modelos independientes. ARTXP representa una estructura de árbol real; en cambio, ARIMA, no.  
  
 Si usa el Visor de árbol de contenido genérico de Microsoft para ver un modelo que utiliza tanto ARIMA como ARTXP, los nodos de los modelos ARIMA y ARTXP se presentan siempre como nodos secundarios del modelo de serie temporal primario. Sin embargo, puede distinguirlos con facilidad por las etiquetas aplicadas a los nodos.  
  
-   El primer conjunto de nodos tiene la etiqueta (All), y representa los resultados del análisis mediante el algoritmo ARTXP.  
  
-   El segundo conjunto de nodos tiene la etiqueta ARIMA, y representa los resultados del análisis mediante el algoritmo ARIMA.  
  
> [!WARNING]  
>  El nombre (All) del árbol ARTXP solo se conserva por compatibilidad con versiones anteriores. Antes de SQL Server 2008, el algoritmo de serie temporal utilizaba un solo algoritmo para el análisis, ARTXP.  
  
 Las siguientes secciones explican cómo se organizan los nodos dentro de cada uno de estos tipos de modelo.  
  
### <a name="structure-of-an-artxp-model"></a>Estructura de un modelo ARTXP  
 El algoritmo ARTXP crea un modelo similar a un modelo de árboles de decisión. Agrupa atributos de predicción y los divide siempre que se encuentran diferencias significativas. Por consiguiente, cada modelo ARTXP contiene una bifurcación independiente para cada atributo de predicción. Por ejemplo, en el Tutorial básico de minería de datos se crea un modelo que predice la cantidad de ventas para varias regiones. En este caso, **[Amount]** es el atributo de predicción y se crea una bifurcación independiente para cada región. Si tuviera dos atributos de predicción, **[Amount]** y **[Quantity]**, se crearía una bifurcación independiente para cada combinación de atributo y región.  
  
 El nodo superior de la bifurcación ARTXP contiene la misma información que hay en el nodo raíz de un árbol de decisión. Esto incluye el número de elementos secundarios para ese nodo (CHILDREN_CARDINALITY), el número de casos que cumplen las condiciones de este nodo (NODE_SUPPORT), y diversas estadísticas descriptivas (NODE_DISTRIBUTION).  
  
 Si el nodo no tiene ningún elemento secundario, es porque no se ha encontrado ninguna condición significativa que justifique dividir los casos en más subgrupos. La bifurcación finaliza en este punto y el nodo se denomina *nodo hoja*. El nodo de hoja contiene los atributos, coeficientes y valores que son los bloques de creación de la fórmula ARTXP.  
  
 Algunas bifurcaciones pueden tener más divisiones, al igual que sucede en los modelos de árboles de decisión. Por ejemplo, la bifurcación del árbol que representa las ventas para la región de Europa divide en dos bifurcaciones. Se produce una bifurcación cuando existe una condición que da lugar a una diferencia significativa entre los dos grupos. El nodo primario indica el nombre del atributo que ha provocado la división, como [Amount] y la cantidad de casos que hay en el nodo primario. Los nodos hoja proporcionan más detalles: el valor del atributo, como [Sales] > 10 000, en lugar de [Sales] < 10 000), el número de casos que cumplen cada condición, y la fórmula ARTXP.  
  
> [!NOTE]  
>  Si desea ver las fórmulas, encontrará la fórmula de regresión completa en el nivel del nodo de hoja, pero no en los nodos intermedios o raíz.  
  
### <a name="structure-of-an-arima-model"></a>Estructura de un modelo ARIMA  
 El algoritmo ARIMA crea un solo dato para cada combinación de una serie de datos (como **[Region]**) y un atributo de predicción (como **[Sales Amount]**), la ecuación que describe el cambio del atributo de predicción a lo largo del tiempo.  
  
 La ecuación para cada serie se deriva de varios componentes, uno para cada estructura periódica encontrada en los datos. Por ejemplo, si tiene datos de ventas que se recopilan mensualmente, el algoritmo podría detectar estructuras mensuales, trimestrales o anuales.  
  
 El algoritmo genera un conjunto independiente de nodo primario y nodos secundarios para cada periodicidad que encuentra. La periodicidad predeterminado es de 1, para un intervalo de tiempo único, y se agrega automáticamente en todos los modelos. Puede especificar las posibles estructuras periódicas escribiendo varios valores en el parámetro PERIODICITY_HINT. Sin embargo, si el algoritmo no detecta una estructura periódica, no generará resultados para esa sugerencia.  
  
 Cada estructura periódica que se genera en el contenido del modelo contiene los siguientes nodos de componente:  
  
-   Un nodo para el *orden de regresión automática* (AR)  
  
-   Un nodo para la *media móvil* (MA)  
  
 Para más información sobre el significado de estos términos, vea [Algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
 El *orden de diferencia* es una parte importante de la fórmula y se representa en la ecuación. Para más información sobre el uso del orden de diferencia, vea [Referencia técnica del algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
## <a name="model-content-for-time-series"></a>Contenido del modelo para series temporales  
 En esta sección solo se proporcionan detalles y ejemplos de las columnas del contenido del modelo de minería de datos que tienen una relevancia especial para los modelos de series temporales.  
  
 Para información sobre las columnas de uso general en el conjunto de filas de esquema, como MODEL_CATALOG y MODEL_NAME, o para obtener una explicación de la terminología del modelo de minería de datos, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Nombre de la base de datos en la que se almacena el modelo.  
  
 MODEL_NAME  
 Nombre del modelo.  
  
 ATTRIBUTE_NAME  
 Atributo predecible para la serie de datos representada en el nodo. (El mismo valor que para MSOLAP_MODEL_COLUMN.)  
  
 NODE_NAME  
 Nombre del nodo.  
  
 Actualmente, esta columna contiene el mismo valor que NODE_UNIQUE_NAME, aunque esto podría cambiar en versiones futuras.  
  
 NODE_UNIQUE_NAME  
 Nombre único del nodo. El nodo primario del modelo siempre se denomina **TS**.  
  
 **ARTXP:** cada nodo se representa mediante TS seguido de un valor numérico hexadecimal. El orden de los nodos carece de relevancia.  
  
 Por ejemplo, los nodos ARTXP que figuran directamente bajo el árbol TS podrían llevar los números TS00000001-TS0000000b.  
  
 **ARIMA:** cada nodo de un árbol ARIMA se representa mediante TA seguido por un valor numérico hexadecimal. Los nodos secundarios contienen el nombre único del nodo primario seguido por otro número hexadecimal que indica la secuencia dentro del nodo.  
  
 Todos los árboles ARIMA están estructurados exactamente igual. Cada raíz contiene los nodos y la convención de nomenclatura cuyo ejemplo se muestra en la siguiente tabla:  
  
|Identificador y tipo de nodo ARIMA|Ejemplo de nombre de nodo|  
|----------------------------|--------------------------|  
|Raíz ARIMA (27)|TA0000000b|  
|Estructura periódica ARIMA (28)|TA0000000b00000000|  
|Regresión automática ARIMA (29)|TA0000000b000000000|  
|Media móvil ARIMA (30)|TA0000000b000000001|  
  
 NODE_TYPE  
 Un modelo de serie temporal genera los siguientes tipos de nodo, dependiendo del algoritmo.  
  
 **ARTXP:**  
  
|Identificador del tipo de nodo|Description|  
|------------------|-----------------|  
|1 (Modelo)|Serie temporal|  
|3 (interior)|Representa una bifurcación interior dentro de un árbol de serie temporal ARTXP.|  
|16 (árbol de serie temporal)|Raíz de árbol ARTXP que corresponde a un atributo y serie de predicción.|  
|15 (serie temporal)|Nodo de hoja en árbol ARTXP.|  
  
 **ARIMA:**  
  
|Identificador del tipo de nodo|Description|  
|------------------|-----------------|  
|27 (Raíz ARIMA)|Nodo superior de un árbol ARIMA.|  
|28 (Estructura periódica ARIMA)|Componente de un árbol ARIMA que describe una sola estructura periódica.|  
|29 (Regresión automática ARIMA)|Contiene un coeficiente para una sola estructura periódica.|  
|30 (Media móvil ARIMA)|Contiene un coeficiente para una sola estructura periódica.|  
  
 NODE_CAPTION  
 Etiqueta o título asociado al nodo.  
  
 Esta propiedad se usa principalmente para la presentación.  
  
 **ARTXP:** contiene la condición de división del nodo, mostrada como una combinación de atributo y rango de valores.  
  
 **ARIMA:** contiene la forma abreviada de la ecuación ARIMA.  
  
 Para obtener información sobre el formato de la ecuación ARIMA, vea [Leyenda de minería de datos para ARIMA](#bkmk_ARIMA_2).  
  
 CHILDREN_CARDINALITY  
 Número de elementos secundarios directos que tiene el nodo.  
  
 PARENT_UNIQUE_NAME  
 Nombre único del nodo primario del nodo. Se devuelve NULL para todos los nodos del nivel raíz.  
  
 NODE_DESCRIPTION  
 Descripción en el texto de las reglas, divisiones o fórmulas del nodo actual.  
  
 **ARTXP:** para obtener más información, vea [Descripción del árbol ARTXP](#bkmk_ARTXP_1).  
  
 **ARIMA:** para obtener más información, vea [Descripción del árbol ARIMA](#bkmk_ARIMA_1).  
  
 NODE_RULE  
 Descripción XML de las reglas, divisiones o fórmulas del nodo actual.  
  
 **ARTXP:** NODE_RULE suele corresponder a NODE_CAPTION.  
  
 **ARIMA:** para obtener más información, vea [Descripción del árbol ARIMA](#bkmk_ARIMA_1).  
  
 MARGINAL_RULE  
 Descripción XML de la división o del contenido que es específico de ese nodo.  
  
 **ARTXP:** MARGINAL_RULE suele corresponder a NODE_DESCRIPTION.  
  
 **ARIMA:** siempre en blanco; use NODE_RULE en su lugar.  
  
 NODE_PROBABILITY  
 **ARTXP:** para los nodos de árbol, siempre 1. Para los nodos de hoja, la probabilidad de alcanzar el nodo a partir del nodo raíz del modelo.  
  
 **ARIMA:** siempre 0.  
  
 MARGINAL_PROBABILITY  
 **ARTXP:** para los nodos de árbol, siempre 1. Para los de nodos hoja, la probabilidad de alcanzar el nodo a partir del nodo primario inmediato.  
  
 **ARIMA:** siempre 0.  
  
 NODE_DISTRIBUTION  
 Tabla que contiene el histograma de probabilidad del nodo. En un modelo de serie temporal, esta tabla anidada contiene todos los componentes necesarios para ensamblar la fórmula de regresión real.  
  
 Para obtener más información sobre la tabla de distribución de nodos en un árbol ARTXP, vea [Descripción del árbol ARTXP](#bkmk_ARTXP_1).  
  
 Para obtener más información sobre la tabla de distribución de nodos en un árbol ARIMA, vea [Descripción del árbol ARIMA](#bkmk_ARIMA_1).  
  
 Si desea ver todas las constantes y otros componentes organizados en un formato legible, utilice el [Visor de series temporales](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), haga clic en el nodo y abra la **Leyenda de minería de datos**.  
  
 NODE_SUPPORT  
 Número de casos que admiten este nodo.  
  
 **ARTXP:** para el nodo **(All)** , indica el número total de intervalos de tiempo incluidos en la bifurcación.  
  
 Para los nodos terminales, indica el número de intervalos de tiempo que están incluidos en el intervalo descrito por NODE_CAPTION. El número de intervalos de tiempo de los nodos terminales siempre se suma al valor de NODE_SUPPORT del nodo de bifurcación **(All)** .  
  
 **ARIMA:** recuento de casos que soportan la estructura periódica actual. El valor del soporte se repite en todos los nodos de la estructura periódica actual.  
  
 MSOLAP_MODEL_COLUMN  
 Atributo predecible para la serie de datos representada en el nodo. (El mismo valor que para ATTRIBUTE_NAME.)  
  
 MSOLAP_NODE_SCORE  
 Valor numérico que caracteriza el valor de información del árbol o de la división.  
  
 **ARTXP:** el valor siempre es 0,0 para los nodos que no tienen ninguna división. Para los nodos con una división, el valor representa la puntuación de grado de interés de la división.  
  
 Para más información sobre los métodos de puntuación, vea [Selección de características &#40;minería de datos&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md).  
  
 **ARIMA:** la puntuación Bayesian Information Criterion (BIC) del modelo ARIMA. La misma puntuación se establece en todos los nodos ARIMA relacionados con la ecuación.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 **ARTXP:**  la misma información que NODE_DESCRIPTION.  
  
 **ARIMA:** la misma información que NODE_CAPTION, es decir, la forma abreviada de la ecuación ARIMA.  
  
##  <a name="bkmk_ARTXP_1"></a> Descripción del árbol ARTXP  
 El modelo ARTXP separa claramente las áreas de los datos que son lineales de las áreas de los datos que se dividen en función de algún otro factor. Siempre que los cambios del atributo de predicción se puedan representar directamente como una función de las variables independientes, se calcula una fórmula de regresión para representar esa relación  
  
 Por ejemplo, si hay una correlación directa entre el tiempo y las ventas para la mayoría de las series de datos, cada serie estaría incluida en un árbol de serie temporal (NODE_TYPE = 16) que no tendría ningún nodo secundario para cada serie de datos, sino únicamente una ecuación de regresión. Sin embargo, si la relación no es lineal, un árbol de serie temporal ARTXP se puede dividir en nodos secundarios para cada condición, exactamente igual que sucede en un modelo de árbol de decisión. Viendo el contenido del modelo en el **Visor de árbol de contenido genérico de Microsoft** , se puede apreciar dónde se producen las divisiones y cómo esto afecta a la línea de tendencia.  
  
 Para entender mejor este comportamiento, puede revisar el modelo de la serie temporal creado en el [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Este modelo, basado en el almacén de datos de AdventureWorks, no utiliza datos especialmente complejos. Por consiguiente, no hay muchas divisiones en el árbol ARTXP. Sin embargo, incluso este modelo relativamente simple muestra tres tipos diferentes de divisiones:  
  
-   La línea de tendencia [Amount] correspondiente a la región del Pacífico se divide en función de la clave temporal. Una división en función de la clave temporal significa que se produce un cambio en la tendencia en un momento determinado. La línea de tendencia únicamente fue lineal hasta un momento determinado; a continuación, la curva adoptó una forma diferente. Por ejemplo, una serie temporal podría continuar hasta el 6 de agosto de 2002 y otra, iniciarse después de esa fecha.  
  
-   La línea de tendencia [Amount] de la región de Norteamérica se divide en función de otra variable. En este caso, la tendencia para las divisiones de Norteamérica se basan en el valor para el mismo modelo en la región de Europa. En otras palabras, el algoritmo detectó que cuando el valor para Europa cambia, también lo hace el valor para Norteamérica.  
  
-   La línea de tendencia para la región de Europa se divide por sí sola.  
  
 ¿Qué significa cada división? Interpretar la información que transmite el modelo de contenido es un arte que requiere una comprensión profunda de los datos y su significado en el contexto empresarial.  
  
-   El vínculo aparente entre las tendencias para las regiones de Europa y Norteamérica podría significar solamente que la serie de datos para Europa tiene más entropía, lo que hace que la tendencia para Norteamérica parezca más débil. Pero también puede ser que no haya ninguna diferencia significativa en las puntuaciones de ambas y que la correlación sea accidental, debida simplemente en que se han llevado a cabo los cálculos de Europa antes que los de Norteamérica. Sin embargo, podría ser conveniente repasar los datos y asegurarse de si se trata de una correlación falsa, o investigar para comprobar si hay algún otro factor que afecte.  
  
-   La división en función de la clave temporal significa que existe un cambio estadísticamente significativo en el degradado de la línea. Esto puede deberse a factores matemáticos, como el soporte para cada intervalo, o los cálculos de la entropía necesaria para la división. Así pues, esta división podría no revestir interés por lo que se refiere al significado del modelo en el mundo real. Sin embargo, al revisar el período de tiempo indicado en la división, podrían encontrarse correlaciones interesantes que no están representadas en los datos, como una promoción comercial u otro evento que se inició en ese momento y puede haber afectado a los datos.  
  
 Si los datos contuvieran otros atributos, muy probablemente se apreciarían ejemplos más interesantes de bifurcaciones en el árbol. Por ejemplo, si se hubiera realizado el seguimiento de la información meteorológica y se hubiera utilizado como atributo para el análisis, es posible que el árbol incluyese varias divisiones que representasen la interacción compleja entre las ventas y las condiciones meteorológicas.  
  
 En pocas palabras, la minería de datos es útil para proporcionar sugerencias de cuándo se producen fenómenos potencialmente interesantes, pero se requiere una investigación más extensa y experiencia por parte de los usuarios empresariales para interpretar con precisión el valor de la información en su contexto.  
  
### <a name="elements-of-the-artxp-time-series-formula"></a>Elementos de la fórmula de serie temporal ARTXP  
 Para ver la fórmula completa de un árbol o una bifurcación ARTXP, se recomienda usar la **Leyenda de minería de datos** del [Visor de series temporales de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), que presenta todas las constantes en un formato legible.  
  
-   [Ver la fórmula de un modelo de serie temporal &#40;Minería de datos&#41;](../../analysis-services/data-mining/view-the-formula-for-a-time-series-model-data-mining.md)  
  
 La siguiente sección presenta una ecuación de ejemplo y explica los términos básicos.  
  
#### <a name="mining-legend-for-an-artxp-formula"></a>Leyenda de minería de datos de una fórmula ARTXP  
 En el siguiente ejemplo se muestra la fórmula ARTXP de una parte del modelo, tal y como aparece en la **Leyenda de minería de datos**. Para ver esta fórmula, abra el modelo [Forecasting] que creó en el Tutorial básico de minería de datos en el Visor de series temporales de Microsoft, haga clic en la pestaña **Modelo** y seleccione el árbol de la serie de datos R250: Europe.  
  
 Para ver la ecuación utilizada para este ejemplo, haga clic en el nodo que representa la serie de fecha correspondiente al día 7/5/2003 o después.  
  
 Ejemplo de ecuación de nodo de árbol:  
  
 `Quantity = 21.322 -0.293 * Quantity(R250 North America,-7) + 0.069 * Quantity(R250 Europe,-1) + 0.023 * Quantity(R250 Europe,-3) -0.142 * Quantity(R750 Europe,-8)`  
  
 En este caso, el valor 21.322 representa el valor que se predice para Quantity como una función de los siguientes elementos de la ecuación.  
  
 Por ejemplo, un elemento es `Quantity(R250 North America,-7)`. Esta notación halla la media de la cantidad correspondiente a la región de Norteamérica en `t-7`, o siete intervalos de tiempo antes del intervalo de tiempo actual. El valor de esta serie de datos se multiplica por el coeficiente -0.293. El coeficiente de cada elemento se obtiene durante el proceso de entrenamiento y se basa en las tendencias halladas en los datos.  
  
 Hay varios elementos en esta ecuación porque el modelo ha calculado que la cantidad del modelo del R250 en la región de Europa depende de los valores de varias series de datos más.  
  
#### <a name="model-content-for-an-artxp-formula"></a>Contenido del modelo para una fórmula ARTXP  
 La siguiente tabla muestra la misma información para la fórmula, usando el contenido del nodo pertinente como se muestra en [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Quantity(R250 Europe,y-intercept)|21.3223433563772|11|0|1.65508795539661|11 (intersección)|  
|Quantity(R250 Europe,-1)|0.0691694140876526|0|0|0|7 (coeficiente)|  
|Quantity(R250 Europe,-1)|20.6363635858123|0|0|182.380682874818|9 (estadísticas)|  
|Quantity(R750 Europe,-8)|-0.1421203048299|0|0|0|7 (coeficiente)|  
|Quantity(R750 Europe,-8)|22.5454545333019|0|0|104.362130048408|9 (estadísticas)|  
|Quantity(R250 Europe,-3)|0.0234095979448281|0|0|0|7 (coeficiente)|  
|Quantity(R250 Europe,-3)|24.8181818883176|0|0|176.475304989169|9 (estadísticas)|  
|Quantity(R250 North America,-7)|-0.292914186039869|0|0|0|7 (coeficiente)|  
|Quantity(R250 North America,-7)|10.36363640433|0|0|701.882534898676|9 (estadísticas)|  
  
 Como puede comprobar al comparar estos ejemplos, el contenido del modelo de minería de datos incluye la misma información que está disponible en la **Leyenda de minería de datos**, pero con columnas adicionales para la *varianza* y el *soporte*. El valor del soporte indica el recuento de casos que admiten la tendencia descrita por esta ecuación.  
  
### <a name="using-the-artxp-time-series-formula"></a>Utilizar la fórmula de serie temporal ARTXP  
 Para la mayoría de los usuarios empresariales, el valor del contenido del modelo ARTXP reside en que combina una vista de árbol y una representación lineal de los datos.  
  
-   Si los cambios del atributo de predicción se pueden representar como una función lineal de las variables independientes, el algoritmo calculará la ecuación de regresión automáticamente y generará esa serie en un nodo independiente.  
  
-   Cuando la relación no se puede expresar como una correlación lineal, la serie temporal se bifurca como un árbol de decisión.  
  
 Examinando el contenido del modelo en el [Visor de series temporales de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md) , se puede observar dónde se produce la división y cómo afecta a la línea de tendencia.  
  
 Si existe una correlación directa entre el tiempo y las ventas en cualquier parte de la serie de datos, la manera más fácil de obtener la fórmula es copiarla de la **Leyenda de minería de datos**y, a continuación, pegarla en un documento o presentación, para ayudar a explicar el modelo. Como alternativa, se podrían extraer la media, el coeficiente y otra información de la tabla NODE_DISTRIBUTION de ese árbol y utilizarla para calcular extensiones de la tendencia. Si la serie completa presenta una relación lineal coherente, la ecuación estará contenida en el nodo (All). Si hay alguna bifurcación en el árbol, la ecuación se incluirá en el nodo de hoja.  
  
 La siguiente consulta devuelve todos los nodos de hoja ARTXP de un modelo de minería de datos, junto con la tabla anidada, NODE_DISTRIBUTION, que contiene la ecuación.  
  
```  
SELECT MODEL_NAME, ATTRIBUTE_NAME, NODE_NAME,  
NODE_CAPTION,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [VARIANCE], VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_TYPE = 15  
```  
  
##  <a name="bkmk_ARIMA_1"></a> Descripción del árbol ARIMA  
 Cada estructura en un modelo ARIMA se corresponde con una *periodicidad* o *estructura periódica*. Una estructura periódica es un patrón de datos que se repite a lo largo de la serie de datos. Se permite alguna variación secundaria en el patrón, dentro de los límites estadísticos. La periodicidad se mide según las unidades de tiempo predeterminadas que se utilizaron en los datos de entrenamiento. Por ejemplo, si los datos de entrenamiento proporcionan datos de ventas para cada día, la unidad de tiempo predeterminada será un día, y todas las estructuras periódicas se definirán como un número concreto de días.  
  
 Cada período que el algoritmo detecta obtiene su propio nodo de estructura. Por ejemplo, si se están analizando los datos de las ventas diarias, el modelo podría detectar estructuras periódicas que representen semanas. En este caso, el algoritmo crearía dos estructuras periódicas en el modelo terminado: uno para el período diario predeterminado, que se indica con la notación {1}, y otro para las semanas, que se indica mediante {7}.  
  
 Por ejemplo, la siguiente consulta devuelve todas las estructuras ARIMA de un modelo de minería de datos.  
  
```  
SELECT MODEL_NAME, ATTRIBUTE_NAME, NODE_NAME, NODE_CAPTION  
FROM Forecasting.CONTENT  
WHERE NODE_TYPE = 27  
```  
  
 Resultados del ejemplo:  
  
|MODEL_NAME|ATTRIBUTE_NAME|NODE_NAME|NODE_TYPE|NODE_CAPTION|  
|-----------------|---------------------|----------------|----------------|-------------------|  
|Forecasting|M200 Europe:Quantity|TA00000000|27|ARIMA (1,0,1)|  
|Forecasting|M200 North America:Quantity|TA00000001|27|ARIMA (1,0,4) X (1,1,4)(6)|  
|Forecasting|M200 Pacific:Quantity|TA00000002|27|ARIMA (2,0,8) X (1,0,0)(4)|  
|Forecasting|M200 Pacific:Quantity|TA00000002|27|ARIMA (2,0,8) X (1,0,0)(4)|  
|Forecasting|R250 Europe:Quantity|TA00000003|27|ARIMA (1,0,7)|  
|Forecasting|R250 North America:Quantity|TA00000004|27|ARIMA (1,0,2)|  
|Forecasting|R250 Pacific:Quantity|TA00000005|27|ARIMA (2,0,2) X (1,1,2)(12)|  
|Forecasting|R750 Europe:Quantity|TA00000006|27|ARIMA (2,1,1) X (1,1,5)(6)|  
|Forecasting|T1000 Europe:Quantity|TA00000009|27|ARIMA (1,0,1)|  
|Forecasting|T1000 North America:Quantity|TA0000000a|27|ARIMA (1,1,1)|  
|Forecasting|T1`000 Pacific:Quantity|TA0000000b|27|ARIMA (1,0,3)|  
  
 A partir de estos resultados, que también se pueden examinar mediante el [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c), se puede deducir de un vistazo qué series son completamente lineales, cuáles tienen varias estructuras periódicas y qué periodicidades se han detectado.  
  
 Por ejemplo, la forma abreviada de la ecuación ARIMA para la serie M200 Europe indica que únicamente se ha detectado el ciclo predeterminado, o diario. La forma abreviada de la ecuación se proporciona en la columna NODE_CAPTION.  
  
 Sin embargo, para la serie M200 North America, se encontró una estructura periódica más. El nodo TA00000001 tiene dos nodos secundarios, uno con la ecuación (1,0,4) y otro con la ecuación (1,1,4)(6). Estas ecuaciones se concatenan y presentan en el nodo primario.  
  
 Para cada estructura periódica, el contenido del modelo proporciona también el *orden* y la *media móvil* como nodos secundarios. Por ejemplo, la siguiente consulta recupera los nodos secundarios de uno de los nodos enumerados en el ejemplo anterior. Observe que la columna, PARENT_UNIQUE_NAME, debe ir entre corchetes para distinguirla de la palabra clave reservada con la misma denominación.  
  
```  
SELECT *   
FROM Forecasting.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = ' TA00000001'  
```  
  
 Dado que se trata de un árbol ARIMA, y no de un árbol ARTXP, no se puede usar la función [IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md) para devolver los nodos secundarios de esta estructura periódica. En cambio, puede utilizar los tipos de nodo y atributo para filtrar los resultados y devolver los nodos secundarios que aportan mayor detalle sobre cómo se ha creado la ecuación, incluidas las medias móviles y el orden de diferencia.  
  
```  
SELECT MODEL_NAME, ATTRIBUTE_NAME, NODE_UNIQUE_NAME,  
NODE_TYPE,  NODE_CAPTION  
FROM Forecasting.CONTENT  
WHERE [MSOLAP_MODEL_COLUMN] ='M200 North America:Quantity'  
AND (NODE_TYPE = 29 or NODE_TYPE = 30)  
```  
  
 Resultados del ejemplo:  
  
|MODEL_NAME|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|NODE_TYPE|NODE_CAPTION|  
|-----------------|---------------------|------------------------|----------------|-------------------|  
|Forecasting|M200 North America:Quantity|TA00000001000000010|29|ARIMA {1,0.961832044807041}|  
|Forecasting|M200 North America:Quantity|TA00000001000000011|30|ARIMA {1,-3.51073103693271E-02,2.15731642954099,-0.220314343327742,-1.33151478258758}|  
|Forecasting|M200 North America:Quantity|TA00000001000000000|29|ARIMA {1,0.643565911081657}|  
|Forecasting|M200 North America:Quantity|TA00000001000000001|30|ARIMA {1,1.45035399809581E-02,-4.40489283927752E-02,-0.19203901352577,0.242202497643993}|  
  
 Estos ejemplos muestran que cuanto más se profundiza en el árbol ARIMA, más detalles se revelan, pero la información importante se combina y presenta también en el nodo primario.  
  
### <a name="time-series-formula-for-arima"></a>Fórmula de serie temporal para ARIMA  
 Para ver la fórmula completa de cualquier nodo ARIMA, recomendamos utilizar la **Leyenda de minería de datos** del [Visor de series temporales de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), que presenta el orden de regresión automática, las medias móviles y otros elementos de la ecuación organizados en un formato coherente.  
  
-   [Ver la fórmula de serie temporal de un modelo & #40; minería de datos & #41;](../../analysis-services/data-mining/view-the-formula-for-a-time-series-model-data-mining.md)  
  
 En esta sección se presenta una ecuación de ejemplo y se explican los términos básicos.  
  
####  <a name="bkmk_ARIMA_2"></a> Leyenda de minería de datos para la fórmula ARIMA  
 En el siguiente ejemplo se muestra la fórmula ARIMA para una parte del modelo, tal y como aparece en la Leyenda de minería de datos. Para ver esta fórmula, abra el modelo **Forecasting** en el **Visor de series temporales de Microsoft**, haga clic en la pestaña **Modelo** , seleccione el árbol de la serie de datos **R250: Europe** y luego haga clic en el nodo que representa la serie de fecha correspondiente al día 7/5/2003 o después. La leyenda de minería de datos organiza todas las constantes en un formato legible, que se muestra en este ejemplo:  
  
 Ecuación ARIMA:  
  
`ARIMA ({1,1},0,{1,1.49791920964142,1.10640053499397,0.888873034670339,-5.05429403071953E-02,-0.905265316720334,-0.961908900643379,-0.649991020901922}) Intercept:56.8888888888889`  
  
 Esta ecuación está en el formato ARIMA largo, que incluye los valores de los coeficientes y la intersección. El formato abreviado de esta ecuación sería {1,0,7}, donde 1 indica el período como un recuento de intervalos de tiempo, 0 indica que el orden de diferencia de término y 7 indica el número de coeficientes.  
  
> [!NOTE]  
>  Analysis Services calcula una constante para hallar la varianza, pero la constante en sí no se muestra en la interfaz de usuario. Sin embargo, puede ver la varianza correspondiente a cualquier punto de la serie como una función de esta constante; para ello, seleccione **Mostrar desviaciones** en la vista **Gráfico** . La Información sobre herramientas para cada serie de datos muestra la varianza correspondiente a un punto predicho concreto.  
  
#### <a name="model-content-for-arima-formula"></a>Contenido del modelo para la fórmula ARIMA  
 Un modelo ARIMA sigue una estructura estándar, donde la información diferente está contenida en nodos de tipos distintos. Para ver el contenido del modelo correspondiente al modelo ARIMA, cambie al **Visor de árbol de contenido genérico de Microsoft**y, a continuación, expanda el nodo cuyo nombre de atributo es **R250 Europe: Quantity**.  
  
 Un modelo ARIMA para un serie de datos contiene la ecuación periódica básica en cuatro formatos diferentes, entre los que se puede elegir, según la aplicación.  
  
 **NODE_CAPTION:** muestra el formato abreviado de la ecuación. El formato abreviado indica cuántas estructuras periódicas se representan y cuántos coeficientes tienen. Por ejemplo, si el formato abreviado de la ecuación es `{4,0,6}`, el nodo representa una estructura periódica con 6 coeficientes. Si el formato abreviado es del tipo `{2,0,8} x {1,0,0}(4)`, el nodo contiene dos estructuras periódicas.  
  
 **NODE DESCRIPTION:** muestra el formato largo de la ecuación, que también es la forma de la ecuación que aparece en la **Leyenda de minería de datos**. La forma larga de la ecuación es similar a la forma abreviada, con la salvedad de que se muestran los valores reales de los coeficientes, en lugar contarse.  
  
 **NODE_RULE:** muestra una representación XML de la ecuación. Según el tipo de nodo, la representación XML puede incluir una o varias estructuras periódicas. En la siguiente tabla se muestra cómo se acumlan los nodos XML en niveles más altos del modelo ARIMA.  
  
|Tipo de nodo|Contenido XML|  
|---------------|-----------------|  
|27 (Raíz ARIMA)|Incluye todas las estructuras periódicas para la serie de datos, así como el contenido de todos los nodos secundarios para cada estructura periódica.|  
|28 (Estructura periódica ARIMA)|Define una sola estructura periódica, incluso su nodo de términos de regresión automática y sus coeficientes de media móvil.|  
|29 (Regresión automática ARIMA)|Enumera los términos para una estructura periódica única.|  
|30 (Media móvil ARIMA)|Enumera los coeficientes para una estructura periódica única.|  
  
 **NODE_DISTRIBUTION:** muestra los términos de la ecuación en una tabla anidada, que se puede consultar para obtener términos concretos. La tabla de distribución de nodos sigue la misma estructura jerárquica que las reglas XML. Es decir, el nodo raíz de la serie ARIMA (NODE_TYPE = 27) contiene el valor de intersección y las periodicidades de toda la ecuación, que puede incluir varias periodicidades; por su parte, los nodos secundarios contienen únicamente información específica de una estructura periódica determinada o de los nodos secundarios de esa estructura periódica.  
  
|Tipo de nodo|Atributo|Tipo de valor|  
|---------------|---------------|----------------|  
|27 (Raíz ARIMA)|Interceptar<br /><br /> Periodicidad|11|  
|28 (Estructura periódica ARIMA)|periodicidad<br /><br /> Orden de regresión automática<br /><br /> orden de diferencia<br /><br /> Orden de media móvil|12<br /><br /> 13<br /><br /> 15<br /><br /> 14|  
|29 (Regresión automática ARIMA)|Coeficiente<br /><br /> (complemento de coeficiente)|7|  
|30 (Media móvil ARIMA)|Valor en t<br /><br /> Valor en t-1<br /><br /> …<br /><br /> Valor en t-n|7|  
  
 El valor del *orden de media móvil* indica el número de medias móviles de una serie. En general, la media móvil se calcula `n-1` veces si hay `n` términos en una serie, pero esta cantidad se puede reducir para facilitar el cálculo.  
  
 El valor del *orden de regresión automática* indica la cantidad de series de regresión automática.  
  
 El valor de *orden de diferencia* indica cuántas veces se comparan, o diferencian, las series.  
  
 Para obtener una lista de los tipos de valores posibles, vea <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>.  
  
### <a name="using-the-arima-tree-information"></a>Utilizar la información del árbol ARIMA  
 Si utiliza predicciones basadas en el algoritmo ARIMA en una solución empresarial, puede ser conveniente pegar la ecuación en un informe para mostrar el método utilizado para crear la predicción. Puede utilizar la leyenda para presentar las fórmulas en formato abreviado, o la descripción para presentar las fórmulas en formato largo.  
  
 Si va a desarrollar una aplicación que utiliza predicciones de serie temporal, puede que le resulte útil obtener la ecuación ARIMA del contenido del modelo y, a continuación, realizar sus propias predicciones. Para obtener la ecuación ARIMA correspondiente a cualquier resultado determinado, puede consultar directamente la raíz ARIMA de ese atributo concreto, como se muestra en los ejemplos anteriores.  
  
 Si conoce el identificador del nodo que contiene la serie que desea, dispone de dos opciones para recuperar los componentes de la ecuación:  
  
-   Formato de tabla anidada: utilice una consulta DMX o realice la consulta mediante el cliente de OLEDB.  
  
-   Representación XML: utilice una consulta XML.  
  
## <a name="remarks"></a>Comentarios  
 Puede resultar complicado recuperar información de un árbol ARTXP, porque la información correspondiente a cada división se encuentra en un lugar diferente dentro del árbol. Por consiguiente, con un modelo ARTXP, debe obtener todas las piezas y, a continuación, procesarlas de alguna forma para reconstituir la fórmula completa. Recuperar una ecuación a partir de un modelo ARIMA es más fácil, porque el árbol pone la fórmula a su disposición en distintos puntos. Para obtener información sobre cómo crear una consulta que recupere esta información, vea [Ejemplos de consultas de modelos de serie temporal](../../analysis-services/data-mining/time-series-model-query-examples.md).  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Ejemplos de consultas de modelo de serie temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
