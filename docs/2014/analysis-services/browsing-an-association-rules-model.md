---
title: Examinar un modelo de reglas de asociación | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ff9705949be3fb9bf99d985d0db1aa17d93ab1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088468"
---
# <a name="browsing-an-association-rules-model"></a>Examinar un modelo de reglas de asociación
  Al abrir un modelo de asociación mediante **examinar**, el modelo se muestra en un visor interactivo, similar al visor de reglas de asociación [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]de.  El visor le permite comprobar de un vistazo qué elementos estaban en correlación entre sí y muestra las reglas que puede utilizar para la predicción o para realizar recomendaciones.  
  
##  <a name="BKMK_ViewerTabs"></a>Explorar el modelo  
 Al abrir un modelo de minería de datos que se creó [!INCLUDE[msCoName](../includes/msconame-md.md)] mediante el algoritmo reglas de Asociación de, la ventana **examinar** incluye las siguientes vistas, cada una diseñada para que pueda explorar un aspecto diferente del modelo:  
  
-   [Conjuntos](#BKMK_Itemsets)  
  
-   [Reglamento](#BKMK_Rules)  
  
-   [Red de dependencias](#BKMK_Dependency)  
  
 Tome nota de la opción en cada pestaña, **Mostrar nombre largo** . Si selecciona esta opción, puede mostrar u ocultar la tabla desde la que el conjunto de elementos se origina, y luego abreviar o alargar el nombre de la regla o el conjunto de elementos. Esta opción es particularmente útil cuando los datos de casos y los datos de atributos son de orígenes de datos distintos.  
  
 Para experimentar con un modelo de asociación, puede utilizar los datos de ejemplo en la pestaña Asociado del libro de ejemplo y generar un modelo de asociación con todos los valores predeterminados. También puede crear un modelo de análisis de la cesta de compras y abrirlo con **examinar**.  
  
###  <a name="BKMK_Itemsets"></a>Conjuntos  
 La pestaña **conjuntos** es un buen lugar para empezar a explorar un modelo de asociación. Esta pestaña muestra una lista de los elementos que el modelo encontró juntos con frecuencia.  
  
 ![Lista de elementos de un modelo de asociación](media/dm13-association-itemsets.gif "Lista de elementos de un modelo de asociación")  
  
 El ejemplo más común de conjuntos de elementos se encuentra en un modelo de cesta de la compra, donde un conjunto de elementos representa pares o conjuntos de productos que muchos clientes compran al mismo tiempo. Sin embargo, según cómo agrupe y ordene los elementos, el conjunto de elementos puede contener una secuencia de películas que los clientes piden durante un período de tiempo o de eventos que tienden a aparecer en una ubicación concreta.  
  
 Un conjunto de *elementos puede contener tan solo un elemento* en dos, tres o, sin embargo, muchos se establece como el tamaño máximo del conjunto de elementos para el modelo. Para cada conjunto de conjunto, el visor muestra la *compatibilidad*, la *probabilidad*y el *tamaño*del conjunto de conjuntos. La compatibilidad y la probabilidad son las estadísticas principales utilizadas para alinear los conjuntos de elementos y las reglas que genera un modelo de asociación. Estos valores también se utilizan para calcular y describir su importancia.  
  
 **Compatibilidad con**. La compatibilidad indica el número de casos o filas de datos de entrada con este elemento. Por ejemplo, si un conjunto de elementos contiene dos elementos que se encuentran en un carro de la compra, el número de la columna **soporte** indica el número de veces que se ha producido la combinación de elementos en los datos de origen.  
  
 **Tamaño**. Al cambiar el tamaño del conjunto de elementos, puede controlar la longitud de las listas de conjuntos de elementos. Si no desea ver los productos individuales en la lista, cambie la opción, **tamaño mínimo**del conjunto de valores, a 2 o más.  Si restringe la lista aumentando el tamaño mínimo de los conjuntos de elementos podrá buscar patrones muy concretos. Esto podría serle útil si está trabajando con un conjunto de datos muy grande.  
  
 Puede filtrar el número de conjuntos que se muestran en la pestaña cambiando los valores de **compatibilidad mínima** y **máximo de filas** . Si aumenta el valor de **compatibilidad mínima** , la lista mostrará menos conjuntos, pero conjuntos serán las más comunes en los datos de entrada. Tanto si es común como importante, es otra pregunta que puede explorar mediante la pestaña **reglas** .  
  
 Tenga en cuenta que al cambiar el valor de compatibilidad u otros controles en la pestaña **conjuntos** solo se cambian los elementos que se muestran y no se ve afectado el modelo subyacente. Si desea generar menos o más conjuntos, o limitar su tamaño, debe utilizar los parámetros `MINIMUM_SUPPORT` y `MAXIMUM_SUPPORT`, disponibles en el cuadro de diálogo parámetros de **algoritmo** .  
  
##### <a name="explore-the-itemsets-list"></a>Explorar la lista de conjuntos de elementos  
  
1.  Haga clic en la columna **soporte** para ordenar de mayor a menor compatibilidad. Esto le proporcionará una idea de lo que los clientes compran con más frecuencia.  
  
2.  Para centrarse en un conjunto de elementos de interés determinado, a partir de los muchos miles de combinaciones posibles, escriba algún texto en el cuadro **filtrar** conjunto de elementos.  
  
     Aquí hemos escrito `Gloves`. Al aplicar el filtro, la lista se actualiza para mostrar solo los conjuntos de elementos que contienen guantes. Esto le permite centrarse en las transacciones en las que los clientes compraron guantes y otros artículos.  
  
     La opción **Filtrar conjunto de elementos** también muestra una lista de los filtros que ha usado anteriormente.  
  
3.  Cambie el valor de **tamaño mínimo** del conjunto de elementos para filtrar los clientes que compraron solo guantes y ningún otro elemento.  
  
4.  Haga clic en la lista desplegable de la opción **Mostrar**para controlar cómo se muestran los atributos:  
  
    -   **Mostrar el valor y el nombre del atributo**  
  
    -   **Mostrar solo el valor del atributo**  
  
    -   **Mostrar solo el nombre del atributo**  
  
     Observe cómo cambia el nombre. En el caso de un modelo de cesta de la compra, que se crea con tablas anidadas de productos que varios clientes compraron, el nombre de atributo suele ser el nombre del producto y la presencia del producto en la lista se marca como `Existing`, lo que significa que el cliente compró el artículo.  
  
     El opuesto de `Existing` es `Missing`, que puede ser un atributo muy útil para investigar en minería de datos. Por ejemplo, supongamos que el conjunto de elementos A + B es tan popular que quería encontrar clientes que compraron el elemento A pero no el elemento B. Para ello, puede usar una consulta de predicción y recuperar las transacciones con una pero no la otra, y realizar algunos análisis más en ellos. Para obtener información sobre cómo crear consultas de predicción en modelos de asociación, vea [ejemplos de consultas de modelos de asociación](data-mining/association-model-query-examples.md) en libros en pantalla de SQL Server  
  
5.  Para forzar que se vuelva a mostrar la lista de conjuntos con los nuevos criterios de filtro, puede activar o desactivar la casilla **Mostrar nombre largo** .  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a>Reglamento  
 La pestaña **reglas** combina información sobre conjuntos y su valor relativo.  
  
 ![Lista de reglas creadas por un modelo de asociación](media/dm13-association-rules.gif "Lista de reglas creadas por un modelo de asociación")  
  
 La *probabilidad* representa la fracción de casos del conjunto de DataSet que contiene la combinación de elementos de destino. La probabilidad es similar al concepto estadístico de *confianza*y proporciona una indicación de la probabilidad de que se produzca el resultado de una regla. Puede cambiar el valor de **probabilidad mínima** en este panel para filtrar las reglas que se muestran.  
  
 El valor de **probabilidad mínima** que se ve inicialmente es el valor de umbral que usó el algoritmo al generar el modelo. Una vez completado el modelo, no puede reducir este valor, pero puede aumentarlo para mostrar solo los elementos de probabilidad más altos.  
  
 La *importancia* está diseñada para medir la utilidad de una regla. Una regla que sea muy común puede ser tan ubicua que tenga poco valor informativo. Cuanto mayor sea la importancia, más valiosa será la regla para predecir el resultado. En el [análisis de la cesta de compras &#40;tabla análisis para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md) Tool, la importancia puede combinarse con el precio de los artículos para determinar las agrupaciones que son potencialmente más valiosas en términos de ventas.  
  
##### <a name="explore-the-rules-list"></a>Explorar la lista de reglas  
  
1.  Intente hacer clic en los encabezados de columna ( **probabilidad**, **importancia**y **regla** ) para ver cómo cambian los datos.  
  
2.  Use la opción **filtrar regla** para escribir valores y centrarse en reglas de destino.  
  
     Por ejemplo, si desea ver todas las reglas que predicen qué clientes es probable que compren junto con guantes, escriba "guantes" en el cuadro de texto y actualice el panel.  
  
     La opción **Filtrar conjunto de elementos** también muestra una lista de los filtros que ha usado anteriormente.  
  
3.  Para forzar que se vuelva a mostrar la lista de reglas usando criterios de filtro, puede activar o desactivar la casilla **Mostrar nombre largo** .  
  
4.  Use la opción **Mostrar** para controlar la manera en que se muestran los nombres de las reglas.  
  
5.  Establezca el valor de la opción **número máximo de filas** en 100 y, a continuación, haga clic en **copiar a Excel**.  
  
     Tenga en cuenta que el cambio de este valor no afecta a la cantidad de datos del modelo; simplemente controla el número de filas de la lista de visualización. Esta opción puede ser útil cuando se trabaja con modelos muy grandes.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a>Red de dependencias  
 La pestaña **red de dependencias** es un mapa visual de las correlaciones entre elementos. Cada óvalo del gráfico (denominado *nodo*) representa un par atributo-valor, como "chaleco = Existing" o "Age = 1-30".  Cada línea que conecta los óvalos (a la que se hace referencia como un *borde*) representa un tipo de correlación.  
  
 ![Gráfico de redes de dependencias para un modelo de asociación](media/dm13-association-dependencynetwork.gif "Gráfico de redes de dependencias para un modelo de asociación")  
  
##### <a name="explore-the-dependency-network"></a>Explorar la red de dependencias  
  
1.  Haga clic en el botón **Buscar** y use el cuadro de diálogo **Buscar nodo** para escribir un elemento de interés.  
  
     Por ejemplo, escriba "guantes" y, a continuación, maximice el gráfico en la ventana para que pueda ver fácilmente los resultados.  
  
     Se resalta el nodo que contiene el elemento, mientras que las flechas que apuntan al nodo representan una regla que conecta elementos.  
  
     La dirección de la flecha le indica la dirección de la regla. Por ejemplo, si alguien que compra guantes también es probable que compre un chaleco, la flecha comenzará desde el nodo "guante" y terminará en el nodo "chaleco".  
  
     Para obtener estadísticas adicionales acerca de esta regla, puede hacer clic en la pestaña **reglas** y buscar una regla con la descripción "guante-existente"-> "atribución existente".)  
  
2.  Haga clic en el control deslizante y arrástrelo a la izquierda del visor.  
  
     El control deslizante actúa como filtro en la probabilidad de las reglas. Si desplaza el control deslizante hacia abajo, solo se verán las reglas más similares.  
  
3.  Haga clic en **copiar a Excel** para copiar una instantánea de la ventana actual en Excel.  
  
     No podrá trabajar con el gráfico que copia en Excel; Si necesita un gráfico de red interactiva, use el [&#41;ver modelos de minería de datos en Visio &#40;complementos de minería de datos ](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>Más información sobre los modelos de asociación  
 Puede usar la característica **examinar** para abrir y explorar cualquier modelo creado mediante el algoritmo de reglas de Asociación de Microsoft. Esto incluye los modelos creados con el análisis de la [cesta de compras &#40;tabla análisis para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md) Tool, en la cinta de opciones [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]herramientas de análisis de **tabla** o en.  
  
 Si crea un modelo de reglas de asociación con la herramienta de análisis de cesta de la compra, muchas de las opciones avanzadas se configuran automáticamente.  
  
 Si desea establecer parámetros avanzados o modificar la probabilidad y la compatibilidad mínimas, use el Asistente para la Asociación &#40;el Asistente para la [&#41;de datos del cliente de minería de datos para Excel](associate-wizard-data-mining-client-for-excel.md) o cree su propio modelo mediante la opción [Agregar modelo a estructura &#40;de minería de datos para Excel&#41;de](add-model-to-structure-data-mining-add-ins-for-excel.md) modelado.  
  
-   **Conjuntos:** Al crear el modelo, también puede controlar el número de conjuntos que se generan asignando un valor al parámetro MINIMUM_PROBABILITY. Este parámetro está disponible en el cuadro de diálogo Parámetros de algoritmo.  
  
-   **Reglas:** El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de reglas de Asociación de usa valores de probabilidad para restringir el número de reglas que se generan. Puede controlar el número de reglas estableciendo los parámetros `MINIMUM_PROBABILITY` o `MINIMUM _IMPORTANCE`.  
  
 Para obtener más información acerca de la configuración de parámetros avanzados, vea [algoritmos de minería de datos &#40;SQL Server complementos de minería de datos&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte también  
 [Examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
