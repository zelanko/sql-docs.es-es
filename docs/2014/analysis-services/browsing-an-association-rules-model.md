---
title: Modelo de reglas de asociación de exploración | Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088468"
---
# <a name="browsing-an-association-rules-model"></a>Examinar un modelo de reglas de asociación
  Al abrir un modelo de asociación utilizando **examinar**, el modelo se muestra en un visor interactivo, similar al Visor de reglas de asociación de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  El visor le permite comprobar de un vistazo qué elementos estaban en correlación entre sí y muestra las reglas que puede utilizar para la predicción o para realizar recomendaciones.  
  
##  <a name="BKMK_ViewerTabs"></a> Explorar el modelo  
 Al abrir un modelo de minería de datos que se creó utilizando el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de reglas de asociación, el **examinar** ventana incluye las siguientes vistas, cada una diseñada para permitirle explorar un aspecto diferente del modelo:  
  
-   [Conjuntos de elementos](#BKMK_Itemsets)  
  
-   [Reglas](#BKMK_Rules)  
  
-   [Red de dependencias](#BKMK_Dependency)  
  
 Tome nota de la opción en cada pestaña, **Mostrar nombre largo** . Si selecciona esta opción, puede mostrar u ocultar la tabla desde la que el conjunto de elementos se origina, y luego abreviar o alargar el nombre de la regla o el conjunto de elementos. Esta opción es particularmente útil cuando los datos de casos y los datos de atributos son de orígenes de datos distintos.  
  
 Para experimentar con un modelo de asociación, puede utilizar los datos de ejemplo en la pestaña Asociado del libro de ejemplo y generar un modelo de asociación con todos los valores predeterminados. También puede crear un modelo de análisis de cesta de la compra y abrirlo con **examinar**.  
  
###  <a name="BKMK_Itemsets"></a> Conjuntos de elementos  
 El **conjuntos de elementos** ficha es un buen lugar para comenzar a explorar un modelo de asociación. Esta pestaña muestra una lista de los elementos que el modelo encontró juntos con frecuencia.  
  
 ![Lista de elementos de un modelo de asociación](media/dm13-association-itemsets.gif "lista de elementos de un modelo de asociación")  
  
 El ejemplo más común de conjuntos de elementos se encuentra en un modelo de cesta de la compra, donde un conjunto de elementos representa pares o conjuntos de productos que muchos clientes compran al mismo tiempo. Sin embargo, según cómo agrupe y ordene los elementos, el conjunto de elementos puede contener una secuencia de películas que los clientes piden durante un período de tiempo o de eventos que tienden a aparecer en una ubicación concreta.  
  
 Un *conjunto de elementos* puede contener tan solo un elemento a dos, tres, o sin embargo, muchos se establece como el tamaño máximo del conjunto de elementos para el modelo. Para cada conjunto de elementos, el visor muestra el conjunto de elementos *admite*, *probabilidad*, y *tamaño*. La compatibilidad y la probabilidad son las estadísticas principales utilizadas para alinear los conjuntos de elementos y las reglas que genera un modelo de asociación. Estos valores también se utilizan para calcular y describir su importancia.  
  
 **Compatibilidad con**. La compatibilidad indica el número de casos o filas de datos de entrada con este elemento. Por ejemplo, si un conjunto de elementos contiene dos elementos que se encuentran en una cesta compra, el número en el **soporte** columna indica el número de veces que se ha producido un combinación de elementos en el origen de datos.  
  
 **Tamaño**. Al cambiar el tamaño del conjunto de elementos, puede controlar la longitud de las listas de conjuntos de elementos. Si no desea ver productos individuales en la lista, cambie la opción **tamaño mínimo del conjunto**a 2 o más.  Si restringe la lista aumentando el tamaño mínimo de los conjuntos de elementos podrá buscar patrones muy concretos. Esto podría serle útil si está trabajando con un conjunto de datos muy grande.  
  
 Puede filtrar el número de conjuntos de elementos que se muestran en la ficha cambiando el **soporte mínimo** y **número máximo de filas** valores. Si aumenta el **soporte mínimo** valor, la lista mostrará menos conjuntos de elementos, pero los conjuntos de elementos serán los más comunes en los datos de entrada. Si lo común es el mismo tan importante es otra cuestión, que puede probar con el **reglas** ficha.  
  
 Tenga en cuenta que al cambiar el valor de soporte técnico u otros controles en el **conjuntos de elementos** ficha solo cambia los elementos que se muestran y no afectan el modelo subyacente. Si desea generar menos o más conjuntos de elementos, o limitar su tamaño, debe usar los parámetros, `MINIMUM_SUPPORT` y `MAXIMUM_SUPPORT`, disponible en el **parámetros de algoritmo** cuadro de diálogo.  
  
##### <a name="explore-the-itemsets-list"></a>Explorar la lista de conjuntos de elementos  
  
1.  Haga clic en el **admite** columna para ordenar por soporte de mayor a menor. Esto le proporcionará una idea de lo que los clientes compran con más frecuencia.  
  
2.  Para centrarse en un determinado conjunto de elementos de interés, de los muchos miles de combinaciones posibles, escriba algún texto en el **Filtrar conjunto de elementos** cuadro.  
  
     Aquí hemos escrito `Gloves`. Al aplicar el filtro, la lista se actualiza para mostrar solo los conjuntos de elementos que contienen guantes. Esto le permite centrarse en las transacciones en las que los clientes compraron guantes y otros artículos.  
  
     La opción **Filtrar conjunto de elementos** también muestra una lista de los filtros que ha usado anteriormente.  
  
3.  Cambie el valor de **tamaño mínimo del conjunto** para filtrar los clientes que compraron solo guantes y no hay otros elementos.  
  
4.  Haga clic en la lista desplegable para la opción **mostrar**, para controlar cómo se muestran los atributos:  
  
    -   **Mostrar el valor y el nombre del atributo**  
  
    -   **Mostrar solo el valor del atributo**  
  
    -   **Mostrar solo el nombre del atributo**  
  
     Observe cómo cambia el nombre. En el caso de un modelo de cesta de la compra, que se crea con tablas anidadas de productos que varios clientes compraron, el nombre de atributo suele ser el nombre del producto y la presencia del producto en la lista se marca como `Existing`, lo que significa que el cliente compró el artículo.  
  
     El opuesto de `Existing` es `Missing`, que puede ser un atributo muy útil para investigar en minería de datos. Por ejemplo, suponga que el conjunto de elementos A + B es tan muy popular que desea encontrar a los clientes que compraron el artículo A pero no elementos B. Puede hacerlo mediante una consulta de predicción y recuperar las transacciones con una pero no en la otra y realizar un análisis posterior en las. Para obtener información acerca de cómo crear consultas de predicción en modelos de asociación, vea [ejemplos de consultas de modelo de asociación](data-mining/association-model-query-examples.md) en libros en pantalla de SQL Server  
  
5.  Para forzar la lista de conjuntos de elementos para volver a mostrar con los nuevos criterios de filtro, puede activar o desactivar el **Mostrar nombre largo** casilla de verificación.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Reglas  
 El **reglas** ficha combina información sobre los conjuntos de elementos y su valor relativo.  
  
 ![Lista de reglas creadas por un modelo de asociación](media/dm13-association-rules.gif "lista de reglas creadas por un modelo de asociación")  
  
 *Probabilidad* representa la fracción de casos del conjunto de datos que contiene la combinación de elementos de destino. Probabilidad es similar al concepto estadístico de *confianza*y le ofrece una indicación de la probabilidad de que el resultado de una regla es que se produzca. Puede cambiar el valor de **probabilidad mínima** en este panel para filtrar las reglas que se muestran.  
  
 El valor de **probabilidad mínima** que ve inicialmente es el valor de umbral que se utilizó el algoritmo al generar el modelo. Una vez completado el modelo, no se puede reducir este valor, pero puede incrementarlo para mostrar solo los elementos con mayor probabilidad.  
  
 *Importancia* está diseñada para medir la utilidad de una regla. Una regla que sea muy común puede ser tan ubicua que tenga poco valor informativo. Cuanto mayor sea la importancia, más valiosa será la regla para predecir el resultado. En el [análisis de cesta de la compra &#40;herramientas de análisis de tabla para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) herramienta, importancia se puede combinar con el precio de los elementos para determinar los paquetes que potencialmente son muy valiosos en términos de ventas.  
  
##### <a name="explore-the-rules-list"></a>Explorar la lista de reglas  
  
1.  Intente hacer clic en la columna de títulos - **probabilidad**, **importancia**, y **regla** : para ver cómo cambian los datos.  
  
2.  Use la **regla de filtro** opción para escribir los valores y centrarse en las reglas que prefiera.  
  
     Por ejemplo, si desea ver todas las reglas que predicen qué clientes es probable que compren guantes, escriba "guantes" en el cuadro de texto y actualizar el panel.  
  
     La opción **Filtrar conjunto de elementos** también muestra una lista de los filtros que ha usado anteriormente.  
  
3.  Para forzar la lista de reglas para volver a mostrar el uso de criterios de filtro, puede activar o desactivar el **Mostrar nombre largo** casilla de verificación.  
  
4.  Utilice la opción **mostrar** para controlar la manera en que se muestran los nombres de las reglas.  
  
5.  Establezca el valor de la **número máximo de filas** opción a 100 y, a continuación, haga clic en **copiar a Excel**.  
  
     Tenga en cuenta que si cambia este valor no tiene ningún efecto en la cantidad de datos en el modelo; simplemente controla el número de filas en la lista para mostrar. Esta opción puede ser útil cuando se trabaja con modelos muy grandes.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Red de dependencias  
 El **red de dependencias** ficha es un mapa visual de las correlaciones entre elementos. Cada Óvalo del gráfico (denominados un *nodo*) representa un par de atributo-valor, como "chaleco = existente" o "edad = 1-30".  Cada línea que conecta los óvalos (denominados un *edge*) representa un tipo de correlación.  
  
 ![Gráfico de red de dependencias de un modelo de asociación](media/dm13-association-dependencynetwork.gif "gráfico de red de dependencias de un modelo de asociación")  
  
##### <a name="explore-the-dependency-network"></a>Explorar la red de dependencias  
  
1.  Haga clic en el **buscar** botón y utilizar el **buscar nodo** cuadro de diálogo para escribir un elemento de interés.  
  
     Por ejemplo, escriba "guantes" y, a continuación, maximice el gráfico en la ventana de modo que puede ver fácilmente los resultados.  
  
     Se resalta el nodo que contiene el elemento, mientras que las flechas que apuntan al nodo representan una regla que conecta elementos.  
  
     La dirección de la flecha le indica la dirección de la regla. Por ejemplo, si alguien que compre guantes es probable que compre un chaleco, la flecha iniciar desde el nodo "guante" y finalizar en el nodo "chaleco".  
  
     Para obtener estadísticas adicionales acerca de esta regla, puede hacer clic en el **reglas** tabulador y busque una regla con la descripción "Guante - existente" -> "Chaleco - existente.")  
  
2.  Haga clic en el control deslizante y arrástrelo a la izquierda del visor.  
  
     El control deslizante actúa como filtro en la probabilidad de las reglas. Si desplaza el control deslizante hacia abajo, solo se verán las reglas más similares.  
  
3.  Haga clic en **copiar a Excel** para copiar una instantánea de la ventana actual en Excel.  
  
     No podrá trabajar con el gráfico que se copia en Excel; Si necesita un gráfico interactivo de red, use la [ver datos de modelos de minería en Visio &#40;complementos de minería de datos&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>Más información acerca de los modelos de asociación  
 Puede usar el **examinar** característica para abrir y explorar un modelo que se creó mediante el algoritmo de reglas de asociación de Microsoft. Esto incluye los modelos generados mediante la [análisis de cesta de la compra &#40;herramientas de análisis de tabla para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) herramienta, en el **herramientas de análisis de tabla** cinta de opciones, o en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Si crea un modelo de reglas de asociación con la herramienta de análisis de cesta de la compra, muchas de las opciones avanzadas se configuran automáticamente.  
  
 Si desea establecer parámetros avanzados o modificar la probabilidad mínima y compatibilidad, use el [Asistente asociar &#40;cliente de minería de datos para Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) asistente, o crear su propio modelo utilizando el [Agregar modelo a Estructura &#40;complementos minería de datos para Excel&#41; ](add-model-to-structure-data-mining-add-ins-for-excel.md) opción de modelado.  
  
-   **Conjuntos de elementos:** Cuando se crea el modelo, también puede controlar el número de conjuntos de elementos que se generan asignando un valor al parámetro MINIMUM_PROBABILITY. Este parámetro está disponible en el cuadro de diálogo parámetros de algoritmo.  
  
-   **Reglas:** El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de reglas de asociación usa valores de probabilidad para restringir el número de reglas que se generan. Puede controlar el número de reglas estableciendo los parámetros `MINIMUM_PROBABILITY` o `MINIMUM _IMPORTANCE`.  
  
 Para obtener más información acerca de cómo configurar los parámetros avanzados, consulte [algoritmos de minería de datos &#40;complementos de minería de datos de SQL Server&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
