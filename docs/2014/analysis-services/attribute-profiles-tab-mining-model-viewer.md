---
title: Atributo de perfiles de pestaña (Visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.profiles.f1
ms.assetid: 17c7e7ae-273c-4a6b-9a35-e8b9b8e65999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c216ce257c513d59a5007637ca4a5642104306f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650676"
---
# <a name="attribute-profiles-tab-mining-model-viewer"></a>Pestaña Perfiles del atributo (Visor de modelos de minería de datos)
  Utilice la pestaña **Perfiles del atributo** para ver cómo la distribución de los valores de entrada en un estado del modelo Bayes naive contribuye a cada estado del atributo de resultados. La distribución de los valores se muestra como un histograma con colores, todas las distribuciones se presentan en un formato tabular, para facilitar la comparación de los valores.  
  
 **Para obtener más información:** [Algoritmo Bayes Naive de Microsoft](data-mining/microsoft-naive-bayes-algorithm.md), [examinar un modelo usando el Visor Bayes Naive de Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos que desea ver de los modelos de la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Viewer**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Puede elegir el visor personalizado proporcionado para cada modelo de minería de datos o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede usar visores de complemento, si están disponibles.  
  
 **Mostrar leyenda**  
 Seleccione esta opción para mostrar una clave que haga coincidir cada valor de **Estados** con uno de los colores usados en el gráfico de distribución.  
  
 **Barras de histograma**  
 Seleccione la cantidad de barras que se incluirán en el histograma. Si existen más barras de las que eligió mostrar, se retienen las barras de la importancia más alta y el resto de las barras se agrupa en **Otro**.  
  
 **Predicción**  
 Seleccione una columna de predicción del modelo de minería de datos.  
  
 **Perfiles del atributo**  
 La tabla contiene las columnas siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Atributos**|Muestra las columnas del modelo de minería de datos contenidas en el modelo de minería de datos.|  
|**Estados**|Una columna opcional que describe el estado que representa el color en la fila de atributos correspondiente. Agregue o quite mediante la casilla **Mostrar leyenda** .|  
|**Población**|Muestra la distribución del atributo en todo el conjunto de datos.|  
|**Columna de Estados del atributo de predicción**|Muestra una columna para cada estado de la columna de predicción, con cada fila correspondiente a un atributo de entrada en el modelo.|  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
