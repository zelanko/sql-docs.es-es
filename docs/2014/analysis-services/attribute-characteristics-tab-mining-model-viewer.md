---
title: Atributo de la pestaña de características (Visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.characteristics.f1
ms.assetid: f0c3350d-84c0-4ab8-9fb8-1527c2647299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 724ac86a4566bac4647e8e7358608c0f5e4ccd85
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650716"
---
# <a name="attribute-characteristics-tab-mining-model-viewer"></a>Pestaña Características del atributo (Visor de modelos de minería de datos)
  Utilice el panel **Características del atributo** para explorar las relaciones entre los resultados y los atributos de entrada en un modelo Bayes Naïve. Puede elegir el valor del atributo de destino y, a continuación, ver una lista de los atributos de entrada que tienen el efecto más fuerte sobre los resultados.  
  
 **Para obtener más información:** [Algoritmo Bayes Naive de Microsoft](data-mining/microsoft-naive-bayes-algorithm.md), [examinar un modelo usando el Visor Bayes Naive de Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos que se desea ver de los modelos de la estructura de minería de datos actual. El modelo de minería de datos se abrirá automáticamente en el visor personalizado más adecuado para el tipo de modelo elegido.  
  
 **Viewer**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Para cada modelo, tiene la opción de un visor personalizado o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . Los visores de complemento también aparecen en esta lista si están disponibles.  
  
 **Atributo**  
 Elija el atributo de predicción que desee analizar.  
  
 **Valor**  
 Elija un estado para el atributo de predicción establecido en **Atributo**. Dado que los modelos Bayes Naïve no admiten variables continuas, todos los atributos de destino tienen resultados discretos o de datos discretos. El atributo Missing siempre se agrega automáticamente a la lista.  
  
 **Las características de \<estado de predicción >**  
 El gráfico contiene las siguientes columnas, que describen cómo los estados de los atributos de entrada están relacionados con el estado de atributo de predicción seleccionado.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Variable**|Enumera los atributos de entrada del modelo de minería de datos.|  
|**Valores**|Enumera cada estado del atributo de entrada en **Variable**.|  
|**Probabilidad**|La barra representa la probabilidad de que el atributo y el valor de dicha fila estén asociados con el estado seleccionado del atributo de predicción. Sitúe el mouse sobre la barra para ver la probabilidad como un porcentaje.|  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
