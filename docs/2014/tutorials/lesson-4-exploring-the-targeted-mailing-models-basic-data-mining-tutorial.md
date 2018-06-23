---
title: 'Lección 4: Explorar los modelos de correo directo (Tutorial de minería de datos básicos) | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
caps.latest.revision: 51
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 57ebae0dfb1e8f472647818cad2c8f724e8b3c0e
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313182"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>Lección 4: Explorar los modelos de correo directo (tutorial básico de minería de datos)
  Una vez procesados los modelos del proyecto, puede explorarlos para buscar tendencias interesantes. Puesto que los patrones pueden ser complejos y difíciles simplemente examinando números, Minería de datos de SQL Server proporciona algunas herramientas visuales que le ayudan a investigar los datos y entender las reglas y relaciones que los algoritmos han detectado en los datos. También puede utilizar diversas pruebas de precisión para validar el conjunto de datos o detectar qué modelo funciona mejor antes de implementarlo.  
  
 Cuando usas [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para explorar los modelos, cada modelo creado aparece en el **Visor de modelos de minería de datos** ficha en el Diseñador de minería de datos. Puede usar los visores para explorar los modelos. Estos visores también están disponibles en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Cada algoritmo usado para crear un modelo en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] devuelve un tipo de resultado diferente. Por tanto, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona visores personalizados para cada tipo de modelo de aprendizaje automático.  
  
 Si desea obtener detalles, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] también proporciona un visor HTML, denominado el **Visor de árbol de contenido genérico**, que muestra información detallada sobre el modelo de datos y los patrones que se encontraron, en un formato semitabular. Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
 En esta lección examinará los resultados de los tres modelos. Cada tipo de modelo se basa en un algoritmo diferente y proporciona visiones diferentes de los datos.  
  
-   El modelo Árbol de decisión le indica los factores que influyen en la compra de bicicletas.  
  
-   El modelo Agrupación en clústeres agrupa los clientes por atributos, como el comportamiento de compra de bicicletas y otros atributos seleccionados.  
  
-   El modelo Bayes naive le permite examinar las relaciones entre los diferentes atributos.  
  
 Vea los temas siguientes para obtener más información sobre cada uno de los visores de modelos de minería de datos.  
  
-   [Explorar el modelo de árbol de decisión &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo de agrupación en clústeres &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo de Bayes Naive &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 Los tres modelos se pueden ver con el **Visor de árbol de contenido genérico**para extraer fórmulas, valores de datos y así sucesivamente.  
  
## <a name="first-task-in-lesson"></a>Primera tarea de la lección  
 [Explorar el modelo de árbol de decisión &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>Lección anterior  
 [Lección 3: Agregar y procesar los modelos](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 5: Probar los modelos &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas del Visor de modelo de minería de datos](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Visores de modelos de minería de datos](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  