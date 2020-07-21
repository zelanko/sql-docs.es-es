---
title: Explorar el modelo de agrupación en clústeres (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63280431"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>Explorar el modelo de agrupación en clústeres (Tutorial básico de minería de datos)
  El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de clústeres agrupa los casos en clústeres que contienen características similares. Estas agrupaciones son útiles para la exploración de datos, la identificación de anomalías en los datos y la creación de predicciones.  
  
 El Visor de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)] ofrece las siguientes pestañas para la exploración de modelos de minería de datos de agrupación en clústeres:  
  

  
##  <a name="cluster-diagram-tab"></a><a name="ClusterDiagramTab"></a>Pestaña diagrama del clúster  
 La pestaña Diagrama del clúster muestra todos los clústeres de un modelo de minería de datos. Las líneas entre los clústeres representan la "proximidad" y aparecen sombreadas en función de la similitud entre los clústeres. El color de cada clúster representa la frecuencia de la variable y el estado del clúster.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>Para explorar el modelo en la pestaña Diagrama del clúster  
  
1.  Utilice la lista **modelo de minería de datos** en la parte superior de la pestaña visor de modelos de minería de **datos** para cambiar al `TM_Clustering` modelo.  
  
2.  En la lista **visor** , seleccione **visor de clústeres de Microsoft**.  
  
3.  En el cuadro **variable de sombreado** , seleccione **Bike Buyer**.  
  
     La variable predeterminada es **Population**, pero puede cambiarla a cualquier atributo del modelo para detectar qué clústeres contienen miembros que tienen los atributos que desea.  
  
4.  Seleccione **1** en el cuadro **Estado** para explorar los casos en los que se compró una bicicleta.  
  
     La leyenda de **densidad** describe la densidad del par de estado de atributo seleccionado en la variable de sombreado y el estado. En este ejemplo, nos indica que el clusterwith el sombreado más oscuro tiene el porcentaje más alto de compradores de bicicletas.  
  
5.  Pause su mouse sobre el clúster con el sombreado más oscuro.  
  
     Una información sobre herramientas muestra el porcentaje de casos que tienen el atributo, `Bike Buyer = 1`.  
  
6.  Seleccione el clúster que tiene la mayor densidad, haga clic con el botón derecho en el clúster, seleccione **cambiar nombre de clúster** y escriba Bike buyers **High** para una identificación posterior. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Busque el clúster que tiene el sombreado más ligero (y la densidad más baja). Haga clic con el botón derecho en el clúster, seleccione **cambiar nombre de clúster** y escriba Bike buyers **Low**. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Haga clic en el clúster Bike buyers **High** y arrástrelo hasta un área del panel que le proporcionará una vista clara de sus conexiones a los otros clústeres.  
  
     Al seleccionar un clúster, se resaltan las líneas que conectan este clúster con otros para que pueda ver todas las relaciones existentes para el mismo. Cuando el clúster no está seleccionado, puede saber por la oscuridad de las líneas la intensidad de las relaciones entre todos los clústeres del diagrama. Si el sombreado es claro o inexistente, los clústeres no son muy similares.  
  
9. Use el control deslizante situado en la parte izquierda de la red para filtrar los vínculos de menor intensidad y encontrar los clústeres con las relaciones más próximas. El departamento comercial de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] podría desear combinar los clústeres similares al determinar el mejor método para entregar el envío de correo directo.  
  

  
##  <a name="cluster-profiles-tab"></a><a name="ClusterProfilesTab"></a>Pestaña perfiles del clúster  
 La pestaña **perfiles del clúster** proporciona una vista general del `TM_Clustering` modelo. La pestaña **perfiles del clúster** contiene una columna para cada clúster del modelo. La primera columna enumera los atributos asociados a un clúster como mínimo. El resto del visor contiene la distribución de estados de un atributo por cada clúster. La distribución de una variable discreta se muestra como una barra de color con el número máximo de barras que se muestran en la lista de **barras de histograma** . Los atributos continuos se muestran con un diagrama de rombo, que representa la desviación media y estándar en cada clúster.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>Para explorar el modelo en la pestaña perfiles del clúster  
  
1.  Establezca barras de **histograma** en **5**.  
  
     En nuestro modelo, 5 es el número máximo de estados para cualquier variable.  
  
2.  Si la **leyenda de minería de datos** bloquea la presentación de los **perfiles de atributo**, muévalo fuera del camino.  
  
3.  Seleccione la columna Bike buyers **High** y arrástrela hacia la derecha de la columna **Population** .  
  
4.  Seleccione la columna Bike buyers **Low** y arrástrela a la derecha de la columna Bike buyers **High** .  
  
5.  Haga clic en la columna Bike buyers **High** .  
  
     La columna **variables** se ordena por orden de importancia para ese clúster. Desplácese por la columna y revise las características del clúster Bike Buyer High. Por ejemplo, es muy probable que en todas ellas la característica común sea que la distancia al trabajo sea corta.  
  
6.  Haga doble clic en la celda **Age** de la columna Bike buyers **High** .  
  
     La **leyenda de minería de datos** muestra una vista más detallada y puede ver el intervalo de edad de estos clientes, así como la edad media.  
  
7.  Haga clic con el botón secundario en la columna Bike buyers **Low** y seleccione **Ocultar columna**.  
  

  
##  <a name="cluster-characteristics-tab"></a><a name="ClusterCharacteristicsTab"></a>Pestaña características del clúster  
 Con la pestaña **características del clúster** , puede examinar con más detalle las características que componen un clúster. En lugar de comparar las características de todos los clústeres (como en la pestaña Perfiles del clúster), puede explorar un clúster a la vez. Por ejemplo, si selecciona Bike buyers **High** en la lista de **clústeres** , puede ver las características de los clientes en este clúster. Aunque la presentación es diferente del visor Perfiles del clúster, los resultados son los mismos.  
  
> [!NOTE]  
>  A menos que establezca un valor inicial para **holdoutseed**, los resultados variarán cada vez que procese el modelo. Para obtener más información, vea [elemento HoldoutSeed](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="cluster-discrimination-tab"></a><a name="ClusterDiscriminationTab"></a>Pestaña distinción del clúster  
 Con la pestaña **distinción del clúster** , puede explorar las características que distinguen a un clúster de otro. Después de seleccionar dos clústeres, uno de la lista **clúster 1** y otro de la lista **clúster 2** , el visor calcula las diferencias entre los clústeres y muestra una lista de los atributos que distinguen los clústeres.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>Para explorar el modelo en la pestaña distinción del clúster  
  
1.  En el cuadro **clúster 1** , seleccione **Bike**buyers High.  
  
2.  En el cuadro **clúster 2** , seleccione **Bike**buyers Low.  
  
3.  Haga clic en **variables** para ordenar alfabéticamente.  
  
     Algunas de las diferencias sustanciales entre los clientes de los clústeres de Bike buyers **Low** y Bike buyers **High** son la edad, la propiedad de los automóviles, el número de hijos y la región.  
  
## <a name="related-tasks"></a>Related Tasks  
 Vea los temas siguientes para explorar los demás modelos de minería de datos.  
  
-   [Explorar el modelo de árbol de decisión &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo Bayes Naive &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar el modelo Bayes Naive &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Explorar el modelo de árbol de decisión &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Examinar un modelo usando el visor de clústeres de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [Pestaña distinción del clúster &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [Pestaña perfiles del clúster &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [Pestaña características del clúster &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [Pestaña diagrama del clúster &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
