---
title: Restringir la consulta con la consulta y el eje segmentador (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f4da2bc11823704012491552c077534f3348c779
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>Ejes de segmentación de datos - restringir la consulta y consulta MDX
  Cuando se formula una instrucción SELECT de Expresiones multidimensionales (MDX), una aplicación normalmente examina un cubo y divide el conjunto de jerarquías en dos subconjuntos:  
  
-   **Ejes de consulta**: conjunto de jerarquías a partir del cual se recuperan los datos para diversos miembros. Para obtener más información sobre los ejes de consulta, vea [Especificar el contenido de un eje de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   **Eje segmentador**: conjunto de jerarquías a partir del cual se recuperan los datos para un solo miembro. Para obtener más información sobre el eje segmentador, vea [Especificar el contenido de un eje de división en sectores &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
 Como los ejes de consulta y segmentador pueden construirse a partir de varias jerarquías del cubo que se va a consultar, estos términos se utilizan para diferenciar las jerarquías que emplea el cubo que se va a consultar de las jerarquías creadas en el cubo que devuelve una consulta de MDX.  
  
 Para ver un sencillo ejemplo del uso de los ejes de consulta y segmentador, consulte [Usar los ejes de consulta y segmentador en un ejemplo simple &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

