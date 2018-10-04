---
title: Explorar los modelos Market Basket (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: da1c9cb7-6c32-4b9b-96ec-ecea772aeb77
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c71dfded020167ddd9d01c458f370882dc493fbc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211945"
---
# <a name="exploring-the-market-basket-models-intermediate-data-mining-tutorial"></a>Explorar los modelos Market Basket (tutorial intermedio de minería de datos)
  Ahora que ha creado el `Association` modelo, puede explorar utilizando el [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de asociación de la **Visor de modelos de minería de datos** ficha del Diseñador de minería de datos. Este tutorial le guía a través del uso del visor para explorar las relaciones entre los elementos. El visor le ayuda a saber de un vistazo qué productos tienden a aparecer juntos y a obtener una idea general de los patrones que surgen.  
  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de asociación contiene tres fichas: **reglas**, **conjuntos de elementos**, y **red de dependencias**. Dado que cada pestaña revela una vista ligeramente diferente de los datos, cuando explore un modelo, normalmente alternará entre los diferentes paneles varias veces mientras obtiene más detalles.  
  
-   [Pestaña red de dependencias](#bkmk_DepNet)  
  
-   [Pestaña conjuntos de elementos](#bkmk_Itemsets)  
  
-   [Pestaña reglas](#bkmk_Rules)  
  
-   [Vista de contenido genérica](#bkmk_ContentViewer)  
  
 Para este tutorial, se iniciará en el **red de dependencias** ficha y, a continuación, utilice el **reglas** pestaña y **conjuntos de elementos** tab para profundizar sus conocimientos de las relaciones se revelan en el Visor. También utilizará el **Visor de árbol de contenido genérico de Microsoft** para recuperar estadísticas detalladas de reglas individuales o conjuntos de datos.  
  
##  <a name="bkmk_DepNet"></a> Pestaña red de dependencias  
 Con el **red de dependencias** ficha, puede investigar la interacción de los diferentes elementos del modelo. Cada nodo del visor representa un elemento mientras que las líneas entre ellos representan las relaciones. Al seleccionar un nodo, puede ver qué otros nodos predicen el elemento seleccionado o qué elementos predice el elemento actual. En algunos casos, hay una asociación bidireccional entre elementos, lo que significa que aparecen a menudo en la misma transacción. Puede hacer referencia a la leyenda de color de la parte inferior de la pestaña para determinar la dirección de la asociación.  
  
 Una línea que conecta dos elementos significa que es probable que aparezcan juntos en una transacción. En otras palabras, es probable que los clientes compren estos elementos conjuntamente. El control deslizante se asocia con la probabilidad de una regla. Mueva el control deslizante arriba o abajo para filtrar las asociaciones débiles, lo que significa que las reglas tienen una probabilidad baja.  
  
 El gráfico de red de dependencias muestra las reglas por parejas, lo que se puede representar lógicamente como A->B y significa que, si se compra el producto A, es probable que se compre después el producto B. El gráfico no puede mostrar reglas del tipo AB ->C. Si mueve el control deslizante para mostrar todas las reglas pero sigue sin ver ninguna línea en el gráfico, significa que no hubo ninguna pareja de reglas que cumplieran los criterios de los parámetros del algoritmo.  
  
 También puede buscar los nodos por nombre, escribiendo las primeras letras del nombre de atributo. Para más información, vea [Cuadro de diálogo Buscar nodo &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/find-node-dialog-box-mining-model-viewer.md).  
  
#### <a name="to-open-the-association-mode-in-the-microsoft-assocaition-rules-viewer"></a>Para abrir el modo de asociación en el Visor de reglas de asociación de Microsoft  
  
1.  En **el Explorador de soluciones**, haga doble clic en la estructura de la asociación.  
  
2.  En el Diseñador de minería de datos, haga clic en la pestaña **Visor de modelo de minería de datos** .  
  
3.  Seleccione asociación en la lista de modelos de minería de datos en el **modelo de minería de datos** lista desplegable.  
  
#### <a name="to-navigate-the-dependency-graph-and-locate-specific-nodes"></a>Para navegar por el gráfico de dependencias y buscar nodos concretos  
  
1.  En el **Visor de modelos de minería de datos** pestaña, haga clic en el **red de dependencias** ficha.  
  
2.  Haga clic en **acercar** varias veces, hasta que se puede ver fácilmente las etiquetas para cada nodo.  
  
     De forma predeterminada, el gráfico se muestra con todos los nodos visibles. En un modelo complejo, puede haber muchos nodos, con lo que cada nodo es bastante pequeño.  
  
3.  Haga clic en el **+** inicie sesión en la esquina inferior derecha del Visor y mantenga presionado el botón del mouse para desplazarse por el gráfico.  
  
4.  En el lado izquierdo del Visor, arrastre el control deslizante hacia abajo, moviéndolo de **todos los vínculos** (valor predeterminado) a la parte inferior del control deslizante.  
  
5.  El visor actualiza el gráfico para que ahora solo muestre la asociación más fuerte, entre los elementos Touring Tire y Touring Tire Tube.  
  
6.  Haga clic en el nodo con la etiqueta **Touring Tire Tube = Existing**.  
  
     El gráfico se actualiza para resaltar únicamente los elementos que están muy relacionados con este elemento. Observe la dirección de la flecha entre los dos elementos.  
  
7.  En el lado izquierdo del visor, arrastre el control deslizante hacia arriba de nuevo, moviéndolo desde la parte inferior aproximadamente hasta el medio.  
  
     Tenga en cuenta los cambios de la flecha que conecta los dos elementos.  
  
8.  Seleccione **mostrar solo el nombre del atributo** en la lista desplegable en la parte superior del panel de red de dependencias.  
  
     Las etiquetas de texto del gráfico se actualizan para mostrar solo el nombre del modelo.  
  
 [Volver al principio](#bkmk_DepNet)  
  
##  <a name="bkmk_Itemsets"></a> Pestaña conjuntos de elementos  
 Luego, obtendrá más información sobre las reglas y conjuntos de elementos generados por el modelo para los productos Touring Tire Tube y Touring Tire. El **conjuntos de elementos** ficha muestra tres extractos de información importantes relacionados con los conjuntos de elementos que el [!INCLUDE[msCoName](../includes/msconame-md.md)] detecta el algoritmo de asociación:  
  
-   **Soporte técnico:** el número de transacciones en el que se produce el conjunto de elementos.  
  
-   **Tamaño:** el número de elementos del conjunto de elementos.  
  
-   **Elementos:** una lista de los elementos incluidos en cada conjunto de elementos.  
  
 Dependiendo de cómo se configuren los parámetros del algoritmo, éste podría generar muchos conjuntos de elementos. Cada conjunto de elementos que se devuelve en el visor representa las transacciones en las que se vendió el elemento. Mediante el uso de los controles en la parte superior de la **conjuntos de elementos** ficha, puede filtrar el Visor para mostrar solo los conjuntos de elementos que contienen un tamaño mínimo especificado de soporte técnico y el conjunto de elementos.  
  
 Si está trabajando con un modelo de minería de datos diferente y no aparece ningún conjunto de elementos, se debe a que ninguno cumplió los criterios de los parámetros del algoritmo. En este tipo de escenario, puede cambiar los parámetros del algoritmo para permitir conjuntos de elementos que tengan una compatibilidad más baja.  
  
#### <a name="to-filter-the-itemsets-that-are-shown-in-the-viewer-by-name"></a>Para filtrar por nombre los conjuntos de elementos que se muestran en el visor  
  
1.  Haga clic en el **conjuntos de elementos** ficha del Visor.  
  
2.  En el **Filtrar conjunto de elementos** , escriba `Touring Tire`y, a continuación, haga clic fuera del cuadro.  
  
     El filtro devuelve todos los elementos que contienen esta cadena.  
  
3.  En el **mostrar** lista, seleccione **mostrar solo el nombre del atributo**.  
  
4.  Seleccione el **Mostrar nombre largo** casilla de verificación.  
  
     La lista de conjuntos de elementos se actualiza para mostrar solo los conjuntos de elementos que contienen la cadena Touring Tire. El nombre largo del conjunto de elementos incluye el nombre de la tabla que contiene el atributo y el valor de cada elemento.  
  
5.  Desactive el **Mostrar nombre largo** casilla de verificación.  
  
     La lista de conjuntos de elementos se actualiza para mostrar solo el nombre corto.  
  
 Los valores de la **soporte** columna indican el número de transacciones para cada conjunto de elementos. Una transacción para un conjunto de elementos significa una compra que incluía todos los elementos del conjunto de elementos.  
  
 De forma predeterminada, el visor muestra en orden descendente los conjuntos de elementos por compatibilidad. Puede hacer clic en los encabezados de columna para ordenar por una columna diferente, por ejemplo por el tamaño del conjunto de elementos o el nombre. Si le interesa obtener más información sobre las transacciones individuales que están incluidas en un conjunto de elementos, puede obtener detalles de los casos individuales en los conjuntos de elementos. Las columnas de estructura de los resultados de la obtención de detalles son el nivel de ingresos del cliente y su identificador, que no se usaron en el modelo.  
  
#### <a name="to-view-details-for-an-itemset"></a>Para ver los detalles de un conjunto de elementos  
  
1.  En la lista de conjuntos de elementos, haga clic en el **conjunto de elementos** encabezado de columna para ordenar por nombre.  
  
2.  Busque el elemento `Touring Tire` (con sin el segundo elemento).  
  
3.  Haga clic en el elemento, `Touring Tire`, seleccione **Drill Through**y, a continuación, seleccione **columnas de modelo y estructura**.  
  
     El **Drill Through** cuadro de diálogo muestra las transacciones individuales utilizadas como compatibilidad para este conjunto de elementos.  
  
4.  Expanda la tabla anidada vAssocSeqLineItems para ver la lista real de compras en la transacción.  
  
#### <a name="to-filter-itemsets-by-support-or-size"></a>Para filtrar los conjuntos de elementos por compatibilidad o tamaño  
  
1.  Borre cualquier texto que podría estar en el **Filtrar conjunto de elementos** cuadro. No puede utilizar un filtro del texto junto con un filtro numérico.  
  
2.  En el **soporte mínimo** , escriba 100 y, a continuación, haga clic en el fondo del Visor.  
  
     La lista de conjuntos de elementos se actualiza para mostrar solo los conjuntos de elementos con una compatibilidad mínima de 100.  
  
 [Volver al principio](#bkmk_DepNet)  
  
##  <a name="bkmk_Rules"></a> Pestaña reglas  
 El **reglas** pestaña muestra la siguiente información relacionada con las reglas que se encuentra el algoritmo.  
  
-   **Probabilidad:** el *probabilidad* de una regla, definida como la probabilidad de que el elemento dado el elemento del lado izquierdo del lado derecho.  
  
-   **Importancia:** una medida de la utilidad de una regla. Un valor mayor significa una regla mejor.  
  
     La importancia se proporciona para ayudarle a calibrar la utilidad de una regla, porque la probabilidad por sí sola puede ser engañosa. Por ejemplo, si cada transacción contuviera una botella de agua, quizás agregada automáticamente al carro de cada cliente como parte de una promoción, el modelo crearía una regla que predice que la botella de agua tiene una probabilidad de 1. Si se basa en la probabilidad únicamente, esta regla es muy precisa, pero no proporciona información útil.  
  
-   **Regla:** la definición de la regla. Para un modelo de cesta de la compra, una regla describe una combinación concreta de elementos.  
  
 Cada regla puede usarse para predecir la presencia de un elemento de una transacción en función de la presencia de otros elementos. Al igual que en el **conjuntos de elementos** ficha, puede filtrar las reglas para que se muestren solo las reglas más interesantes. Si está trabajando con un modelo de minería de datos que no tiene ninguna regla, podría desear cambiar los parámetros de algoritmo para bajar el umbral de probabilidad de las reglas.  
  
#### <a name="to-see-only-rules-that-include-the-mountain-200-bicycle"></a>Para ver solo reglas que incluyen la bicicleta Mountain-200  
  
1.  En el **Visor de modelos de minería de datos** pestaña, haga clic en el **reglas** ficha.  
  
2.  En el **regla de filtro** , escriba `Mountain-200`.  
  
     Desactive el **Mostrar nombre largo** casilla de verificación.  
  
3.  Desde el **mostrar** lista, seleccione **mostrar solo el nombre del atributo**.  
  
     El Visor mostrará solo las reglas que contienen las palabras "`Mountain-200`". La probabilidad de que la regla le indica qué posibilidades es que cuando alguien compre una `Mountain-200` bicicleta, esa persona también compre el otro producto enumerado.  
  
 Las reglas se ordenan por probabilidad en orden descendente, pero puede hacer clic en los encabezados de columna para cambiar el criterio de ordenación. Si le interesa averiguar más detalles sobre una regla determinada, puede utilizar la obtención de detalles para ver los casos complementarios.  
  
#### <a name="to-view-cases-that-support-a-particular-rule"></a>Para ver los casos que complementan una regla determinada  
  
1.  En el **reglas** pestaña, haga clic en la regla que desea ver.  
  
2.  Seleccione **Drill Through**y, a continuación, seleccione **solo columnas de modelos**, o **columnas de modelo y estructura**.  
  
     El **Drill Through** cuadro de diálogo proporciona un resumen de la regla en la parte superior del panel y una lista de todos los casos que se utilizaron como datos complementarios para la regla.  
  
 [Volver al principio](#bkmk_DepNet)  
  
##  <a name="bkmk_ContentViewer"></a> Visor de árbol de contenido genérico  
 Este visor se puede usar para todos los modelos, sin tener en cuenta el algoritmo o tipo de modelo. El **Visor de árbol de contenido genérico de Microsoft** está disponible en el **Visor** lista desplegable.  
  
 Un árbol de contenido es una representación de un modelo de minería como una serie de nodos, donde cada nodo representa el conocimiento adquirido acerca de cierto subconjunto de los datos. El nodo puede contener un modelo, un conjunto de reglas, un clúster o la definición de un intervalo de fechas que comparten ciertas características. El contenido exacto del nodo difiere dependiendo del algoritmo y el tipo del atributo predecible, pero la representación general del contenido es la misma. Puede expandir cada nodo para ver un mayor nivel de detalle y copiar el contenido de cualquier nodo en el Portapapeles.  
  
#### <a name="to-view-details-about-the-rule-by-using-the-content-viewer"></a>Para ver los detalles sobre la regla utilizando el visor de contenido  
  
1.  En el **Visor de modelos de minería de datos** ficha, seleccione **Visor de árbol de contenido genérico de Microsoft** desde el **Visor** lista.  
  
2.  En el panel Título de nodo, desplácese a la parte inferior de la lista y haga clic en el último nodo.  
  
     El visor muestra los conjuntos de elementos primero y las reglas después, pero no los agrupa. La manera más fácil de buscar un nodo concreto es crear una consulta de contenido. Para más información, vea [Ejemplos de consultas del modelo de asociación](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
3.  En el panel Detalles de nodo, revise el valor de NODE_TYPE y NODE_DESCRIPTION.  
  
     Un tipo de nodo 8 es una regla y un tipo de nodo 7 es un conjunto de elementos. Para una regla, el valor de NODE_DESCRIPTION indica las condiciones que la constituyen. Para un conjunto de elementos, el valor de NODE_DESCRIPTION indica los elementos incluidos en el conjunto de elementos.  
  
 También puede crear una consulta de contenido para obtener estadísticas detalladas sobre las reglas. Para obtener más información sobre el contenido del modelo de minería de datos y cómo interpretarla, vea [contenido del modelo de minería de datos para los modelos de asociación &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Volver al principio](#bkmk_DepNet)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Filtrar una tabla anidada en un modelo de minería de datos &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Lección 3: Generar un escenario de cesta &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)   
 [Lección 4: Generar una escenario de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)   
 [Algoritmo de asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Referencia técnica del algoritmo de asociación de Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)  
  
  
