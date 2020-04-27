---
title: Examinar un modelo de árboles de decisión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 17b3a2765781813c832b0b654e4a02475b3ab623
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064668"
---
# <a name="browsing-a-decision-trees-model"></a>Examinar un modelo de árboles de decisión
  Al abrir un modelo de clasificación con **examinar**, el modelo se muestra en un visor de árbol de decisión interactivo, similar [!INCLUDE[msCoName](../includes/msconame-md.md)] al visor de árboles [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]de decisión de. El visor muestra los resultados de clasificación en forma de gráfico, que se ha diseñado para resaltar los criterios que distinguen un grupo de datos de otro. También puede explorar en profundidad los subconjuntos individuales del árbol y recuperar los datos subyacentes.  
  
##  <a name="explore-the-model"></a><a name="bkmk_Top"></a>Explorar el modelo  
 Los modelos basados en el algoritmo de árboles de decisión tienen gran cantidad de información interesante que se puede explorar. La ventana **examinar** incluye las pestañas y los paneles siguientes para ayudarle a conocer los patrones y predecir los resultados con el gráfico:  
  
-   [Árbol de decisión](#BKMK_DecisionTree)  
  
-   [Red de dependencias](#BKMK_DNetwork)  
  
 Para experimentar con árboles de decisión, puede utilizar los datos de ejemplo en la pestaña Datos de aprendizaje (o Datos de origen) del libro de datos de ejemplo y generar un modelo de árbol de decisión con Bike Buyer como atributo de predicción.  
  
###  <a name="decision-tree"></a><a name="BKMK_DecisionTree"></a>Árbol de decisión  
 Esta vista se ha diseñado para ayudarle a conocer y explorar los factores que generan resultados.  
  
 El gráfico de árboles de decisión se puede leer de izquierda a derecha como sigue:  
  
-   Los rectángulos, que se conocen como *nodos*, contienen subconjuntos de los datos. La etiqueta del nodo indica las características de definición de ese subconjunto.  
  
-   El nodo situado más a la izquierda, con la etiqueta **todo**, representa el conjunto de datos completo. Todos los nodos siguientes representan subconjuntos de los datos.  
  
-   Un árbol de decisión contiene muchas *divisiones*o lugares en los que los datos difieren en varios conjuntos basados en atributos.  
  
     Por ejemplo, la primera división en el modelo de ejemplo divide el conjunto de datos en tres grupos de edad.  
  
-   La división inmediatamente después del nodo **todos** es la más importante porque muestra la condición primaria que divide este conjunto de filas.  
  
     Las divisiones adicionales se muestran a la derecha. Por tanto, cuando se analizan diferentes segmentos del árbol, podrá saber qué atributos tuvieron mayor influencia en el comportamiento de compra.  
  
 ![Gráfico de redes de dependencias para un modelo de asociación](media/dm13-dec-tree-split-definition.gif "Gráfico de redes de dependencias para un modelo de asociación")  
  
 Con esta información, puede dirigir una campaña de marketing hacia aquellos clientes que puedan necesitar simplemente el estímulo para realizar una compra.  
  
##### <a name="explore-the-decision-tree"></a>Explorar el árbol de decisión  
  
1.  Haga clic en el nodo **todos** y examine la **leyenda de minería de datos**.  
  
     Muestra el recuento exacto de casos en el conjunto de datos de aprendizaje, así como un análisis desglosado de los resultados.  
  
     Puede ver los mismos detalles en la información sobre herramientas si sitúa el mouse sobre un nodo.  
  
2.  Haga clic en los signo más y menos junto a cada nodo para expandir o contraer del árbol.  
  
     También puede usar el control deslizante **Mostrar nivel** para expandir o reducir el árbol.  
  
3.  Se habrá dado cuenta de que algunos nodos son más oscuros que otros.  
  
     De forma predeterminada, el **rellenado** se usa como variable de sombreado, lo que significa que la intensidad del color muestra qué nodos tienen la mayor compatibilidad.  
  
     Por consiguiente el nodo en el extremo izquierdo es el más oscuro porque contiene el conjunto de datos completo.  
  
4.  Cambie el valor de **fondo** de **todos los casos** a **sí**.  
  
     ![cambiar el gráfico de árboles de decisión para resaltar los compradores](media/dm13-dectreeshadedbuyer.gif "cambiar el gráfico de árboles de decisión para resaltar los compradores")  
  
5.  Ahora la intensidad de color indica cuántos clientes en cada nodo compraron una bicicleta, que es el comportamiento que le interesa.  
  
     Observe las barras coloreadas en cada nodo. Es un histograma que muestra la distribución de los resultados en este subconjunto de datos. Por ejemplo, en el árbol de decisión Bike Buyer de ejemplo, la barra coloreada muestra la proporción de clientes que compraron bicicletas (sí valores) frente a aquellos que no lo hicieron (ningún valor). Para obtener los valores exactos, puede hacer clic en el nodo y ver la **leyenda de minería de datos**.  
  
6.  Si observa el gráfico, podrá ver cómo cada subconjunto de datos se va descomponiendo en grupos más pequeños y los atributos que se usan con mayor frecuencia en la predicción de resultados.  
  
     Basta con ver la intensidad del sombreado para centrarse en los grupos que le interesan y obtener información más detallada para compararlos. Por ejemplo, estos grupos muestran bastantes posibilidades de comprar bicicletas:  
  
    -   Age >= 32 y \< 53 e ingresos anuales >= 26000 e hijos = 0  
  
         Total de casos: 1150  
  
         Probabilidad de comprador de bicicletas: 18%  
  
    -   Age >= 32 y \< 53 y yearly income >= 26000 y Children not = 0 and civil status = ' single '  
  
         Total de casos: 402  
  
         Probabilidad de ser comprador de bicicletas: 16 %  
  
7.  Cambie el valor de **background** de **sí** a **no** y vea cómo cambia el gráfico.  
  
     ![Gráfico de redes de dependencias para un modelo de asociación](media/dm13-dec-tree-background-no.gif "Gráfico de redes de dependencias para un modelo de asociación")  
  
 **Sugerencias**  
  
-   Si los datos se pueden dividir en varias series, se crea otro modelo para cada conjunto de datos que desee modelar.  
  
-   En el modelo de datos de ejemplo, solo hay un resultado predecible, Bike Buyer, pero Supongamos que tiene información sobre si el cliente ha adquirido un plan de servicio y desea predecirlo también. En ese caso tendría esos datos en una columna independiente e incluiría dos atributos de predicción en el modelo.  
  
     Haga clic en la opción **histograma** , en la esquina superior izquierda del panel del árbol de decisión, para cambiar el número máximo de Estados que pueden aparecer en los histogramas del árbol. Esto resulta útil si el atributo de predicción tiene muchos estados. Los estados aparecen en una histograma en orden de popularidad de izquierda a derecha.  
  
-   También puede usar las opciones de la pestaña **árbol de decisión** para influir en el modo en que se muestra el árbol, al acercar o alejar, o al ajustar el tamaño del gráfico para que se ajuste a la ventana.  
  
-   Use **Expansión predeterminada** para configurar el número predeterminado de niveles que van a aparecer en todos los árboles del modelo.  
  
-   Seleccione **Mostrar nombre largo** para mostrar el nombre completo del atributo, incluido el origen de datos. Los nombres cortos y largos son los mismos, a menos que los casos se hayan obtenido de un origen de datos distinto al de los atributos de cada caso.  
  
 [Volver al principio](#bkmk_Top)  
  
###  <a name="dependency-network"></a><a name="BKMK_DNetwork"></a>Red de dependencias  
 La vista **red de dependencias** muestra las conexiones entre los atributos de entrada y los atributos de predicción del modelo.  
  
1.  Haga clic en el control deslizante y arrástrelo a la izquierda del visor  
  
     En la parte superior, se muestran todas las conexiones. Cuando desplace el control deslizante hacia abajo, solamente se muestran en el visor los vínculos de mayor importancia.  
  
2.  Ahora haga clic en el nodo Bike Buyer.  
  
     ![Vista de red de dependencia de árboles de decisión](media/dm13-dectree-depnet.gif "Vista de red de dependencia de árboles de decisión")  
  
     Cuando se selecciona un nodo, el visor resalta las dependencias específicas de dicho nodo. En este caso, el visor resalta cada nodo que le ayude a predecir el resultado.  
  
3.  Si el visor contiene muchos nodos, puede buscar nodos específicos mediante el botón **Buscar nodo** . Al hacer clic en **Buscar nodo** se abre el cuadro de diálogo **Buscar nodo** , en el que puede utilizar un filtro para buscar y seleccionar nodos específicos.  
  
4.  La leyenda de la parte inferior del visor vincula códigos de color con el tipo de dependencia en el gráfico. Por ejemplo, cuando selecciona un nodo de predicción, este nodo se sombrea en color turquesa y los nodos que predicen el nodo seleccionado aparecen sombreados en color naranja.  
  
 [Volver al principio](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>Obtener información detallada en datos subyacentes  
 Varios tipos de modelos admiten la capacidad de obtener *detalles* del modelo en los datos de casos subyacentes. Esto puede resultar muy útil para ponerse en contacto con los clientes de un sector determinado o para obtener los datos necesarios para realizar un análisis más profundo.  
  
##### <a name="get-case-data"></a>Obtener datos de un caso  
  
1.  Haga clic con el botón secundario del mouse en el nodo del árbol que contiene los datos deseados y seleccione una de estas opciones:  
  
    -   **Obtención de detalles del modelo**. Esta opción obtiene los casos que pertenecen al nodo seleccionado y los guarda en una tabla de Excel. Obtendrá solamente las columnas de los datos que se usaron realmente en la generación del modelo.  
  
    -   Obtener **detalles de las columnas**de la estructura. Esta opción obtiene los casos que pertenecen al nodo seleccionado y los guarda en una tabla de Excel. Obtiene toda la información que estaba disponible en los datos subyacentes cuando se compiló, incluso una columna no se utilizó en el modelo. Por ejemplo, puede haber excluido la dirección del cliente y código postal porque esos campos no resultan útiles con el análisis, pero los ha dejado en la estructura.  
  
     Vuelva a Excel para ver los datos. El visor Examinar ejecuta una consulta, guarda los datos en una hoja de cálculo nueva y etiqueta los resultados.  
  
     ![los resultados de la obtención de detalles se guardan en Excel](media/dm13-dectree-drillthroughresults.gif "los resultados de la obtención de detalles se guardan en Excel")  
  
## <a name="see-also"></a>Consulte también  
 [Examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
