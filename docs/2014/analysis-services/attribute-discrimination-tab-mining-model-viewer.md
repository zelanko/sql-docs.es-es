---
title: Pestaña distinción del (Visor de modelos de minería de datos) del atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.discrimination.f1
ms.assetid: 68323f23-121e-44fc-be85-6f9915d6d3c7
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e661e6a993639d3eac86bd5fb45f607ba8d346f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161526"
---
# <a name="attribute-discrimination-tab-mining-model-viewer"></a>Pestaña Distinción del atributo (Visor de modelos de minería de datos)
  Utilice la pestaña **Distinción del atributo** para comparar los estados de los atributos de entrada y ver cómo se relacionan con el atributo de resultados. Los valores de atributo que permiten diferenciar en mayor medida los dos estados de atributo de predicción se enumeran en primer lugar.  
  
 **Para más información:** [Algoritmo Bayes naive de Microsoft](data-mining/microsoft-naive-bayes-algorithm.md), [Examinar un modelo usando el visor Bayes naive de Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos de los de la estructura de minería de datos actual. El modelo de minería de datos se abre automáticamente en el visor personalizado correcto.  
  
 **Visor**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Para cada modelo, puede elegir el visor personalizado o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede utilizar visores de complemento si están disponibles.  
  
 **Atributo**  
 Elija un atributo de predicción.  
  
 **Valor 1**  
 Elija un estado del atributo de predicción para compararlo con el estado contenido en el **Valor 2**.  
  
 **Valor 2**  
 Seleccione un estado del atributo de predicción para compararlo con el estado contenido en el **Valor 1**. También puede seleccionar **Todos los otros estados** para comparar el valor de **Valor 1** con su complemento, es decir, todos los otros valores excepto Valor 1.  
  
 **Puntuaciones de distinción para \<valor 1 > y \<valor 2 >**  
 El gráfico contiene las siguientes columnas, que describen cómo se relaciona el atributo de destino con los estados específicos del atributo de entrada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Atributos**|Un atributo de entrada en el modelo de minería de datos.|  
|**Valores**|Un estado del atributo que se incluye en **Atributos**.|  
|**Favorece \<valor 1 >**|La barra indica si el atributo y valor actuales favorecen el resultado de destino seleccionado en **Valor 1**.|  
|**Favorece \<valor 2 >**|La barra indica si el atributo y valor actuales favorecen el resultado de destino seleccionado en **Valor 2.**|  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
