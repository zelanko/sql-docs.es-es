---
title: Restringir la consulta con la consulta y el eje segmentador (MDX) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4de964dcfa7bad1f307de12e81593c93bcd8e859
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020782"
---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>Ejes de segmentación de datos - restringir la consulta y consulta MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Cuando se formula una instrucción SELECT de Expresiones multidimensionales (MDX), una aplicación normalmente examina un cubo y divide el conjunto de jerarquías en dos subconjuntos:  
  
-   **Ejes de consulta**: conjunto de jerarquías a partir del cual se recuperan los datos para diversos miembros. Para obtener más información sobre los ejes de consulta, vea [Especificar el contenido de un eje de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   **Eje segmentador**: conjunto de jerarquías a partir del cual se recuperan los datos para un solo miembro. Para obtener más información sobre el eje segmentador, vea [Especificar el contenido de un eje de división en sectores &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
 Como los ejes de consulta y segmentador pueden construirse a partir de varias jerarquías del cubo que se va a consultar, estos términos se utilizan para diferenciar las jerarquías que emplea el cubo que se va a consultar de las jerarquías creadas en el cubo que devuelve una consulta de MDX.  
  
 Para ver un sencillo ejemplo del uso de los ejes de consulta y segmentador, consulte [Usar los ejes de consulta y segmentador en un ejemplo simple &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con miembros, tuplas y conjuntos de & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Aspectos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
