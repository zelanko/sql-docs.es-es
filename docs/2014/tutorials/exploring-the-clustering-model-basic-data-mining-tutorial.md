---
title: Explorar el modelo de agrupación en clústeres (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26869ca780bc74e3c9c56b38b39195b893dbf523
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147775"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>Explorar el modelo de agrupación en clústeres (Tutorial básico de minería de datos)
  El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de agrupación en clústeres agrupa los casos en los clústeres que contengan características similares. Estas agrupaciones son útiles para la exploración de datos, la identificación de anomalías en los datos y la creación de predicciones.  
  
 El Visor de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)] ofrece las siguientes pestañas para la exploración de modelos de minería de datos de agrupación en clústeres:  
  

  
##  <a name="ClusterDiagramTab"></a> Pestaña diagrama del clúster  
 La pestaña Diagrama del clúster muestra todos los clústeres de un modelo de minería de datos. Las líneas entre los clústeres representan la "proximidad" y aparecen sombreadas en función de la similitud entre los clústeres. El color de cada clúster representa la frecuencia de la variable y el estado del clúster.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>Para explorar el modelo en la pestaña Diagrama del clúster  
  
1.  Use la **Mining Model** lista en la parte superior de la **Visor de modelos de minería de datos** tab para cambiar a la `TM_Clustering` modelo.  
  
2.  En el **Visor** lista, seleccione **Visor de clústeres de Microsoft**.  
  
3.  En el **Variable de sombreado** cuadro, seleccione **Bike Buyer**.  
  
     La variable predeterminada es **rellenado**, pero puede cambiarlo a cualquier atributo en el modelo, para descubrir qué clústeres contienen los miembros que tienen los atributos que desee.  
  
4.  Seleccione **1** en el **estado** cuadro para explorar esos casos donde se compró una bicicleta.  
  
     El **densidad** leyenda describe la densidad del par de estado de atributo seleccionado en la Variable de sombreado y el estado. En este ejemplo nos indica que el clusterwith el sombreado más oscuro tiene el porcentaje más alto de compradores de bicicletas.  
  
5.  Pause su mouse sobre el clúster con el sombreado más oscuro.  
  
     Una información sobre herramientas muestra el porcentaje de casos que tienen el atributo, `Bike Buyer = 1`.  
  
6.  Seleccione el clúster que tiene la máxima densidad, haga clic en el clúster, seleccione **cambiar nombre de clúster** y tipo **Bike Buyers High** para una identificación posterior. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Busque el clúster que tiene el sombreado más ligero (y la densidad más baja). Haga clic en el clúster, seleccione **cambiar nombre de clúster** y tipo **Bike Buyers Low**. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Haga clic en el **Bike Buyers High** del clúster y arrástrelo hasta un área del panel que le proporcionará una visión clara de sus conexiones a los otros clústeres.  
  
     Al seleccionar un clúster, se resaltan las líneas que conectan este clúster con otros para que pueda ver todas las relaciones existentes para el mismo. Cuando el clúster no está seleccionado, puede saber por la oscuridad de las líneas la intensidad de las relaciones entre todos los clústeres del diagrama. Si el sombreado es claro o inexistente, los clústeres no son muy similares.  
  
9. Use el control deslizante situado en la parte izquierda de la red para filtrar los vínculos de menor intensidad y encontrar los clústeres con las relaciones más próximas. El departamento comercial de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] podría desear combinar los clústeres similares al determinar el mejor método para entregar el envío de correo directo.  
  

  
##  <a name="ClusterProfilesTab"></a> Pestaña perfiles del clúster  
 El **perfiles del clúster** ficha proporciona una visión general de la `TM_Clustering` modelo. El **perfiles del clúster** pestaña contiene una columna para cada clúster del modelo. La primera columna enumera los atributos asociados a un clúster como mínimo. El resto del visor contiene la distribución de estados de un atributo por cada clúster. La distribución de una variable discreta se muestra como una barra coloreada y el número máximo de barras aparece en el **barras de histograma** lista. Los atributos continuos se muestran con un diagrama de rombo, que representa la desviación media y estándar en cada clúster.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>Para explorar el modelo en la pestaña perfiles del clúster  
  
1.  Establecer **histograma** las barras de **5**.  
  
     En nuestro modelo, 5 es el número máximo de estados para cualquier variable.  
  
2.  Si el **leyenda de minería de datos** bloquea la presentación de la **perfiles del atributo**, muévalo fuera de la vista.  
  
3.  Seleccione el **Bike Buyers High** columna y arrástrelo a la derecha de la **rellenado** columna.  
  
4.  Seleccione el **Bike Buyers Low** columna y arrástrelo a la derecha de la **Bike Buyers High** columna.  
  
5.  Haga clic en el **Bike Buyers High** columna.  
  
     El **Variables** columna está ordenada por orden de importancia para ese clúster. Desplácese por la columna y revise las características del clúster Bike Buyer High. Por ejemplo, es muy probable que en todas ellas la característica común sea que la distancia al trabajo sea corta.  
  
6.  Haga doble clic en el **Age** de celda en la **Bike Buyers High** columna.  
  
     El **leyenda de minería de datos** muestra una forma más detallada vista y puede ver el intervalo de edad de estos clientes, así como la edad Media.  
  
7.  Haga clic en el **Bike Buyers Low** columna y seleccione **Ocultar columna**.  
  

  
##  <a name="ClusterCharacteristicsTab"></a> Pestaña características del clúster  
 Con el **características del clúster** ficha, puede examinar con más detalle las características que forman un clúster. En lugar de comparar las características de todos los clústeres (como en la pestaña Perfiles del clúster), puede explorar un clúster a la vez. Por ejemplo, si selecciona **Bike Buyers High** desde el **clúster** lista, puede ver las características de los clientes en este clúster. Aunque la presentación es diferente del visor Perfiles del clúster, los resultados son los mismos.  
  
> [!NOTE]  
>  A menos que establezca un valor inicial para **holdoutseed**, los resultados variarán cada vez que procese el modelo. Para obtener más información, consulte [elemento HoldoutSeed](../analysis-services/scripting/properties/holdoutseed-element.md)  
  

  
##  <a name="ClusterDiscriminationTab"></a> Pestaña distinción del clúster  
 Con el **distinción del clúster** ficha, puede explorar las características que distinguen un clúster de otro. Después de seleccionar dos clústeres, uno de los **clúster 1** lista y uno de los **clúster 2** lista, el Visor calcula las diferencias entre los clústeres y muestra una lista de los atributos que distinguir los clústeres más.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>Para explorar el modelo en la pestaña distinción del clúster  
  
1.  En el **clúster 1** cuadro, seleccione **Bike Buyers High**.  
  
2.  En el **clúster 2** cuadro, seleccione **Bike Buyers Low**.  
  
3.  Haga clic en **Variables** para ordenar alfabéticamente.  
  
     Algunas de las diferencias sustanciales entre clientes de la **Bike Buyers Low** y **Bike Buyers High** clústeres incluyen la edad, posesión de un vehículo, el número de hijos y la región.  
  
## <a name="related-tasks"></a>Related Tasks  
 Vea los temas siguientes para explorar los demás modelos de minería de datos.  
  
-   [Explorar el modelo de árbol de decisión &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo Bayes Naive &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar el modelo Bayes Naive &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Explorar el modelo de árbol de decisión &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Examinar un modelo usando el Visor de clústeres de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [Pestaña distinción del clúster &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [Pestaña perfiles de clúster &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [Pestaña características del clúster &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [Pestaña diagrama del clúster &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
