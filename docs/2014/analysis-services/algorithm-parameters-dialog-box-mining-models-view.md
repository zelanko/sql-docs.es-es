---
title: Cuadro de diálogo parámetros de algoritmo (vista modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.models.algorithmparameters.f1
helpviewer_keywords:
- Algorithm Parameters dialog box
ms.assetid: 57f9f6f8-8ca4-4a6e-8f18-85f0571b7060
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c72a3c52da21ca7af10103010500bb43fd46a10a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062609"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>Parámetros de algoritmo (vista Modelos de minería de datos, cuadro de diálogo)
  Utilice el cuadro de diálogo **Parámetros de algoritmo** para ajustar parámetros de algoritmo específicos del modelo seleccionado. Al cambiar un parámetro de algoritmo, normalmente cambiará los resultados del modelo de minería de datos. La manera en que cada parámetro afecta a los resultados depende del algoritmo que se use y de los datos. Para más información, vea [Personalizar la estructura y los modelos de minería de datos](data-mining/customize-mining-models-and-structure.md).  
  
## <a name="options"></a>Opciones  
 **Los**  
 Enumera los parámetros disponibles para el modelo de minería de datos seleccionado.  
  
 La siguiente lista describe las columnas disponibles.  
  
|Columna|Descripción|  
|------------|-----------------|  
|**Parámetro**|Especifica el nombre del parámetro.|  
|**Valor**|Especifique un valor únicamente si desea cambiar el valor predeterminado del parámetro.|  
|**Predeterminada**|Especifica el valor predeterminado del parámetro que utilizará el algoritmo si no indica un valor en la columna **Valor** .|  
|**Intervalo**|Especifique el intervalo de valores posibles que puede indicar en la columna **Valor** . Los intervalos pueden ser uno de los siguientes:<br /><br /> Una lista discreta, como 1, 2, 3<br /><br /> Un intervalo inclusivo, como [0, 100]<br /><br /> Un intervalo exclusivo, como (0,...)<br /><br /> Una combinación, como [0,...)|  
  
 **Descripción**  
 Describe el parámetro seleccionado en la lista **Parámetros**.  
  
 **Add (Agregar)**  
 Haga clic para agregar a la lista parámetros específicos de algoritmo adicionales. Después de agregar el parámetro, puede indicar el nombre correcto en la columna **Parámetro** y proporcionar un valor en la columna **Valor** .  
  
 **Remove**  
 Haga clic para eliminar un parámetro personalizado de la lista.  
  
 Si elimina uno de los parámetros estándar de algoritmo de Analysis Services de la lista, el parámetro todavía se utilizará en el modelo, pero con los valores predeterminados para ese parámetro. El parámetro no se elimina permanentemente y aparecerá la próxima vez que abra el cuadro de diálogo.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Vista modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-models-view-data-mining-model-designer.md)   
 [Mover objetos de minería de datos](data-mining/moving-data-mining-objects.md)  
  
  
