---
title: Explorar el modelo de agrupación en clústeres de secuencia (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f8a485d5-47ed-4dd5-bb66-ef4d6d463845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e0904239933361b80727700c94b03e379751251f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63164055"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Explorar el modelo de agrupación en clústeres de secuencia (Tutorial intermedio de minería de datos)
  Ahora que ha creado la **agrupación en clústeres de secuencia con** el modelo de regiones, puede explorarla mediante el [!INCLUDE[msCoName](../includes/msconame-md.md)] visor de agrupación en clústeres de secuencia de la pestaña visor de modelos de **minería** de datos del diseñador de minería de datos. El [!INCLUDE[msCoName](../includes/msconame-md.md)] visor de clústeres de secuencia contiene cinco pestañas: **Diagrama del clúster**, **perfiles del clúster**, **características del clúster**, **ClusterDiscrimination**y **transiciones de estado**. Para obtener más información sobre cómo usar este visor, vea [examinar un modelo usando el visor de clústeres de secuencia de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
-   [Pestaña diagrama del clúster](#bkmk_CDiagram)  
  
-   [Pestaña perfiles del clúster](#bkmk_CProfiles)  
  
-   [Pestaña características del clúster](#bkmk_CChars)  
  
-   [Pestaña distinción del clúster](#bkmk_CDiscrim2)  
  
-   [Pestaña Transiciones de estado](#bkmk_StateTran)  
  
-   [Visor de árbol de contenido genérico](#bkmk_Generic)  
  
##  <a name="bkmk_CDiagram"></a>Pestaña diagrama del clúster  
 En la pestaña **Diagrama del clúster** se muestran gráficamente los clústeres detectados por el algoritmo en la base de datos. El diseño del diagrama, con clústeres similares agrupados juntos, representa las relaciones entre los clústeres. De forma predeterminada, el sombreado de cada nodo representa la densidad de todos los casos del clúster: cuanto más oscuro es el sombreado del nodo, más casos contiene. Puede cambiar el significado del sombreado de los nodos para que represente la compatibilidad de un atributo y un estado dentro de cada clúster.  
  
 También puede cambiar el nombre de los clústeres para identificar los clústeres de destino y trabajar con ellos fácilmente. En este tutorial, cambiará el nombre del clúster que tiene el porcentaje más alto de clientes de la región del Pacífico y el clúster que tiene en total mayor número de casos.  
  
> [!NOTE]  
>  Los casos asignados a clústeres concretos pueden cambiar cuando se vuelve a procesar el modelo, en función de los datos y los parámetros del modelo. Además, si cambia el nombre de los clústeres, estos nombres se perderán cuando vuelva a procesar el modelo de minería de datos.  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>Para cambiar el atributo usado para resaltar los clústeres  
  
1.  En la lista **variable de sombreado** , seleccione **modelo**.  
  
2.  Seleccione el **límite de ciclos** en la lista **Estado** .  
  
     El diagrama se actualiza para mostrar la concentración del producto seleccionado en cada uno de los clústeres. El clúster que tiene el sombreado más oscuro contiene mayor cantidad de gorras de ciclismo (cycling cap). Puede cambiar la variable de sombreado para que use cualquier estado de cualquier columna de entrada.  
  
3.  En la lista **variable de sombreado** , seleccione **rellenado**.  
  
     Cuando cambie la variable de sombreado a Población, el diagrama se actualizará para comparar los clústeres por tamaño. El clúster con el sombreado más oscuro tendrá más casos que los demás clústeres.  
  
#### <a name="to-rename-nodes-in-the-model"></a>Para cambiar el nombre de los nodos del modelo  
  
1.  Cambie la **variable de sombreado** a `Region`y establezca el **Estado** en **Pacific**.  
  
2.  Resalte el nodo más oscuro del gráfico.  
  
3.  Haga clic con el botón derecho en este clúster y seleccione **cambiar nombre de clúster.**  
  
4.  Escriba el nombre**Pacific cluster.**  
  
5.  Cambie el valor de **variable de sombreado** a **población**.  
  
6.  En el gráfico actualizado, busque el clúster más oscuro, que debería ser el clúster más grande. Si a través del sombreado no puede determinar cuál es el clúster más grande, sitúe el mouse sobre cada uno de los clústeres y vea la Información sobre herramientas; a continuación, elija el clúster que contiene mayor número de casos.  
  
7.  Haga clic con el botón derecho en este clúster y seleccione **cambiar nombre de clúster**. Escriba el nuevo nombre, `Largest Cluster`.  
  
 Puede explorar en profundidad el nodo que representa el clúster para ver los detalles de los casos que hay en cada clúster. Esto puede resultar útil si desea tomar alguna acción sobre los resultados del análisis, como por ejemplo, enviar un correo electrónico a un cliente. También puede examinar los demás atributos de los casos que incluyó en la estructura y no se usan en el modelo, como Region e IncomeGroup. Para obtener más información acerca de los modelos de minería de datos a los casos subyacentes, vea [consultas de obtención de detalles &#40;&#41;de minería de datos ](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>Para explorar en profundidad los detalles del diagrama del clúster  
  
1.  Haga clic `Pacific Cluster`con el botón derecho, seleccione obtener **detalles**y, a continuación, seleccione **columnas de modelo y estructura**.  
  
     Se abre el cuadro de diálogo obtener **detalles** . Las columnas que no se utilizan en el modelo pero que están disponibles para realizar consultas tienen el prefijo **Structure**.  
  
     Como puede ver, esta clúster contiene en su mayoría clientes de la región del Pacífico y muy pocos clientes de las demás regiones.  
  
2.  Haga clic en el signo más de la columna anidada v Assoc Seq Line Items para ver la secuencia de artículos en un orden de clientes determinado.  
  
3.  Cierre el cuadro de diálogo obtener **detalles** .  
  
    > [!NOTE]  
    >  El botón **reproducir** permite volver a consultar los datos. sin embargo, la reconsultación no cambia los datos que se muestran, a menos que algún otro proceso actualice dinámicamente el modelo en segundo plano.  
  
 [Volver al principio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CProfiles"></a>Pestaña perfiles del clúster  
 La pestaña **perfiles del clúster** muestra las secuencias que se encuentran en cada clúster. Los clústeres se enumeran en columnas individuales a la derecha de la columna **Estados** .  
  
 En el visor, la fila del **modelo** describe la distribución general de los elementos de un clúster y la fila **Model. samples** contiene secuencias de los elementos. Cada línea de las secuencias de color de cada celda de la fila **Model. samples** representa el comportamiento de un usuario seleccionado aleatoriamente en el clúster.  
  
 Cada color de un histograma de secuencia individual representa un modelo de producto. La Leyenda de minería de datos muestra las secuencias de productos usando tanto la codificación de colores como los nombres de los modelos de productos. Si agregó otras columnas al modelo para la agrupación en clústeres, como Region o Income Group, el visor incluirá una fila adicional por cada columna en la que se mostrará la distribución de estos valores en cada clúster.  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>Para ver las secuencias más comunes de un clúster  
  
1.  Haga clic con el botón derecho en la fila del **modelo** en `Largest Cluster`la columna del clúster y seleccione **Mostrar leyenda**.  
  
     La columna **color** contiene una barra sombreada que indica la frecuencia de los elementos que se encuentran en las secuencias. Cada color representa un elemento diferente. La columna **significado** enumera los nombres de los modelos de producto para cada color. La columna **Distribution (distribución** ) indica el porcentaje de casos que contenían este elemento en una secuencia.  
  
2.  Cierre la **leyenda de minería de datos**.  
  
3.  Haga clic con el botón secundario en la fila **Model. samples** de la columna con el encabezado, **Population** y seleccione **Mostrar leyenda**.  
  
4.  Examinar la lista de secuencias en el modelo general`.`  
  
     En Leyenda de minería de datos se muestran primero las secuencias más comunes, y, como puede ver, Mountain Tire Tube es el primer artículo de muchas secuencias. Esto significa que es muy probable que un cliente incluya primero el artículo Mountain Tire Tube en la cesta de la compra.  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>Para explorar en profundidad los casos en el visor de clústeres  
  
1.  Desplácese hacia abajo en el panel atributo hasta que encuentre la fila `Region` del atributo.  
  
     La fila contiene un histograma para cada clúster del modelo, más un histograma adicional para la **población**, es decir, el conjunto completo de casos utilizados en el modelo. Un histograma es una barra con colores diferentes, donde cada color representa un atributo y el tamaño de la sección coloreada de ese atributo representa el porcentaje de casos en los que aparece ese atributo.  
  
2.  Compare los histogramas de los clústeres a los que `Pacific Cluster` ha `Largest Cluster`cambiado el nombre y. Cada clúster aparece en una columna diferente.  
  
     En ambos se usan colores sólidos, pero los colores son diferentes.  
  
3.  En la `Region` fila, coloque el mouse sobre el histograma de color `Largest Cluster`para.  
  
     En la Información sobre herramientas se muestran los porcentajes reales de casos de cada región.  
  
4.  Haga clic con el botón secundario en el `Region` histograma de `Pacific Cluster`color de la fila de, seleccione obtener **detalles**y, a continuación, seleccione **solo columnas del modelo**.  
  
5.  Mueva la barra de desplazamiento para revisar todos los clientes de este clúster.  
  
     Si vuelve a explorar en profundidad los detalles, podrá ver que la mayoría de los pedidos que contiene el clúster proceden de la región del Pacífico, pero también hay unos pocos de las regiones de Norteamérica y Europa.  
  
6.  Cierre el cuadro de diálogo obtener **detalles** .  
  
 [Volver al principio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CChars"></a>Pestaña características del clúster  
 La pestaña **características del clúster** resume las transiciones entre los Estados de un clúster mostrando las barras que representan visualmente la importancia del valor del atributo para el clúster seleccionado. La columna **variables** le indica lo que el modelo ha descubierto que es importante para el clúster o el rellenado seleccionado: un valor determinado o la relación entre los valores, lo que se conoce como *transición*. La columna **valores** proporciona más detalles sobre el valor o la transición, y la columna **probabilidad** representa visualmente el peso de este atributo o transición.  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>Para ver los atributos importantes de un clúster  
  
1.  En la lista desplegable **clúster** , `Pacific Cluster`seleccione.  
  
     La lista se actualiza para mostrar las características del clúster cuyo nombre ha `Pacific Cluster`cambiado. En este clúster, la característica más importante es `Region`.  
  
2.  Sitúe el mouse sobre la barra sombreada en la fila de `Region`.  
  
     La probabilidad de que el valor sea Pacific es muy elevada. Para obtener más información sobre cómo interpretar estos valores, consulte [referencia técnica del algoritmo de clústeres de secuencia de Microsoft](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
3.  Examine la lista de características del clúster hasta que encuentre la primera fila de transición.  
  
4.  Una fila de transición contiene la transición de texto en la columna **variables** y alguna combinación de valores de atributo secuenciales en la columna **valor** . La secuencia también puede contener los puntos iniciales y los valores que faltan.  
  
     Por ejemplo, supongamos que la transición tiene el valor [Inicio]-> tubo de neumático de la carretera. Esto significa que los clientes de este clúster con frecuencia incluyen primero el artículo Road Tire Tube en su cesta de la compra. Esto podría significar que el producto es un elemento popular que los clientes buscan en primer lugar o podría indicar simplemente que el producto es fácil de encontrar en el lugar de compra.  
  
5.  Desplácese por la lista hasta que encuentre la primera transición que no tiene **[Inicio]** o que **falta** en ella.  
  
     Por ejemplo, supongamos que encuentra la transición, **Touring tire y Touring tire**. Esto significa que los clientes de este clúster compran a menudo estos artículos juntos, exactamente en este orden.  
  
6.  Sitúe el mouse sobre la barra sombreada de esta transición.  
  
     La probabilidad de esta transición se muestra en forma de porcentaje.  
  
7.  En la lista desplegable **clúster** , seleccione **población (todos)**.  
  
     La lista de atributos se actualiza para mostrar las características de todos los pedidos usados para crear el modelo. En este modelo de minería de datos, la característica más importante para distinguir entre clústeres es `Region`, con un valor de **Norteamérica**.  
  
 Después de revisar estas tareas, habrá observado dos cosas. La primera es que necesita una gran cantidad de datos para obtener un número significativo de combinaciones. Por ejemplo, las secuencias con las probabilidades más altas suelen incluir un estado **[Inicio]** o **ausente** .  
  
 La segunda es que hay un efecto de agrupación en clústeres fuerte `Region`en los atributos de, lo que hace más difícil ver los grupos de secuencias. Por tanto, decídase a crear otro modelo que use exclusivamente secuencias y no incluya las columnas de las regiones o los ingresos.  
  
 [Volver al principio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CDiscrim2"></a>Pestaña distinción del clúster  
 La pestaña **distinción del clúster** le ayuda a comparar dos clústeres, para determinar qué atributos distinguen un clúster determinado de otro clúster. La pestaña contiene cuatro columnas: **variables**, **valores**, **clúster 1**y **clúster 2**.  Puede elegir cualquier clúster para usarlo como **clúster 1** y **clúster 2**.  
  
 La columna **variables** indica el nombre del atributo, que puede ser un nombre de columna o una combinación de nombre de columna y la palabra **Transition**. La columna **valores** muestra el valor exacto del atributo o de la transición. Las barras sombreadas de las columnas de **clúster 1** y **clúster 2** indican la intensidad del atributo en los clústeres que se van a comparar. Cuanto mayor sea la barra, mayor será la probabilidad de que incluya casos con ese atributo.  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>Para comparar dos clústeres usando la pestaña Distinción del clúster  
  
1.  En la pestaña **distinción del clúster** , en **clúster 1**, `Pacific Cluster`seleccione.  
  
     De forma predeterminada, la selección de **clúster 2** cambia a **complemento de Pacific Cluster**.  
  
     El atributo Top que distingue `Pacific Cluster` de todos los demás casos es la región. Region es un tipo de atributo de agrupación en clústeres que oculta otros atributos. Para evitar este efecto, intente comparar algunos de los clústeres más pequeños entre sí. Al hacerlo, la lista de atributos cambia y se pueden incluir más transiciones entre los modelos.  
  
2.  Busque una fila de transición y sitúe el mouse sobre la barra sombreada.  
  
     Los elementos de la columna **valores** pueden incluir Estados y transiciones. El sombreado de cada elemento indica la puntuación de la distinción. Para obtener más información sobre el significado de las diferentes puntuaciones, vea [contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia &#40;Analysis Services-&#41;de minería de datos ](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Volver al principio](#bkmk_CDiagram)  
  
##  <a name="bkmk_StateTran"></a>Pestaña transiciones de estado  
 En la pestaña **transiciones de estado** , puede seleccionar un clúster y examinar sus transiciones de estado. Si selecciona **población (todos)** en la lista desplegable clúster, el diagrama muestra la distribución de Estados para todo el modelo de minería de datos.  
  
 Cada nodo del gráfico representa un estado o valor posible de las secuencias que está intentando analizar. El color de fondo de los nodos representa la frecuencia del estado. Las líneas conectan algunos estados, lo que indica una transición entre estados. Puede mover el control deslizante arriba o abajo para cambiar el umbral de probabilidad de las transiciones. Algunos nodos llevan asociados unos números, que indican la probabilidad de ese estado.  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>Para explorar las relaciones en la pestaña de Transiciones de estado  
  
1.  En la pestaña **transiciones de estado** del visor de modelos de minería `Pacific Cluster` de datos, seleccione en la lista de clústeres. Asegúrese de que la opción **Mostrar etiquetas perimetrales** está seleccionada.  
  
     El gráfico se actualiza para mostrar las transiciones que son más comunes en este clúster.  
  
2.  Haga clic en cualquier nodo que esté conectado a otro nodo mediante una línea.  
  
     El gráfico se actualiza y resalta los nodos relacionados. El valor numérico situado junto a la línea indica la probabilidad de la transición.  
  
3.  Suba el control deslizante hasta **todos los vínculos**para aumentar el número de transiciones que se incluyen en el gráfico.  
  
4.  Seleccione **población (todos)** del **clúster**.  
  
     Tenga en cuenta que al cargar un clúster diferente, se restablece la configuración de presentación predeterminada del gráfico, por lo que el control deslizante se sitúa de nuevo en su posición media.  
  
5.  Haga clic en el nodo más oscuro del gráfico, que debe ser **deportivo-100**.  
  
     Fíjese que no hay líneas que conecten este producto con otros.  
  
6.  Mueva hacia arriba un paso el control deslizante para aumentar el número de transiciones que se incluyen en el gráfico. No desplazarse hasta todos los **vínculos** todavía.  
  
     El gráfico se actualiza y se agregan algunas transiciones más, pero ninguna que incluya el modelo Sport-100.  
  
7.  Mueva el control deslizante hasta todos los **vínculos**. Haga clic en el nodo Sport-100, si aún no está seleccionado.  
  
     El gráfico se actualiza para mostrar numerosas transiciones que incluyen el producto Sport-100. La dirección de la flecha de la línea de conexión indica si el artículo Sport-100 se seleccionó como primer o segundo elemento del par.  
  
8.  Haga clic en el nodo de Touring Tire y mueva el control deslizante de nuevo hacia abajo, hasta su posición media.  
  
     En primer lugar, hay muchas líneas de transición que conectan Touring neumático con otros productos, pero al aumentar el umbral de probabilidad, las transiciones menos probables se eliminan del gráfico, con lo que solo se abandona la transición, Touring neumático > Touring neumático. Esta transición significa que si el cliente incluye un artículo Touring Tire en la cesta de la compra, existe una gran probabilidad de que incluya a continuación el producto Touring Tire Tube.  
  
 [Volver al principio](#bkmk_CDiagram)  
  
##  <a name="bkmk_Generic"></a>Visor de árbol de contenido genérico  
 Este visor se puede usar para todos los modelos, sin tener en cuenta el algoritmo o tipo de modelo. El **visor de árbol de contenido de MicrosoftGeneric** está disponible en la lista desplegable **visor** .  
  
 Un árbol de contenido es una representación de un modelo de minería de datos como una serie de nodos, donde cada nodo representa el conocimiento adquirido acerca de los datos de entrenamiento. El nodo puede contener un patrón, un conjunto de reglas, un clúster o la definición de un intervalo de fechas que comparten ciertos atributos. El contenido exacto del nodo varía en función del algoritmo y del atributo de predicción, pero la representación general del contenido es la misma.  
  
 Puede expandir cada nodo para ver un mayor nivel de detalle y copiar el contenido de cualquier nodo en el Portapapeles. Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>Para ver los detalles de un modelo de agrupación en clústeres de secuencia usando el visor de árbol de contenido genérico  
  
1.  En la pestaña **visor de modelos de minería de datos** , haga clic en la lista **visor** y seleccione visor de **árbol de contenido genérico de Microsoft**.  
  
2.  En el panel **título de nodo** , `Pacific Cluster (1)`haga clic en.  
  
     El nombre de este nodo contiene tanto el nombre descriptivo que se asignó al clúster como el identificador de nodo subyacente. Puede usar los identificadores de nodo para explorar en profundidad otros detalles del modelo.  
  
3.  Expanda el primer nodo secundario, denominado **nivel de secuencia para el clúster 1**.  
  
     El nodo de nivel de secuencia de un clúster contiene los detalles sobre las transiciones y los estados incluidos en dicho clúster. Puede usar estos detalles, disponibles en la columna NODE_DISTRIBUTION, para explorar las secuencias y los estados de cada clúster o del modelo en su conjunto.  
  
4.  Continúe expandiendo los nodos y consulte los detalles en el panel del visor HTML.  
  
 Para obtener más información sobre el contenido del modelo de minería de datos y cómo usar los detalles en el visor, vea [contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia &#40;Analysis Services-data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Volver al principio](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear un modelo de agrupación en clústeres de secuencia relacionado &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de clústeres de secuencia de Microsoft](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Ejemplos de consultas de modelos de clústeres de secuencia](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
