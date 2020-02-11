---
title: Examinar un modelo de agrupación en clústeres | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- clustering [data mining]
- mining model, clustering
ms.assetid: 7f3f0949-d791-403a-88e2-54cb1a803dae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b2662a08974c0eee0eed58b21d77421b3b75749
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064680"
---
# <a name="browsing-a-clustering-model"></a>Examinar un modelo de clústeres
  Al abrir un modelo de agrupación en clústeres mediante **examinar**, el modelo se muestra en un visor interactivo, similar al visor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]agrupación en clústeres de. El visor le ayudará a explorar los clústeres que se han creado y a conocer las características del clúster. Asimismo, podrá comparar y contrastar segmentos individuales con otros segmentos o con la población.  
  
##  <a name="BKMK_Tabs"></a>Explorar el modelo  
 La ventana **examinar** incluye las siguientes herramientas para ayudarle a entender el modelo de agrupación en clústeres y explorar los atributos de los grupos de datos subyacentes:  
  
-   [Diagrama del clúster](#BKMK_ClusterDiagram)  
  
-   [Perfiles del clúster](#BKMK_ClusterProfiles)  
  
-   [Características del clúster](#BKMK_ClusterCharacteristics)  
  
-   [Distinción del clúster](#BKMK_ClusterDiscrimination)  
  
 Para experimentar con un modelo de agrupación en clústeres, puede usar los datos de ejemplo de la pestaña entrenamiento del libro de datos de ejemplo y generar un modelo de agrupación en clústeres mediante el [Asistente para clúster &#40;complementos de minería de datos para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md) y todos los valores predeterminados.  
  
###  <a name="BKMK_ClusterDiagram"></a>Diagrama del clúster  
 La pestaña **Diagrama del clúster** muestra todos los clústeres que se encuentran en un modelo de minería de datos. Aquí puede comprobar la cantidad de agrupaciones que se encontraron en el conjunto de datos y lo cerca o lejos que se encuentran entre sí.  
  
##### <a name="explore-the-cluster-diagram"></a>Explorar el diagrama del clúster  
  
1.  Haga clic en el Clúster 1 en el diagrama.  
  
     Observe cómo las líneas en gris que conectan todos los clústeres cambian, de forma que la líneas que se dirigen al clúster seleccionado se resaltan en azul chillón.  
  
     ![introducción al diagrama del clúster](media/dm13-cluster-diagram-intro.gif "introducción al diagrama del clúster")  
  
     La intensidad de la línea que conecta un clúster a otro representa la importancia de la similitud de los clústeres. Si el sombreado es claro o inexistente, los clústeres no son muy similares. A medida que la línea se va oscureciendo, indica que la similitud entre dos clústeres es más marcada.  
  
2.  Haga clic y arrastre el control deslizante hacia la izquierda del diagrama del clúster para ajustar el número de líneas que va a mostrar el visor.  
  
     Cuando baje el control deslizante, solamente se mostrarán los vínculos de mayor importancia entre los clústeres. De esta forma, resultará más sencillo centrase en los grupos relacionados.  
  
3.  Observe el control **variable de sombreado** en la esquina superior derecha de la ventana **Diagrama del clúster** .  
  
     De forma predeterminada, se establece en **Population**. Esto indica que los clústeres más oscuros proporcionan mayor compatibilidad.  
  
4.  Deténgase sobre cualquier clúster con el cursor.  
  
     Aparecerá una ventana con información sobre herramientas que contiene la población de ese clúster.  
  
5.  Ahora, haga clic en la lista desplegable **variable de sombreado** y elija la variable **Age** . Al hacerlo, aparecerá una lista de valores en el cuadro de texto **Estado** .  
  
     La columna Edad se usa como entrada en este modelo y contiene valores numéricos continuos, pero para fines de agrupación en clústeres, el algoritmo siempre discretiza números. Aquí puede ver las ubicaciones o los grupos creados por el algoritmo, como "muy bajo (\<= 27)" y "muy alto (>= 63)".  
  
6.  En las listas desplegables **Estado** , seleccione **muy alta** y vea cómo cambia el diagrama.  
  
     Si cambia la variable de sombreado, podrá ver fácilmente qué clústeres contienen más elementos de este grupo de edad objetivo y qué clústeres contienen muy pocos clientes de este grupo de edad.  
  
     ![Modificar el diagrama de clúster para mostrar la edad](media/dm13-cluster-diagramshadebyage.gif "Modificar el diagrama de clúster para mostrar la edad")  
  
     Cuanto más oscuro sea el sombreado, mayor será la proporción del atributo de destino y la distribución de valores para ese clúster.  
  
7.  Busque el clúster sombreado más oscuro cuando la variable de **sombreado** esté establecida en Age >65.  
  
     Mantenga el mouse sobre el clúster.  
  
     El valor que aparece ahora en la ventana de información sobre herramientas muestra la población de clientes en este clúster con más de 65 años de edad.  
  
8.  Haga clic con el botón derecho en el clúster y seleccione **cambiar nombre de clúster**. Escriba un nuevo nombre descriptivo, por ejemplo, **más de 65**. El nuevo nombre se guarda con el modelo en el servidor y se puede usar para identificar el clúster en las otras vistas de agrupación en clústeres.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterProfiles"></a>Perfiles del clúster  
 La pestaña **perfiles del clúster** le permite comparar la composición de todos los clústeres de un vistazo. Es un buen punto de partida cuando se empieza a familiarizar con el modelo. Esta vista será también útil más adelante, si ha estado explorando un clúster determinado y decide que necesita buscar clústeres relacionados.  
  
 Los **perfiles de clúster** también proporcionan una buena información general sobre el modo en que los clústeres son diferentes entre sí. Por consiguiente, se recomienda usar esta vista para asignar a cada clúster un nombre descriptivo.  
  
##### <a name="explore-the-cluster-profiles"></a>Explorar los perfiles del clúster  
  
1.  Haga clic en la celda de profesiones, en la columna **Estados** , para ver la lista de todos los valores de ocupación.  
  
2.  Ahora desplace el cursor sobre Empleos en los perfiles del clúster.  
  
     La información sobre herramientas muestra la distribución de los empleos en ese clúster.  
  
     ![Vea los valores detallados en la información sobre herramientas o en la leyenda](media/dm13-cluster-profile-age-tooltip.gif "Vea los valores detallados en la información sobre herramientas o en la leyenda")  
  
     Tenga en cuenta que, en algunos clústeres (como el del gráfico), la lista de profesiones no está completa y algunas profesiones se sustituyen por la etiqueta **other**.  
  
     Esto es así por motivos de diseño, ya que podría resultar difícil ver las diferencias entre muchas barras pequeñas en un histograma. De forma predeterminada, solo se conservan las barras de mayor importancia y las barras restantes se agrupan en **otro** cubo gris.  
  
     Para cambiar el número de barras que están visibles en cualquier histograma, use la opción **barras de histograma**.  
  
3.  Tenga en cuenta que la columna **Age** es diferente de las demás. Haga clic en el rombo del gráfico que se usa para representar la edad.  
  
     La columna Edad inicialmente solo contenía números continuos. El algoritmo de clústeres requiere valores discretos, de modo que agrupó los valores numéricos de la columna Edad en un número limitado de grupos de edad, en función de la distribución de valores.  
  
4.  Haga clic en uno de los gráficos de rombo en un perfil del clúster.  
  
     Estos gráficos de rombo se muestran únicamente cuando los datos de origen usan valores numéricos continuos. Los gráficos de rombo proporcionan algunas estadísticas descriptivas de utilidad, lo cual incluye la media y la desviación estándar para ese valor en cada clúster:  
  
    -   La línea del gráfico de rombo representa el intervalo de valores del atributo. Los valores también se muestran en la columna **Estados** a la izquierda del gráfico **perfiles** .  
  
    -   El centro del rombo se encuentra en la media del nodo.  
  
    -   El ancho del rombo representa la varianza del atributo en ese nodo. Por tanto, un rombo más estrecho indica que el nodo puede crear una predicción más exacta.  
  
5.  Para hacer más espacio en el gráfico, haga clic con el botón derecho en un clúster que no necesite ver de inmediato y seleccione **Ocultar columna**. Esto no lo elimina del modelo, simplemente contrae la columna de forma temporal.  
  
     Para ver los clústeres que ha ocultado, puede hacer clic y arrastrar el borde de la columna o seleccionar el nombre del clúster en la lista, **más clústeres**.  
  
6.  Descienda por la lista de atributos hasta que encuentre Bike Buyer y, después, busque el clúster con el porcentaje más alto de los valores Sí.  
  
     Haga clic con el botón derecho en el encabezado de columna del clúster cuyo nombre desea cambiar, seleccione **cambiar nombre de clúster**y escriba **Bike**Buyers.  
  
     El nuevo nombre del clúster se mantiene en todas las vistas y en el servidor hasta que se vuelva a procesar el modelo.  
  
     ![Cambiar el nombre de los clústeres para que el gráfico sea más fácil de utilizar](media/dm13-cluster-rename.gif "Cambiar el nombre de los clústeres para que el gráfico sea más fácil de utilizar")  
  
 **Útiles**  
  
-   Haga clic en un encabezado de columna para ordenar los atributos por orden de importancia respecto a ese clúster.  
  
-   Arrastre las columnas para volver a ordenarlas en el visor.  
  
-   Haga clic en cualquier celda del gráfico de perfiles para ver estadísticas detalladas en la **leyenda de minería de datos**.  
  
-   Haga clic con el botón secundario en cualquier celda y seleccione **columnas del modelo de obtención de detalles** para generar los datos subyacentes en una nueva hoja de cálculo de Excel.  
  
-   Haga clic con el botón derecho en el encabezado de columna del clúster y seleccione **obtención de detalles para estructurar datos** para obtener información detallada sobre los miembros del clúster que no se incluyeron en el modelo.  
  
     Por ejemplo, si va a generar perfiles de clientes, puede dejar la información de contacto en los datos subyacentes (la estructura de minería de datos), pero no incluirla en el modelo, ya que no es útil para el análisis. Sin embargo, una vez se hayan asignado los clientes a los clústeres, podrá ver los datos detallados mediante la obtención de detalles.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterCharacteristics"></a>Características del clúster  
 Con la vista Características de clúster, podrá realizar una exploración profunda de un solo clúster, para buscar los atributos que mejor definen a este grupo de datos.  
  
##### <a name="explore-the-cluster-characteristics"></a>Explorar las características del clúster  
  
1.  Seleccione el clúster de **más de 65** en la lista de **clústeres** .  
  
     Tras seleccionar un clúster, puede ver detalladamente las características que lo componen.  
  
     Los atributos que contiene el clúster se enumeran en las columnas **Variables** ; el estado del atributo se indica en la columna **Valores** .  
  
     Los Estados de los atributos se muestran por orden de importancia, junto con su probabilidad en este clúster, representados como una barra coloreada en la columna **probabilidad** .  
  
     ![Características de un modelo de agrupación en clústeres](media/dm13-cluster-characteristics.gif "Características de un modelo de agrupación en clústeres")  
  
2.  Haga clic en la columna **variables** para ordenar por atributo.  
  
     Al cambiar la variable para ordenar, podrá ver con más facilidad cómo se distribuyen en el grupo los valores de variables tales como ingresos o propiedad de vehículo.  
  
3.  Haga clic en **copiar a Excel**.  
  
     Se agrega una nueva hoja de cálculo al libro que contiene las características del clúster seleccionado.  
  
4.  Ahora elija otro clúster de la lista, **Bike**Buyers.  
  
5.  Haga clic en **copiar a Excel**.  
  
     Tenga en cuenta que el nuevo gráfico de características del clúster se ha agregado en su propia hoja de cálculo. Puede moverla a la misma hoja de cálculo que el otro perfil para facilitar su comparación, lo que hará en el paso siguiente.  
  
 **Útiles**  
  
-   Tenga en cuenta que la principal característica del cliente en el clúster de más de 65 es que no compran el producto. Si quiere saber por qué es así, puede examinar los clústeres y comparar los grupos o bien, puede crear un modelo relacionado con un algoritmo que sea bueno para examinar las causas y los resultados, como un modelo de árbol de decisión o un modelo Bayes naive.  
  
-   Si desea obtener una lista completa de atributos y de probabilidades para este clúster (o para todos los clústeres) puede crear una consulta. Para obtener ejemplos de consultas en los modelos de agrupación en clústeres, vea [ejemplos de consultas de modelos de agrupación en clústeres](data-mining/clustering-model-query-examples.md).  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterDiscrimination"></a>Distinción del clúster  
 Utilice la pestaña **distinción del clúster** para comparar los atributos entre dos clústeres, o entre un clúster y todos los demás casos del conjunto de datos.  
  
 Para resaltar las características de este visor, se comparará con las tablas en paralelo de Excel que se crearon en función de la vista **características del clúster** .  
  
##### <a name="explore-cluster-discrimination"></a>Explorar la distinción del clúster  
  
1.  Utilice las listas **Clúster 1** y **Clúster 2** para seleccionar los clústeres que desea comparar.  
  
    -   Para Clúster 1, seleccione Más de 65.  
  
    -   Para Clúster 2, seleccione Bike Buyers.  
  
     La comparación debería tener una apariencia similar a la del gráfico siguiente:  
  
     ![comparar los clústeres de un modelo](media/dm13-cluster-compareclusters.gif "comparar los clústeres de un modelo")  
  
     Tenga en cuenta que, en segundo plano, el visor de **distinción de clústeres** envía consultas complejas al servidor de minería de datos para extraer los atributos más importantes para distinguir entre los dos grupos, lo que facilita la comparación de dos conjuntos de clientes.  
  
2.  Haga clic en una de las columnas **favorecer...** .  
  
     La barra a la derecha de la lista de atributos y valores muestra las características o valores que son más importantes como rasgos diferenciadores del clúster seleccionado.  
  
3.  Ahora compare las listas de Excel.  
  
     ![Gráfico de redes de dependencias para un modelo de asociación](media/dm13-comparing-profiles-in-excel.gif "Gráfico de redes de dependencias para un modelo de asociación")  
  
     Dado que las estadísticas subyacentes que se usaron para generar la imagen en el visor se guardan en Excel como tablas, puede filtrar y ordenar, y ver los valores reales de probabilidad.  
  
     Además de utilizar Excel, se recomienda que pruebe el visor de clústeres para Visio, el cual permite no solo ver los puntos de datos, sino también modificar y mejorar ampliamente el gráfico. Para obtener más información, vea [tutorial del diagrama del clúster &#40;complementos de minería de datos&#41;](cluster-diagram-walkthrough-data-mining-add-ins.md).  
  
 **Útiles**  
  
 Después de obtener información sobre los grupos de clientes, pruebe a usar el [escenario de escenarios condicionales &#40;herramientas de análisis de tabla para excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md) o el [escenario de búsqueda de objetivos &#40;herramientas de análisis de tabla para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md) herramientas para explorar los factores del modelo que podrían cambiarse para afectar al resultado.  
  
## <a name="see-also"></a>Consulte también  
 [Examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)   
 [Asistente para clúster &#40;complementos de minería de datos para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
  
