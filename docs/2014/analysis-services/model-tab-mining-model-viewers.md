---
title: Pestaña modelo (visores de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 42285f94057441d01259c5fd54ce896dd0316b94
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537367"
---
# <a name="model-tab-mining-model-viewers"></a>Pestaña Modelo (Visores de modelos de minería de datos)
  La pestaña **Modelo** del Visor de series temporales de Microsoft muestra una representación de una serie temporal como un nodo en un gráfico, similar a la utilizada en los modelos de árboles de decisión.  
  
 Utilice esta vista de un modelo de serie temporal para extraer información útil sobre el análisis de la serie temporal, incluida la ecuación del gráfico, los términos ARIMA y los coeficientes.  
  
 **Para obtener más información:** [Algoritmo de serie temporal de Microsoft](data-mining/microsoft-time-series-algorithm.md), [Examinar un modelo usando el Visor de serie temporal de Microsoft](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md), [Algoritmo de serie temporal de Microsoft](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos que desee ver. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado de este tipo de modelo o el **Visor de árbol de contenido genérico de Microsoft** . También puede utilizar visores de complemento, si están disponibles.  
  
 **Acercar**  
 Acerque el diagrama.  
  
 **Alejar**  
 Aleje el diagrama.  
  
 **Copiar vista del gráfico**  
 Copie la sección visible del diagrama en el portapapeles.  
  
 **Copiar todo el gráfico**  
 Copie el diagrama completo en el portapapeles.  
  
 **Ajustar diagrama a la ventana**  
 Aleje el diagrama hasta que el todo él se ajuste a la pantalla.  
  
 **Palmera**  
 Seleccione un árbol de la lista desplegable para mostrarlo en el visor  
  
 Si el modelo de serie temporal incluye varias series, cada serie se representa como un árbol independiente. Por ejemplo, si creó predicciones a lo largo del tiempo para [Quantity] y [Sales Amount], se crea una serie independiente para cada atributo de predicción.  
  
 La longitud del resaltado de colores en la lista indica el número de niveles del árbol. Es decir, un modelo de serie temporal que se puede representar mediante un único nodo tendría una única ecuación para describir la tendencia y la barra coloreada sería muy corta. (Por supuesto, si el modelo es un modelo mixto, el nodo contendrá una ecuación ARIMA y otra ARTXP).  
  
 Si el árbol mostrado en la lista desplegable tiene una barra coloreada más larga, significa que el modelo tiene muchas bifurcaciones en el árbol. La bifurcación significa que la regresión es más compleja y el modelo se tiene que dividir en varios segmentos, con una ecuación diferente (o par de ecuaciones) en cada nodo.  
  
 **Fondo**  
 Utilice este control para seleccionar el estado que se representa mediante el color de fondo en cada nodo.  
  
 **Expansión predeterminada**  
 Ajuste el número de niveles predeterminado que se muestra para todos los árboles del modelo.  
  
 **Mostrar nivel**  
 Cambie el número de niveles que se muestra en el árbol.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
