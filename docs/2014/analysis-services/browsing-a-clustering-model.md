---
title: Examinar un modelo de agrupación en clústeres | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- clustering [data mining]
- mining model, clustering
ms.assetid: 7f3f0949-d791-403a-88e2-54cb1a803dae
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fab210756002a80e392bac74e7d1378679b05b2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103438"
---
# <a name="browsing-a-clustering-model"></a>Examinar un modelo de clústeres
  Cuando se abre un modelo de agrupación en clústeres con **examinar**, el modelo se muestra en un visor interactivo, similar al Visor de agrupación en clústeres de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El visor le ayudará a explorar los clústeres que se han creado y a conocer las características del clúster. Asimismo, podrá comparar y contrastar segmentos individuales con otros segmentos o con la población.  
  
##  <a name="BKMK_Tabs"></a> Explorar el modelo  
 El **examinar** ventana incluye las siguientes herramientas para ayudarle a entender el modelo de agrupación en clústeres y explorar los atributos de los grupos de datos subyacente:  
  
-   [Diagrama del clúster](#BKMK_ClusterDiagram)  
  
-   [Perfiles del clúster](#BKMK_ClusterProfiles)  
  
-   [Características del clúster](#BKMK_ClusterCharacteristics)  
  
-   [Distinción del clúster](#BKMK_ClusterDiscrimination)  
  
 Para experimentar con un modelo de agrupación en clústeres, puede utilizar los datos de ejemplo en la pestaña entrenamiento del libro de datos de ejemplo y generar un modelo de agrupación en clústeres mediante [Asistente para clúster &#40;complementos minería de datos para Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) y todos los valores predeterminados .  
  
###  <a name="BKMK_ClusterDiagram"></a> Diagrama del clúster  
 El **diagrama del clúster** ficha muestra todos los clústeres que se encuentran en un modelo de minería de datos. Aquí puede comprobar la cantidad de agrupaciones que se encontraron en el conjunto de datos y lo cerca o lejos que se encuentran entre sí.  
  
##### <a name="explore-the-cluster-diagram"></a>Explorar el diagrama del clúster  
  
1.  Haga clic en el Clúster 1 en el diagrama.  
  
     Observe cómo las líneas en gris que conectan todos los clústeres cambian, de forma que la líneas que se dirigen al clúster seleccionado se resaltan en azul chillón.  
  
     ![Introducción al diagrama del clúster](media/dm13-cluster-diagram-intro.gif "Introducción al diagrama del clúster")  
  
     La intensidad de la línea que conecta un clúster a otro representa la importancia de la similitud de los clústeres. Si el sombreado es claro o inexistente, los clústeres no son muy similares. A medida que la línea se va oscureciendo, indica que la similitud entre dos clústeres es más marcada.  
  
2.  Haga clic y arrastre el control deslizante hacia la izquierda del diagrama del clúster para ajustar el número de líneas que va a mostrar el visor.  
  
     Cuando baje el control deslizante, solamente se mostrarán los vínculos de mayor importancia entre los clústeres. De esta forma, resultará más sencillo centrase en los grupos relacionados.  
  
3.  Observe el **Variable de sombreado** control en la esquina superior derecha de la **diagrama del clúster** ventana.  
  
     De forma predeterminada, se establece en **rellenado**. Esto indica que los clústeres más oscuros proporcionan mayor compatibilidad.  
  
4.  Deténgase sobre cualquier clúster con el cursor.  
  
     Aparecerá una ventana con información sobre herramientas que contiene la población de ese clúster.  
  
5.  Ahora, haga clic en el **Variable de sombreado** lista desplegable lista y elija la **Age** variable. Al hacerlo, aparece una lista de valores en el **estado** cuadro de texto.  
  
     La columna Edad se usa como entrada en este modelo y contiene valores numéricos continuos, pero para fines de agrupación en clústeres, el algoritmo siempre discretiza números. Aquí puede ver las bandejas o grupos que ha creado el algoritmo, como "muy bajo (\<= 27)" y "muy alto (> = 63)".  
  
6.  Desde el **estado** listas desplegables, seleccione **muy alto** y vea cómo cambia el diagrama.  
  
     Si cambia la variable de sombreado, podrá ver fácilmente qué clústeres contienen más elementos de este grupo de edad objetivo y qué clústeres contienen muy pocos clientes de este grupo de edad.  
  
     ![Modificar el diagrama del clúster para mostrar la edad](media/dm13-cluster-diagramshadebyage.gif "modificar el diagrama del clúster para mostrar la edad")  
  
     Cuanto más oscuro sea el sombreado, mayor será la proporción del atributo de destino y la distribución de valores para ese clúster.  
  
7.  Busque el clúster sombreado más oscuro cuando la **Variable de sombreado** se establezca en edad > 65.  
  
     Mantenga el mouse sobre el clúster.  
  
     El valor que aparece ahora en la ventana de información sobre herramientas muestra la población de clientes en este clúster con más de 65 años de edad.  
  
8.  Haga clic en el clúster y seleccione **cambiar el nombre de clúster**. Escriba un nombre nuevo que sea descriptivo, como **más de 65**. El nuevo nombre se guarda con el modelo en el servidor y se puede usar para identificar el clúster en las otras vistas de agrupación en clústeres.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterProfiles"></a> Perfiles del clúster  
 El **perfiles del clúster** pestaña le permite comparar la composición de todos los clústeres de un vistazo. Es un buen punto de partida cuando se empieza a familiarizar con el modelo. Esta vista será también útil más adelante, si ha estado explorando un clúster determinado y decide que necesita buscar clústeres relacionados.  
  
 **Perfiles del clúster** también ofrece una buena introducción sobre cómo los clústeres son diferentes entre sí. Por consiguiente, se recomienda usar esta vista para asignar a cada clúster un nombre descriptivo.  
  
##### <a name="explore-the-cluster-profiles"></a>Explorar los perfiles del clúster  
  
1.  Haga clic en la celda con los empleos, en la **estados** columna, para ver la lista de todos los valores para empleos.  
  
2.  Ahora desplace el cursor sobre Empleos en los perfiles del clúster.  
  
     La información sobre herramientas muestra la distribución de los empleos en ese clúster.  
  
     ![Ver valores detallados en la información sobre herramientas o en la leyenda](media/dm13-cluster-profile-age-tooltip.gif "ver valores detallados en la información sobre herramientas o en la leyenda")  
  
     Observe que, en algunos clústeres (por ejemplo, uno en el gráfico), la lista de empleos no está completa y algunos empleos se reemplazan con la etiqueta, **otros**.  
  
     Esto es así por motivos de diseño, ya que podría resultar difícil ver las diferencias entre muchas barras pequeñas en un histograma. De forma predeterminada se conservan solo las barras de mayor importancia y el resto de las barras se agrupa en un gris **otros** depósito.  
  
     Para cambiar el número de barras que están visibles en un histograma, utilice la opción **barras de histograma**.  
  
3.  Tenga en cuenta que la **Age** columna tiene un aspecto diferente de los demás. Haga clic en el rombo del gráfico que se usa para representar la edad.  
  
     La columna Edad inicialmente solo contenía números continuos. El algoritmo de clústeres requiere valores discretos, de modo que agrupó los valores numéricos de la columna Edad en un número limitado de grupos de edad, en función de la distribución de valores.  
  
4.  Haga clic en uno de los gráficos de rombo en un perfil del clúster.  
  
     Estos gráficos de rombo se muestran únicamente cuando los datos de origen usan valores numéricos continuos. Los gráficos de rombo proporcionan algunas estadísticas descriptivas de utilidad, lo cual incluye la media y la desviación estándar para ese valor en cada clúster:  
  
    -   La línea del gráfico de rombo representa el intervalo de valores del atributo. También se muestran los valores en el **estados** columna a la izquierda de la **perfiles** gráfico.  
  
    -   El centro del rombo se encuentra en la media del nodo.  
  
    -   El ancho del rombo representa la varianza del atributo en ese nodo. Por tanto, un rombo más estrecho indica que el nodo puede crear una predicción más exacta.  
  
5.  Para crear más espacio en el gráfico, haga clic en un clúster que no necesite ver de forma inmediata y seleccione **Ocultar columna**. Esto no elimina la columna del modelo, tan solo la contrae temporalmente.  
  
     Para ver los clústeres que ha ocultado, haga clic y arrastre el borde de la columna o seleccione el nombre del clúster en la lista, **más clústeres**.  
  
6.  Descienda por la lista de atributos hasta que encuentre Bike Buyer y, después, busque el clúster con el porcentaje más alto de los valores Sí.  
  
     Haga clic en el encabezado de columna para el clúster que desea cambiar el nombre, seleccione **clúster Rename**y el tipo de **compradores de bicicletas**.  
  
     El nuevo nombre del clúster se mantiene en todas las vistas y en el servidor hasta que se vuelva a procesar el modelo.  
  
     ![Cambiar el nombre de los clústeres para facilitar el uso del gráfico](media/dm13-cluster-rename.gif "cambiar el nombre de los clústeres para facilitar el uso del gráfico")  
  
 **Sugerencias**  
  
-   Haga clic en un encabezado de columna para ordenar los atributos por orden de importancia respecto a ese clúster.  
  
-   Arrastre las columnas para volver a ordenarlas en el visor.  
  
-   Haga clic en cualquier celda en el gráfico de perfiles para ver estadísticas detalladas en el **leyenda de minería de datos**.  
  
-   Haga clic en cualquier celda y seleccione **columnas del modelo de obtención de detalles** para extraer los datos subyacentes a una nueva hoja de cálculo de Excel.  
  
-   Haga clic en la columna del clúster encabezada y seleccione **obtención de detalles para estructurar los datos** para obtener información detallada acerca de los miembros del clúster que no se incluyó en el modelo.  
  
     Por ejemplo, si está creando perfiles de clientes, puede que deje la información de contacto en datos subyacentes (la estructura de minería de datos) pero sin incluirla en el modelo porque no es de utilidad para el análisis. Sin embargo, una vez se hayan asignado los clientes a los clústeres, podrá ver los datos detallados mediante la obtención de detalles.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterCharacteristics"></a> Características del clúster  
 Con la vista Características de clúster, podrá realizar una exploración profunda de un solo clúster, para buscar los atributos que mejor definen a este grupo de datos.  
  
##### <a name="explore-the-cluster-characteristics"></a>Explorar las características del clúster  
  
1.  Seleccione el **más de 65** clúster desde el **clúster** lista.  
  
     Tras seleccionar un clúster, puede ver detalladamente las características que lo componen.  
  
     Los atributos que contiene el clúster se enumeran en las columnas **Variables** ; el estado del atributo se indica en la columna **Valores** .  
  
     Estados del atributo se enumeran por orden de importancia, junto con su probabilidad en este clúster, representado como una barra coloreada en la **probabilidad** columna.  
  
     ![Las características de un modelo de agrupación en clústeres](media/dm13-cluster-characteristics.gif "las características de un modelo de agrupación en clústeres")  
  
2.  Haga clic en el **Variables** columna para ordenar por atributo.  
  
     Al cambiar la variable para ordenar, podrá ver con más facilidad cómo se distribuyen en el grupo los valores de variables tales como ingresos o propiedad de vehículo.  
  
3.  Haga clic en **copiar a Excel**.  
  
     Se agrega una nueva hoja de cálculo al libro que contiene las características del clúster seleccionado.  
  
4.  Ahora elija otro clúster de la lista, **compradores de bicicletas**.  
  
5.  Haga clic en **copiar a Excel**.  
  
     Tenga en cuenta que el nuevo gráfico de características del clúster se ha agregado en su propia hoja de cálculo. Puede moverlo a la misma hoja de cálculo que el otro perfil para hacer más sencilla su comparación, lo cual lo hará en el paso siguiente.  
  
 **Sugerencias**  
  
-   Observe que la característica principal del cliente en el clúster Más de 65 es que no compran su producto. Si quiere saber por qué es así, puede examinar los clústeres y comparar los grupos o bien, puede crear un modelo relacionado con un algoritmo que sea bueno para examinar las causas y los resultados, como un modelo de árbol de decisión o un modelo Bayes naive.  
  
-   Si desea obtener una lista completa de atributos y de probabilidades para este clúster (o para todos los clústeres) puede crear una consulta. Para obtener ejemplos de consultas en modelos de agrupación en clústeres, consulte [ejemplos de consultas de modelo de agrupación en clústeres](data-mining/clustering-model-query-examples.md).  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterDiscrimination"></a> Distinción del clúster  
 Usa el **distinción del clúster** tab para comparar los atributos entre dos clústeres, o entre un clúster y el resto de los casos del conjunto de datos.  
  
 Para resaltar las características de este visor, lo compararemos a las tablas en paralelo en Excel que había creado según la **características del clúster** vista.  
  
##### <a name="explore-cluster-discrimination"></a>Explorar la distinción del clúster  
  
1.  Utilice las listas **Clúster 1** y **Clúster 2** para seleccionar los clústeres que desea comparar.  
  
    -   Para Clúster 1, seleccione Más de 65.  
  
    -   Para Clúster 2, seleccione Bike Buyers.  
  
     La comparación debería tener una apariencia similar a la del gráfico siguiente:  
  
     ![comparar los clústeres de un modelo de](media/dm13-cluster-compareclusters.gif "comparar los clústeres de un modelo")  
  
     Tenga en cuenta que, tras los bastidores, la **distinción del clúster** Visor envía consultas complejas con el servidor de minería de datos, para extraer los atributos que son más importantes para distinguir entre los dos grupos, lo que resulte más fácil comparar dos conjuntos de clientes.  
  
2.  Haga clic en cualquiera de los **favorece...** columnas.  
  
     La barra a la derecha de la lista de atributos y valores muestra las características o valores que son más importantes como rasgos diferenciadores del clúster seleccionado.  
  
3.  Ahora compare las listas de Excel.  
  
     ![Gráfico de red de dependencias de un modelo de asociación](media/dm13-comparing-profiles-in-excel.gif "gráfico de red de dependencias de un modelo de asociación")  
  
     Dado que las estadísticas subyacentes que se usaron para generar la imagen en el visor se guardan en Excel como tablas, puede filtrar y ordenar, y ver los valores reales de probabilidad.  
  
     Además de utilizar Excel, se recomienda que pruebe el visor de clústeres para Visio, el cual permite no solo ver los puntos de datos, sino también modificar y mejorar ampliamente el gráfico. Para obtener más información, consulte [tutorial del diagrama de clúster &#40;complementos de minería de datos&#41;](cluster-diagram-walkthrough-data-mining-add-ins.md).  
  
 **Sugerencias**  
  
 Después de obtener algo de información sobre grupos de clientes, pruebe a usar la [escenario y si &#40;herramientas de análisis de tabla para Excel&#41; ](what-if-scenario-table-analysis-tools-for-excel.md) o [escenario de búsqueda de objetivo &#40;herramientas de análisis de tabla para Excel&#41; ](goal-seek-scenario-table-analysis-tools-for-excel.md) herramientas para explorar los factores que influyen en el modelo que se puede cambiar para modificar los resultados.  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)   
 [Asistente para clúster &#40;datos complementos de minería de datos para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
  