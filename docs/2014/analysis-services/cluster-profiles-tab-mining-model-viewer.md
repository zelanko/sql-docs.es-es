---
title: Los perfiles de clúster (Visor de modelos de minería de datos) de la ficha | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 663b12f2e83de016d3f1799536b8a3ed674ef544
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680868"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>Pestaña Perfiles del clúster (Visor de modelos de minería de datos)
  Utilice la pestaña **Perfiles del clúster** para obtener una vista general de los clústeres que ha descubierto el algoritmo en un modelo de agrupación en clústeres. La pestaña muestra cada atributo junto con la distribución del atributo en cada clúster.  
  
 **Para obtener más información:** [Algoritmo de clústeres de Microsoft](data-mining/microsoft-clustering-algorithm.md), [examinar un modelo usando el Visor de clústeres de Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos de los de la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Viewer**  
 Elija un visor para ver el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado del modelo de minería de datos o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede utilizar visores de complemento si están disponibles.  
  
 **Mostrar leyenda**  
 Seleccione esta opción para mostrar una clave que muestre la asignación de colores en el visor a los valores de la columna **Estados** .  
  
 **Barras de histograma**  
 Cambie este valor para controlar cuántos estados se incluyen en cada histograma. Si hay más estados de los que ha elegido mostrar, aparecen en el histograma los estados con la probabilidad más alta, y el resto de los estados se agrupan en **Otros**.  
  
 **Atributos**  
 Enumera las columnas incluidas en el modelo de agrupación en clústeres. Los histogramas de cada atributo muestran cómo se distribuye el atributo entre los clústeres identificados por el algoritmo.  
  
 **Estados**  
 Proporciona una clave que denota qué color representa cada estado en la fila de clústeres correspondiente, o un control deslizante con rombo que indica la distribución de los valores numéricos continuos. Puede mostrar u ocultar esta columna mediante la casilla **Mostrar leyenda** .  
  
 **Perfiles del clúster**  
 Esta sección contiene una columna para cada clúster del modelo. Para cada atributo, el histograma muestra la distribución de los valores en el atributo solo para ese clúster. El gráfico también tiene una columna para **Población**, que también utiliza histogramas para mostrar la distribución de valores de cada atributo, pero para todos los casos del modelo.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
