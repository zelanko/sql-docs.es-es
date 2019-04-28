---
title: Para los modelos de clústeres de secuencia de contenido del modelo de minería de datos (Analysis Services - minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, sequence clustering models
- sequence clustering algorithms [Analysis Services]
ms.assetid: 68e1934a-e147-4d53-b122-fa15e3fd5485
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94224bbc5c254b01fab49c850b554427757b714b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733439"
---
# <a name="mining-model-content-for-sequence-clustering-models-analysis-services---data-mining"></a>Contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia(Analysis Services - Minería de datos)
  En este tema se describe el contenido del modelo de minería de datos específico de los modelos que utilizan el algoritmo de clústeres de secuencia de Microsoft. Para obtener una explicación de terminología general y de estadística relacionada con el contenido del modelo de minería de datos válida para todos los tipos de modelo, vea [Mining Model Content &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-sequence-clustering-model"></a>Descripción de la estructura de un modelo de agrupación en clústeres de secuencia  
 Un modelo de agrupación en clústeres de secuencia tiene un nodo primario único (NODE_TYPE = 1) que representa el modelo y sus metadatos. El nodo primario, que se etiqueta **(Todos)**, tiene un nodo de secuencia relacionado (NODE_TYPE = 13) que muestra todas las transiciones que se hayan detectado en los datos de entrenamiento.  
  
 ![Estructura del modelo de clústeres de secuencia](../media/modelcontent-seqclust.gif "estructura del modelo de clústeres de secuencia")  
  
 El algoritmo también crea varios clústeres, según las transiciones que se encontraran en los datos y cualquier otro atributo de entrada incluido al crear el modelo, como la información demográfica de los clientes o de otro tipo. Cada clúster (NODE_TYPE = 5) contiene su propio nodo de secuencia (NODE_TYPE = 13) que muestra únicamente las transiciones que se utilizaron para generar ese clúster concreto. A partir del nodo de secuencia, puede explorar en profundidad para ver los detalles de las transiciones de estados individuales (NODE_TYPE = 14).  
  
 Para obtener una explicación de las transiciones de estado y secuencia, con ejemplos, vea [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md).  
  
## <a name="model-content-for-a-sequence-clustering-model"></a>Contenido de un modelo de agrupación en clústeres de secuencia  
 En esta sección se proporciona información adicional sobre las columnas del contenido del modelo de minería de datos que tienen una relevancia especial para la agrupación en clústeres de secuencia.  
  
 MODEL_CATALOG  
 Nombre de la base de datos en la que se almacena el modelo.  
  
 MODEL_NAME  
 Nombre del modelo.  
  
 ATTRIBUTE_NAME  
 Siempre en blanco.  
  
 NODE_NAME  
 Nombre del nodo. Actualmente, el mismo valor que NODE_UNIQUE_NAME.  
  
 NODE_UNIQUE_NAME  
 Nombre único del nodo.  
  
 NODE_TYPE  
 Modelo de agrupación en clústeres de secuencia que genera los tipos de nodos siguientes:  
  
|Identificador del tipo de nodo|Descripción|  
|------------------|-----------------|  
|1 (Modelo)|Nodo raíz para el modelo|  
|5 (clúster)|Contiene un recuento de las transiciones del clúster, una lista de los atributos y estadísticas que describen los valores del clúster.|  
|13 (secuencia)|Contiene una lista de las transiciones incluidas en el clúster.|  
|14 (transición)|Describe una secuencia de eventos en forma de tabla en la que la primera fila contiene el estado inicial y todas las demás filas contienen los estados sucesivos, junto con estadísticas de probabilidad y compatibilidad.|  
  
 NODE_GUID  
 : en blanco.  
  
 NODE_CAPTION  
 Etiqueta o título asociado al nodo para la presentación.  
  
 Puede cambiar el nombre de los títulos del clúster mientras está utilizando el modelo; sin embargo, si cierra el modelo, el nombre nuevo no se conserva.  
  
 CHILDREN_CARDINALITY  
 Cálculo del número de elementos secundarios que tiene el nodo.  
  
 **Raíz del modelo** : el valor de la cardinalidad es igual al número de clústeres más uno. Para obtener más información, vea [Cardinalidad](#bkmk_cardinality).  
  
 **Nodos de clúster** : la cardinalidad siempre es 1, porque cada clúster tiene un único nodo secundario, que contiene la lista de secuencias en el clúster.  
  
 **Nodos de secuencia** : la cardinalidad indica el número de transiciones que están incluidas en ese clúster. Por ejemplo, la cardinalidad del nodo de secuencia para la raíz del modelo indica cuántas transiciones se encontraron en todo el modelo.  
  
 PARENT_UNIQUE_NAME  
 Nombre único del nodo primario del nodo.  
  
 Se devuelve NULL para todos los nodos del nivel raíz.  
  
 NODE_DESCRIPTION  
 Igual que el título del nodo.  
  
 NODE_RULE  
 Siempre en blanco.  
  
 MARGINAL_RULE  
 Siempre en blanco.  
  
 NODE_PROBABILITY  
 **Raíz del modelo** Siempre es 0.  
  
 **Nodos de clúster** : la probabilidad ajustada del clúster en el modelo. Las probabilidades ajustadas no suman 1, porque el método de agrupación en clústeres utilizado en la agrupación en clústeres de secuencia permite la pertenencia parcial en varios clústeres.  
  
 **Nodos de secuencia** : siempre es 0.  
  
 **Nodos de transición** : siempre es 0.  
  
 MARGINAL_PROBABILITY  
 **Raíz del modelo** Siempre es 0.  
  
 **Nodos de clúster** El mismo valor que NODE_PROBABILITY.  
  
 **Nodos de secuencia** : siempre es 0.  
  
 **Nodos de transición** : siempre es 0.  
  
 NODE_DISTRIBUTION  
 Tabla que contiene probabilidades y otra información. Para más información, vea [Tabla NODE_DISTRIBUTION](#bkmk_NODEDIST).  
  
 NODE_SUPPORT  
 Número de transiciones que admiten este nodo. Por consiguiente, si hay 30 ejemplos de secuencia "Producto A seguido de producto B" en los datos de entrenamiento, la compatibilidad total es 30.  
  
 **Modelo raíz** : número total de transiciones en el modelo.  
  
 **Nodos de clústeres** : compatibilidad neta para el clúster, que indica el número de casos de entrenamiento que contribuyen a los casos para este clúster.  
  
 **Nodos de secuencia** : siempre es 0.  
  
 **Nodos de transición** : porcentaje de casos en el clúster que representan una transición concreta. Puede ser 0 o un valor positivo. Se calcula tomando la compatibilidad neta para el nodo del clúster y multiplicándola por la probabilidad del clúster.  
  
 A partir de este valor, puede indicar cuántos casos de entrenamiento contribuyeron a la transición.  
  
 MSOLAP_MODEL_COLUMN  
 No aplicable.  
  
 MSOLAP_NODE_SCORE  
 No aplicable.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Igual que NODE_DESCRIPTION.  
  
## <a name="understanding-sequences-states-and-transitions"></a>Descripción de las secuencias, estados y transiciones  
 Un modelo de agrupación en clústeres de secuencia tiene una estructura única que combina dos tipos de objetos con clases muy diferentes de información: el primer tipo de objeto es el clúster y el segundo es la transición de estado.  
  
 Los clústeres creados mediante agrupación en clústeres de secuencia se parecen a los creados mediante el algoritmo de clústeres de Microsoft. Cada clúster tiene un perfil y características. Sin embargo, en la agrupación en clústeres de secuencia, cada clúster contiene además un nodo secundario único que muestra las secuencias en ese clúster. Cada nodo de secuencia contiene varios nodos secundarios que describen en detalle las transiciones de estado, con probabilidades.  
  
 Casi siempre hay más secuencias en el modelo de lo que puede encontrar en un único caso, porque las secuencias se pueden encadenar. Microsoft Analysis Services almacena los punteros de un estado al otro para que se pueda contar el número de veces que cada transición se produce. También puede encontrar información de cuántas veces se produjo la secuencia y cuantificar la probabilidad de producirse en comparación con el conjunto completo de estados observados.  
  
 La tabla siguiente resume cómo se almacena la información en el modelo y cómo se relacionan los nodos.  
  
|Nodo|Tiene nodo secundario|Tabla NODE_DISTRIBUTION|  
|----------|--------------------|------------------------------|  
|Raíz del modelo|Varios nodos de clúster<br /><br /> Nodo con secuencias para el modelo completo|Muestra todos los productos en el modelo, con la compatibilidad y probabilidad.<br /><br /> Dado que el método de agrupación en clústeres permite la pertenencia parcial en varios clústeres, la compatibilidad y probabilidad pueden tener valores fraccionarios. Es decir, en lugar de contar una vez un único caso, cada caso puede pertenecer potencialmente a varios clústeres. Por consiguiente, cuando se determina la última pertenencia al clúster, el valor se ajusta con la probabilidad de ese clúster.|  
|Nodo de secuencia para el modelo|Varios nodos de transición|Muestra todos los productos en el modelo, con la compatibilidad y probabilidad.<br /><br /> Dado que el número de secuencias se conoce por el modelo, en este nivel, los cálculos para la compatibilidad y la probabilidad son sencillos:<br /><br /> Compatibilidad = recuento de casos<br /><br /> Probabilidad = probabilidad neta de cada secuencia del modelo. Todo las probabilidades deberían sumar 1.|  
|Nodos de clúster individuales|Nodo con secuencias para ese clúster únicamente|Muestra todos los productos de un clúster, pero proporciona los valores de compatibilidad y probabilidad únicamente para los productos que son característicos del clúster.<br /><br /> La compatibilidad representa el valor de compatibilidad ajustada para cada caso en este clúster. Los valores de probabilidad son ajustados.|  
|Nodos de secuencia para clústeres individuales|Varios nodos con transiciones para las secuencias en ese clúster únicamente|Exactamente la misma información que en los nodos de clúster individuales.|  
|Transiciones|Ningún nodo secundario|Muestra las transiciones para el primer estado relacionado.<br /><br /> La compatibilidad un valor ajustado, que indica los casos que toman parte en cada transición. La probabilidad es la probabilidad ajustada, representada como un porcentaje.|  
  
###  <a name="bkmk_NODEDIST"></a> Tabla NODE_DISTRIBUTION  
 En la tabla NODE_DISTRIBUTION se proporciona información detallada de la compatibilidad y la probabilidad de las transiciones y secuencias de un clúster concreto.  
  
 Una fila siempre se agrega a la tabla de transiciones para representar los posibles valores `Missing`. Para obtener información acerca de lo que el `Missing` valor medio, y cómo afecta a los cálculos, vea [los valores que faltan &#40;Analysis Services - minería de datos&#41;](missing-values-analysis-services-data-mining.md).  
  
 Los cálculos de compatibilidad y probabilidad difieren en función de si el cálculo se aplica a los casos de entrenamiento o al modelo terminado. Esto se debe a que el método de agrupación en clústeres predeterminado, maximización de la expectativa (EM), supone que cualquier caso puede pertenecer a más de un clúster. Al calcular la compatibilidad para los casos en el modelo, es posible utilizar recuentos netos y probabilidades netas. Sin embargo, las probabilidades de una secuencia determinada en un clúster deben ser compensadas por la suma de todas las combinaciones posibles de clústeres y secuencias.  
  
###  <a name="bkmk_cardinality"></a> Cardinalidad  
 En un modelo de agrupación en clústeres, la cardinalidad del nodo primario generalmente indica cuántos clústeres contiene el modelo. Sin embargo, un modelo de agrupación en clústeres de secuencia tiene dos tipos de nodos en el nivel de clúster: un tipo de nodo contiene los clústeres y el otro contiene una lista de secuencias para el modelo como un todo.  
  
 Por consiguiente, para obtener información sobre el número de clústeres del modelo, puede tomar el valor de NODE_CARDINALITY para el nodo (Todos) y restar uno. Por ejemplo, si el modelo creara 9 clústeres, la cardinalidad de la raíz del modelo sería de 10. Esto es porque el modelo contiene 9 nodos de clúster, cada uno con su propio nodo de secuencia, más un nodo de secuencia adicional denominado clúster 10, que representa las secuencias para el modelo.  
  
## <a name="walkthrough-of-structure"></a>Tutorial de la estructura  
 Un ejemplo podría ayudar a clarificar cómo se almacena la información y cómo puede interpretarse. Por ejemplo, puede encontrar el pedido mayor, es decir, la cadena más larga observada en los datos de [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] subyacentes mediante la consulta siguiente:  
  
```  
USE AdventureWorksDW2012  
SELECT DISTINCT OrderNumber, Count(*)  
FROM vAssocSeqLineItems  
GROUP BY OrderNumber  
ORDER BY Count(*) DESC  
```  
  
 En estos resultados, observa que los números de pedido 'SO72656', 'SO58845' y 'SO70714' contienen las secuencias más grandes, con ocho elementos cada una. Mediante los identificadores de pedido puede ver los detalles de un pedido determinado para comprobar qué artículos se compraron y en qué orden.  
  
|OrderNumber|LineNumber|Modelo|  
|-----------------|----------------|-----------|  
|SO58845|1|Mountain-500|  
|SO58845|2|LL Mountain Tire|  
|SO58845|3|Mountain Tire Tube|  
|SO58845|4|Fender Set - Mountain|  
|SO58845|5|Mountain Bottle Cage|  
|SO58845|6|Water Bottle|  
|SO58845|7|Sport-100|  
|SO58845|8|Long-Sleeve Logo Jersey|  
  
 Sin embargo, algunos clientes que compran el producto Mountain-500 podrían comprar productos diferentes. Puede ver todos los productos que siguen a Mountain-500 en la lista de secuencias del modelo. Los procedimientos siguientes le permiten ver estas secuencias utilizando los dos visores que se proporcionan en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
#### <a name="to-view-related-sequences-by-using-the-sequence-clustering-viewer"></a>Para ver las secuencias relacionadas con el visor de agrupaciones en clústeres de secuencia  
  
1.  En el Explorador de objetos, haga clic con el botón secundario en el modelo [Clústeres de secuencia] y, a continuación, haga clic en Examinar.  
  
2.  En el visor de agrupaciones en clústeres de secuencia, haga clic en la pestaña **Transiciones de estado** .  
  
3.  En la lista desplegable **Clúster** , asegúrese de que esté seleccionada la opción **Población (Todo)** .  
  
4.  Mueva completamente la barra deslizante a la izquierda del panel hasta la parte superior para mostrar todos los vínculos.  
  
5.  En el diagrama, busque **Mountain-500**y haga clic en el nodo en el diagrama.  
  
6.  Las líneas resaltadas señalan a los estados siguientes (los productos que se compraron después de Mountain-500) y los números indican la probabilidad. Compare con los resultados del visor de contenido de modelo genérico.  
  
#### <a name="to-view-related-sequences-by-using-the-generic-model-content-viewer"></a>Para ver las secuencias relacionadas utilizando el visor de contenido de modelo genérico  
  
1.  En el Explorador de objetos, haga clic con el botón secundario en el modelo [Clústeres de secuencia] y, a continuación, haga clic en Examinar.  
  
2.  En la lista desplegable del visor, seleccione **Visor de árbol de contenido genérico de Microsoft**.  
  
3.  En el panel **Título de nodo** , haga clic el nodo denominado **Nivel de secuencia para el clúster 16**.  
  
4.  En el panel de detalles Nodo, busque la fila NODE_DISTRIBUTION y haga clic en cualquier parte en la tabla anidada.  
  
     La fila superior siempre es para el valor Missing. Esta fila es el estado 0 de la secuencia.  
  
5.  Presione la tecla de flecha hacia abajo o utilice las barras de desplazamiento para moverse hacia abajo a través de la tabla anidada hasta que vea la fila Mountain-500.  
  
     Esta fila es el estado 20 de la secuencia.  
  
    > [!NOTE]  
    >  Puede obtener mediante programación el número de fila para un estado de secuencia determinado, pero si únicamente está examinando, podría ser más fácil copiar simplemente la tabla anidada en un libro de Excel.  
  
6.  Vuelva al panel Título de nodo y expanda el nodo **Nivel de secuencia para el clúster 16**, si aún no está expandido.  
  
7.  Busque entre sus nodos secundarios **Fila de transición para el estado de secuencia 20.** Haga clic en el nodo de transición.  
  
8.  La tabla NODE_DISTRIBUTION anidada contiene los productos y probabilidades siguientes. Compárelos con los resultados de la pestaña **Transiciones de estado** del visor de agrupaciones en clústeres de secuencia.  
  
 En la tabla siguiente se muestran los resultados de la tabla NODE_DISTRIBUTION, junto con los valores de probabilidad redondeados que se muestran en el visor gráfico.  
  
|Producto|Compatibilidad (tabla NODE_DISTRIBUTION)|Probabilidad (tabla NODE_DISTRIBUTION))|Probabilidad (del gráfico)|  
|-------------|------------------------------------------|------------------------------------------------|--------------------------------|  
|Missing|48.447887|0.138028169|(no se muestra)|  
|Cycling Cap|10.876056|0.030985915|0.03|  
|Fender Set - Mountain|80.087324|0.228169014|0.23|  
|Half-Finger Gloves|0.9887324|0.002816901|0.00|  
|Hydration Pack|0.9887324|0.002816901|0.00|  
|LL Mountain Tire|51.414085|0.146478873|0.15|  
|Long-Sleeve Logo Jersey|2.9661972|0.008450704|0.01|  
|Mountain Bottle Cage|87.997183|0.250704225|0.25|  
|Mountain Tire Tube|16.808451|0.047887324|0.05|  
|Short-Sleeve Classic Jersey|10.876056|0.030985915|0.03|  
|Sport-100|20.76338|0.05915493|0.06|  
|Water Bottle|18.785915|0.053521127|0.25|  
  
 Aunque el caso que seleccionamos inicialmente en los datos de entrenamiento contenía el producto 'Mountain-500' seguido de 'LL Mountain Tire', puede ver que hay muchas otras secuencias posibles. Para buscar información detallada de un clúster en especial, debe repetir el proceso de explorar en profundidad en la lista de secuencias del clúster hasta las transiciones reales de cada estado o producto.  
  
 Puede saltar de la secuencia enumerada en un clúster determinado a la fila de transición. Con esa fila de transición puede determinar qué producto es el siguiente y volver a ese producto en la lista de secuencias. Repitiendo este proceso para cada primer y segundo estados, puede trabajar con cadenas de estados largas.  
  
## <a name="using-sequence-information"></a>Usar la información de la secuencia  
 Un escenario común para la agrupación en clústeres de secuencia es realizar el seguimiento de los clics del usuario en un sitio web. Por ejemplo, si los datos provinieran de registros de compras del cliente del sitio web de comercio electrónico de Adventure Works, el modelo de agrupación en clústeres de secuencia resultante se podría utilizar para deducir el comportamiento del usuario, rediseñar el sitio de comercio electrónico para resolver los problemas de navegación o promocionar las ventas.  
  
 Por ejemplo, el análisis podría mostrar que los usuarios siempre siguen una cadena determinada de productos, sin tener en cuenta la información demográfica. Además, podría encontrar que los usuarios frecuentemente salen del sitio después de hacer clic en un producto concreto. Dado este descubrimiento, podría preguntarse qué rutas de acceso adicionales podría proporcionar a los usuarios que les inducirían a quedarse en el sitio web.  
  
 Si no tiene información adicional que pueda utilizar para clasificar a sus usuarios, simplemente puede utilizar la información de la secuencia para recopilar datos sobre la navegación y entender mejor el comportamiento global. Sin embargo, si puede recopilar información sobre los clientes y hacer corresponder esa información con la base de datos de clientes, puede combinar la eficacia de la agrupación en clústeres con la predicción de secuencias con el fin de proporcionar recomendaciones personalizadas para el usuario o quizás basadas en la ruta de acceso de navegación en la página actual.  
  
 Otro uso de la completa información de estado y transiciones que compila un modelo de agrupación en clústeres de secuencia es determinar qué posibles rutas de acceso no se usan nunca. Por ejemplo, si muchos visitantes que van a las páginas 1 a 4, pero nunca continúan hacia la página 5, podría investigar si hay problemas que impiden la navegación a dicha página. Puede hacer esto consultando el contenido del modelo y comparándolo con una lista de posibles rutas de acceso.  Se pueden crear gráficos que le indiquen todas las rutas de navegación de un sitio web mediante programación o utilizando diversas herramientas de análisis de sitios.  
  
 Para conocer cómo obtener la lista de rutas de acceso observadas consultando el contenido del modelo y ver otros ejemplos de consultas en un modelo de agrupación en clústeres de secuencia, vea [Ejemplos de consultas de modelos de clústeres de secuencia](clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)   
 [Ejemplos de consultas de modelos de clústeres de secuencia](clustering-model-query-examples.md)  
  
  
