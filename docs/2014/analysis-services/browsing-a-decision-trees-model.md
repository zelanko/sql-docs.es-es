---
title: Modelo de árboles de decisión de exploración | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- tree viewer
- mining model, decision tree
- decision tree [data mining]
- dependency network
ms.assetid: 6b3dd1ae-caff-41c3-817b-802dc020ff88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 257d193c84420a0c70ea99ef2a8cadfa9e11eec5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52525560"
---
# <a name="browsing-a-decision-trees-model"></a>Examinar un modelo de árboles de decisión
  Al abrir un modelo de clasificación con **examinar**, el modelo se muestra en un visor de árbol de decisión interactivo, similar a la [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de árboles de decisión de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El visor muestra los resultados de clasificación en forma de gráfico, que se ha diseñado para resaltar los criterios que distinguen un grupo de datos de otro. También puede explorar en profundidad los subconjuntos individuales del árbol y recuperar los datos subyacentes.  
  
##  <a name="bkmk_Top"></a> Explorar el modelo  
 Los modelos basados en el algoritmo de árboles de decisión tienen gran cantidad de información interesante que se puede explorar. El **examinar** ventana incluye las siguientes fichas y paneles que le ayudarán a aprender los patrones y predecir resultados mediante el gráfico:  
  
-   [Árbol de decisión](#BKMK_DecisionTree)  
  
-   [Red de dependencias](#BKMK_DNetwork)  
  
 Para experimentar con árboles de decisión, puede utilizar los datos de ejemplo en la pestaña Datos de aprendizaje (o Datos de origen) del libro de datos de ejemplo y generar un modelo de árbol de decisión con Bike Buyer como atributo de predicción.  
  
###  <a name="BKMK_DecisionTree"></a> Árbol de decisión  
 Esta vista se ha diseñado para ayudarle a conocer y explorar los factores que generan resultados.  
  
 El gráfico de árboles de decisión se puede leer de izquierda a derecha como sigue:  
  
-   Los rectángulos, que se conocen como *nodos*, contienen subconjuntos de los datos. La etiqueta del nodo indica las características de definición de ese subconjunto.  
  
-   El nodo más a la izquierda, con la etiqueta **todas**, representa el conjunto de datos completo. Todos los nodos siguientes representan subconjuntos de los datos.  
  
-   Un árbol de decisión contiene muchas *divide*, o en lugares donde los datos divergen en varios conjuntos basados en atributos.  
  
     Por ejemplo, la primera división en el modelo de ejemplo divide el conjunto de datos en tres grupos de edad.  
  
-   La división inmediatamente después de la **todas** nodo es más importante porque muestra la condición principal que divide este conjunto de datos.  
  
     Las divisiones adicionales se muestran a la derecha. Por tanto, cuando se analizan diferentes segmentos del árbol, podrá saber qué atributos tuvieron mayor influencia en el comportamiento de compra.  
  
 ![Gráfico de red de dependencias de un modelo de asociación](media/dm13-dec-tree-split-definition.gif "gráfico de red de dependencias de un modelo de asociación")  
  
 Con esta información, puede dirigir una campaña de marketing hacia aquellos clientes que puedan necesitar simplemente el estímulo para realizar una compra.  
  
##### <a name="explore-the-decision-tree"></a>Explorar el árbol de decisión  
  
1.  Haga clic en el **todas** nodo y mire la **leyenda de minería de datos**.  
  
     Muestra el recuento exacto de casos en el conjunto de datos de aprendizaje, así como un análisis desglosado de los resultados.  
  
     Puede ver los mismos detalles en la información sobre herramientas si sitúa el mouse sobre un nodo.  
  
2.  Haga clic en los signo más y menos junto a cada nodo para expandir o contraer del árbol.  
  
     También puede usar el **Mostrar nivel** control deslizante para expandir o contraer el árbol.  
  
3.  Se habrá dado cuenta de que algunos nodos son más oscuros que otros.  
  
     De forma predeterminada, **rellenado** se utiliza como la variable de sombreado, lo que significa que la intensidad del color muestra qué nodos tienen más soporte técnico.  
  
     Por consiguiente el nodo en el extremo izquierdo es el más oscuro porque contiene el conjunto de datos completo.  
  
4.  Cambie el valor de **en segundo plano** desde **todos los casos** a **Sí**.  
  
     ![gráfico de árboles de decisión cambiantes para resaltar los compradores](media/dm13-dectreeshadedbuyer.gif "cambiar el gráfico de árboles de decisión para resaltar los compradores")  
  
5.  Ahora la intensidad de color indica cuántos clientes en cada nodo compraron una bicicleta, que es el comportamiento que le interesa.  
  
     Observe las barras coloreadas en cada nodo. Es un histograma que muestra la distribución de los resultados en este subconjunto de datos. Por ejemplo, en el árbol de decisión Bike Buyer de ejemplo, la barra coloreada muestra la proporción de los clientes que compraron bicicletas (valores en Sí) frente a los que no lo hicieron (sin valores). Para obtener los valores exactos, puede hacer clic en el nodo y ver el **leyenda de minería de datos**.  
  
6.  Si observa el gráfico, podrá ver cómo cada subconjunto de datos se va descomponiendo en grupos más pequeños y los atributos que se usan con mayor frecuencia en la predicción de resultados.  
  
     Basta con ver la intensidad del sombreado para centrarse en los grupos que le interesan y obtener información más detallada para compararlos. Por ejemplo, estos grupos muestran bastantes posibilidades de comprar bicicletas:  
  
    -   Edad > = 32 y \< ingresos anuales y 53 > = 26 000 e hijos = 0  
  
         Total de casos: 1150  
  
         Probabilidad de ser comprador de bicicletas: 18%  
  
    -   Edad > = 32 y \< ingresos anuales y 53 > = 26 000 e hijos no = 0 y estado civil = 'Single'  
  
         Total de casos: 402  
  
         Probabilidad de ser comprador de bicicletas: 16%  
  
7.  Cambie el valor de **en segundo plano** desde **Sí** a **No** y ver cómo cambia el gráfico.  
  
     ![Gráfico de red de dependencias de un modelo de asociación](media/dm13-dec-tree-background-no.gif "gráfico de red de dependencias de un modelo de asociación")  
  
 **Sugerencias**  
  
-   Si los datos se pueden dividir en varias series, se crea otro modelo para cada conjunto de datos que desee modelar.  
  
-   En el modelo de datos de ejemplo, hay solo un resultado de predicción: Bike Buyer - pero imaginemos que tiene información sobre si el cliente compra un plan de servicio y desea predecir también eso. En ese caso tendría esos datos en una columna independiente e incluiría dos atributos de predicción en el modelo.  
  
     Haga clic en el **histograma** opción, en la esquina superior izquierda del panel de árbol de decisión, para cambiar el número máximo de Estados que pueden aparecer en los histogramas del árbol. Esto resulta útil si el atributo de predicción tiene muchos estados. Los estados aparecen en una histograma en orden de popularidad de izquierda a derecha.  
  
-   También puede utilizar las opciones de la **árbol de decisión** tab para afectar a cómo se muestra el árbol, acercar o alejar o cambiar el tamaño del gráfico a la ventana.  
  
-   Use **Expansión predeterminada** para configurar el número predeterminado de niveles que van a aparecer en todos los árboles del modelo.  
  
-   Seleccione **Mostrar nombre largo** para mostrar el nombre completo del atributo, incluido el origen de datos. Los nombres cortos y largos son los mismos, a menos que los casos se hayan obtenido de un origen de datos distinto al de los atributos de cada caso.  
  
 [Volver al principio](#bkmk_Top)  
  
###  <a name="BKMK_DNetwork"></a> Red de dependencias  
 El **red de dependencias** vista muestra las conexiones entre los atributos de entrada y los atributos de predicción del modelo.  
  
1.  Haga clic en el control deslizante y arrástrelo a la izquierda del visor  
  
     En la parte superior, se muestran todas las conexiones. Cuando desplace el control deslizante hacia abajo, solamente se muestran en el visor los vínculos de mayor importancia.  
  
2.  Ahora haga clic en el nodo Bike Buyer.  
  
     ![Vista de dependencia de red para los árboles de decisión](media/dm13-dectree-depnet.gif "vista de dependencia de red para los árboles de decisión")  
  
     Cuando se selecciona un nodo, el visor resalta las dependencias específicas de dicho nodo. En este caso, el visor resalta cada nodo que le ayude a predecir el resultado.  
  
3.  Si el Visor contiene muchos nodos, puede buscar nodos específicos mediante el **buscar nodo** botón. Al hacer clic en **Buscar nodo** se abre el cuadro de diálogo **Buscar nodo** , en el que puede utilizar un filtro para buscar y seleccionar nodos específicos.  
  
4.  La leyenda de la parte inferior del visor vincula códigos de color con el tipo de dependencia en el gráfico. Por ejemplo, cuando selecciona un nodo de predicción, este nodo se sombrea en color turquesa y los nodos que predicen el nodo seleccionado aparecen sombreados en color naranja.  
  
 [Volver al principio](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>Obtener información detallada en datos subyacentes  
 Varios tipos de modelos admiten la capacidad *obtención de detalles* del modelo a los datos del caso subyacentes. Esto puede resultar muy útil para ponerse en contacto con los clientes de un sector determinado o para obtener los datos necesarios para realizar un análisis más profundo.  
  
##### <a name="get-case-data"></a>Obtener datos de un caso  
  
1.  Haga clic con el botón secundario del mouse en el nodo del árbol que contiene los datos deseados y seleccione una de estas opciones:  
  
    -   **Obtener detalles del modelo**. Esta opción obtiene los casos que pertenecen al nodo seleccionado y los guarda en una tabla de Excel. Obtendrá solamente las columnas de los datos que se usaron realmente en la generación del modelo.  
  
    -   **Obtención de detalles de las columnas de estructura**. Esta opción obtiene los casos que pertenecen al nodo seleccionado y los guarda en una tabla de Excel. Obtenga toda la información que estaba disponible en la base de datos cuando se crearon, incluso de una columna no se usaron en el modelo. Por ejemplo, puede haber excluido la dirección del cliente y código postal porque esos campos no resultan útiles con el análisis, pero los ha dejado en la estructura.  
  
     Vuelva a Excel para ver los datos. El visor Examinar ejecuta una consulta, guarda los datos en una hoja de cálculo nueva y etiqueta los resultados.  
  
     ![los resultados de obtención de detalles se guardan en Excel](media/dm13-dectree-drillthroughresults.gif "los resultados de obtención de detalles se guardan en Excel")  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
