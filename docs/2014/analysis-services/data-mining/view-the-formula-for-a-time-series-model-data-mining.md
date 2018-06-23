---
title: Ver la fórmula de serie temporal de un modelo (minería de datos) | Documentos de Microsoft
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
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 11427eb72ea27bd93e8cb360afcf1221ab19b05a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203529"
---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>Ver la fórmula de un modelo de serie temporal (Minería de datos)
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] inData de Visor de Series temporales Diseñador de minería de datos proporciona la manera más fácil de ver los detalles de la ecuación de regresión utilizada en un modelo de serie temporal.  
  
 Puede extraer la fórmula de regresión para un modelo de serie temporal consultando el contenido del modelo. Sin embargo, para ver la fórmula completa de ARTXP o ARIMA, recomendamos que utilice la **leyenda de minería de datos** de la [Visor de Series temporales de Microsoft](browse-a-model-using-the-microsoft-time-series-viewer.md), que presenta todas las constantes en un formato legible.  
  
 Si se crea un modelo mixto, los análisis ARIMA y ARTXP se crean en árboles independientes, unidos en el nodo raíz que representa el modelo. Las estructuras de los árboles ARIMA y ARTXP son muy diferentes. Por ejemplo, el árbol ARTXP es una estructura de árbol, como un árbol de decisión, mientras que el árbol ARIMA representa una serie de medias móviles. Por lo tanto, aunque las dos representaciones se presentan en un modelo por comodidad, se deben tratar como dos modelos independientes. Las ecuaciones son también completamente diferentes y no se pueden combinar ni comparar.  
  
 También puede ver modelos de serie temporal mediante el [Visor de árbol de contenido genérico de Microsoft](../microsoft-generic-content-tree-viewer-data-mining.md). Para obtener más información sobre el contenido de un modelo de serie temporal, vea [contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services: minería de datos&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>Para ver la fórmula de regresión de ARTXP para un modelo de serie temporal  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione el modelo de serie temporal que desea ver y haga clic en **Examinar**.  
  
     O bien  
  
     En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione el modelo de serie temporal y, a continuación, haga clic en la pestaña **Visor de modelos de minería de datos** .  
  
2.  Haga clic en la pestaña **Modelo** .  
  
3.  Si el modelo contiene varios árboles, seleccione uno en la lista desplegable **Árbol** .  
  
    > [!NOTE]  
    >  Un modelo siempre tendrá varios árboles si tiene más de una serie de datos. Sin embargo, no verá tantos árboles en el **Visor de series temporales** como en el [Visor de árbol de contenido genérico de Microsoft](../microsoft-generic-content-tree-viewer-data-mining.md). Esto se debe a que el Visor de series temporales combina la información de ARIMA y ARTXP para cada serie de datos en una única representación.  
  
4.  Haga clic en cualquier nodo hoja en el árbol.  
  
     Los nodos con la etiqueta **Serie de datos** siempre son nodos hoja y contienen una ecuación. Si un nodo **(Todos)** no tiene ningún nodo secundario, también puede contener una ecuación.  
  
5.  Si la **Leyenda de minería de datos** no está disponible, haga clic con el botón derecho en el nodo y seleccione **Mostrar leyenda**.  
  
     La fórmula de ARTXP se muestra en la primera la mitad de la **Leyenda de minería de datos**, como la **Ecuación de nodo de árbol**.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas del Visor de modelo de minería de datos](mining-model-viewer-tasks-and-how-tos.md)   
 [Examinar un modelo usando el Visor de Series temporales de Microsoft](browse-a-model-using-the-microsoft-time-series-viewer.md)   
 [Ejemplos de consultas de modelos de serie temporal](time-series-model-query-examples.md)  
  
  