---
title: "Creación de cálculos de celdas en MDX (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c38088beea623b224ea2e5af1225ad78acf62576
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-cell-calculations---build-cell-calculations"></a>Cálculos de celdas MDX - cálculos de celdas de compilación
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Expresiones multidimensionales (MDX) proporciona una variedad de herramientas para generar los valores calculados, como los miembros calculados, resúmenes personalizados y miembros personalizados. Sin embargo, es difícil que estas características puedan afectar en este tema a un determinado conjunto de celdas o incluso a una sola.  
  
 Para generar valores calculados para celdas específicas, es necesario utilizar las características de celdas calculadas en MDX. Las celdas calculadas permiten definir un determinado segmento de celdas, denominado *subcubo de cálculo*, y aplicar una fórmula a todas y cada una de las celdas del subcubo de cálculo, sujeto a una condición opcional que puede aplicarse a cada celda.  
  
 Las celdas calculadas también ofrecen funcionalidades complejas, como las fórmulas de búsqueda de objetivos (como se usan en los KPI) o las fórmulas de análisis especulativos. Este nivel de funcionalidad proviene de la característica de orden de paso de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que permite realizar pasos recursivos con las celdas calculadas mediante fórmulas de cálculo aplicadas en pasos específicos del orden de paso. Para más información sobre el orden de paso, vea [Descripción de orden de paso y orden de resolución &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 En términos del ámbito de creación, las celdas calculadas similares a los conjuntos con nombre y los miembros calculados en dichas celdas calculadas pueden crearse temporalmente para la duración de una sesión o una sola consulta, o bien pueden estar disponibles de manera global como parte de un cubo:  
  
-   **Ámbito de consulta** Para crear una celda calculada que se defina como parte de una consulta MDX y cuyo ámbito, por lo tanto, esté limitado a la consulta, use la palabra clave WITH. A continuación puede utilizar la celda calculada en una instrucción MDX SELECT. Con este enfoque, la celda calculada creada con la palabra clave **WITH** puede cambiarse sin que ello tenga ningún impacto en la instrucción SELECT.  
  
     Para más información sobre el uso de la palabra clave WITH para crear miembros calculados, vea [Crear cálculos de celdas del ámbito de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md).  
  
-   **Ámbito de sesión** Para crear un miembro calculado cuyo ámbito sea más amplio que el contexto de la consulta (es decir, cuyo ámbito sea la duración de la sesión MDX) puede usar las instrucciones CREATE CELL CALCULATION o ALTER CUBE.  
  
     Para más información sobre el uso de las instrucciones CREATE CELL CALCULATION o ALTER CUBE para crear celdas calculadas en una sesión, vea [Crear celdas calculadas de ámbito de sesión](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER CUBE &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-definition-alter-cube.md)   
 [CREATE CELL CALCULATION instrucción &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Creación de cálculos de celdas del ámbito de consulta &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
