---
title: "Ver la fórmula de serie temporal de un modelo (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3d33c91d9e9ed1cfd6bc58e8d44041d0e5f43c96
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>Ver la fórmula de un modelo de serie temporal (Minería de datos)
  Si ha creado un modelo de serie temporal con la minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la forma más sencilla de ver la ecuación de regresión del modelo es usar la **Leyenda de minería de datos** del [Visor de series temporales de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), que presenta todas las constantes en un formato legible.  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>Para ver la fórmula de regresión de ARTXP para un modelo de serie temporal  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione el modelo de serie temporal que desea ver y haga clic en **Examinar**.  
  
     O bien  
  
     En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione el modelo de serie temporal y, a continuación, haga clic en la pestaña **Visor de modelos de minería de datos** .  
  
2.  Haga clic en la pestaña **Modelo** .  
  
3.  Si el modelo contiene varios árboles, seleccione uno en la lista desplegable **Árbol** .  
  
    > [!NOTE]  
    >  Un modelo siempre tendrá varios árboles si tiene más de una serie de datos. Sin embargo, no verá tantos árboles en el **Visor de series temporales** como en el [Visor de árbol de contenido genérico de Microsoft](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c). Esto se debe a que el Visor de series temporales combina la información de ARIMA y ARTXP para cada serie de datos en una única representación.  
  
4.  Haga clic en cualquier nodo hoja en el árbol.  
  
     Los nodos con la etiqueta **Serie de datos** siempre son nodos hoja y contienen una ecuación. Si un nodo **(Todos)** no tiene ningún nodo secundario, también puede contener una ecuación.  
  
5.  Si la **Leyenda de minería de datos** no está disponible, haga clic con el botón derecho en el nodo y seleccione **Mostrar leyenda**.  
  
     La fórmula de ARTXP se muestra en la primera la mitad de la **Leyenda de minería de datos**, como la **Ecuación de nodo de árbol**.  
  
     ![ver la fórmula de serie temporal en la leyenda](../../analysis-services/data-mining/media/ssdm-timeserieslegend.png "ver la fórmula de serie temporal en la leyenda")  
  
### <a name="to-view-the-arima-formula-for-a-time-series-model"></a>Para ver la fórmula de ARIMA para un modelo de serie temporal  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione el modelo de serie temporal que desea ver y haga clic en **Examinar**.  
  
     O bien  
  
     En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione el modelo de serie temporal y, a continuación, haga clic en la pestaña **Visor de modelos de minería de datos** .  
  
2.  Haga clic en la pestaña **Modelo** .  
  
3.  Si el modelo contiene varios árboles, seleccione uno en la lista desplegable **Árbol** .  
  
    > [!NOTE]  
    >  El modelo siempre tendrá varios árboles si incluye más de una serie de datos.  
  
4.  Haga clic en cualquier nodo en el árbol.  
  
     La fórmula de ARIMA se muestra en la segunda la mitad de la **Leyenda de minería de datos**, como la **Ecuación ARIMA**.  
  
5.  Si la **Leyenda de minería de datos** no está disponible, haga clic con el botón derecho en el nodo y seleccione **Mostrar leyenda**.  
  
### <a name="to-get-the-coefficients-and-terms-for-the-equation"></a>Para obtener los coeficientes y los términos de la ecuación  
  
1.  También puede obtener los términos y los coeficientes de la fórmula de regresión de un modelo de serie temporal si crea una **consulta de contenido** en el contenido del modelo.  
  
     Para más información, vea [Ejemplos de consultas de modelos de serie temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)  
  
2.  También puede examinar los modelos de la serie temporal y buscar los términos y coeficientes con el [Visor de árbol de contenido genérico de Microsoft](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
     Para más información, vea [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
    > [!NOTE]  
    >  Si examina el contenido de un modelo mixto en el que se usan los modelos ARIMA y ARTXP, verá que los dos modelos están en árboles separados, unidos en el nodo raíz que representa el modelo. Aunque los modelos ARIMA y ARTXP se presentan en un visor para su comodidad, las estructuras son muy diferentes (como las ecuaciones, que no se combinan o se comparan). El árbol ARTXP es más bien como un árbol de decisión, mientras que el árbol ARIMA representa una serie de medias móviles.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Examinar un modelo usando el Visor de serie temporal de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
  

