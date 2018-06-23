---
title: Restringir la consulta con ejes de consulta y segmentador (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e727b432afec1f42a6a111442c2263d6c48784de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200819"
---
# <a name="restricting-the-query-with-query-and-slicer-axes-mdx"></a>Restringir la consulta con ejes de consulta y segmentador (MDX)
  Cuando se formula una instrucción SELECT de Expresiones multidimensionales (MDX), una aplicación normalmente examina un cubo y divide el conjunto de jerarquías en dos subconjuntos:  
  
-   **Ejes de consulta**: conjunto de jerarquías a partir del cual se recuperan los datos para diversos miembros. Para obtener más información sobre los ejes de consulta, vea [Especificar el contenido de un eje de consulta &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   **Eje segmentador**: conjunto de jerarquías a partir del cual se recuperan los datos para un solo miembro. Para obtener más información sobre el eje segmentador, vea [Especificar el contenido de un eje de división en sectores &#40;MDX&#41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
 Como los ejes de consulta y segmentador pueden construirse a partir de varias jerarquías del cubo que se va a consultar, estos términos se utilizan para diferenciar las jerarquías que emplea el cubo que se va a consultar de las jerarquías creadas en el cubo que devuelve una consulta de MDX.  
  
 Para ver un sencillo ejemplo del uso de los ejes de consulta y segmentador, consulte [Usar los ejes de consulta y segmentador en un ejemplo simple &#40;MDX&#41;](mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [Aspectos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  