---
title: Pestaña características del clúster de clústeres de secuencia (visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.characteristics.f1
ms.assetid: 3a9e8a0c-7d03-47cc-8625-e68d73a8c947
author: minewiskan
ms.author: owend
ms.openlocfilehash: f82bab25b25c8d27e1aad2e2692d9ca519c9269b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940766"
---
# <a name="sequence-clustering-cluster-characteristics-tab-mining-model-viewer"></a>Pestaña Características de la agrupación en clústeres de secuencia (Visor de modelos de minería de datos)
  La pestaña **Características del clúster** en el **Visor de agrupación en clústeres de secuencia de Microsoft** proporciona una lista detallada de las características que definen un clúster de secuencia. Esas características pueden incluir pares de atributo-valor simples, así como transiciones entre los estados.  
  
 Utilice esta vista de un modelo de agrupación en clústeres de secuencia para obtener detalles del contenido del clúster, y vea las secuencias que son representativas de un clúster.  
  
 **Para más información:** [Algoritmo de clústeres de secuencia de Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor que desee usar para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado o el **Visor de árbol de contenido genérico de Microsoft**. También puede utilizar visores de complemento si están disponibles.  
  
 **Por**  
 Elija el clúster que desea ver.  
  
 **Características de\<Cluster>**  
 Esta tabla proporciona una lista de las secuencias que se asignaron al clúster actual, ordenadas por probabilidad. Recuerde que una secuencia es básicamente una par de atributo-valor, seguido de uno o varios pares de atributo-valor adicionales. La combinación de secuencias y sus probabilidades son las características que definen cada clúster.  
  
 Por ejemplo, en un modelo de agrupación en clústeres de secuencia basado en el análisis de la cesta de la compra, un clúster podría tener como su característica superior un cliente que elija el elemento de venta y, a continuación, finalice la transacción sin comprar nada. En un modelo de agrupación en clústeres de secuencia que busca analizar los errores del servidor, las características primarias de un clúster podrían ser una serie de eventos de error de gran frecuencia.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variable**|Esta columna indica si la característica es un valor o una transición.<br /><br /> Si la característica es un valor, la columna **variable** contiene el nombre del atributo.<br /><br /> Si la característica representa una transición de estado, la columna **variable** contiene el texto "transiciones".|  
|**Valores**|El valor de esta columna depende de si la característica es una par de atributo-valor simple, o una transición de estado que representa una secuencia común de elementos o eventos.<br /><br /> Si la característica es un valor, la columna **valor** contiene el estado.<br /><br /> Si la característica representa una transición de estado, la columna **valor** contiene la descripción de la transición de estado.|  
|**Probabilidad**|Esta columna muestra una barra que indica la probabilidad relativa de que esta característica (un par de atributo-valor simple o alguna combinación de estados) sea miembro del clúster actual.<br /><br /> Puede situar el mouse sobre el par para mostrar el valor de frecuencia de la característica.|  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
