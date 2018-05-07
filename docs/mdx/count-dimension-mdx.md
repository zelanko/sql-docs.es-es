---
title: Recuento (Dimension) (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: 4b9c52f6-5bb0-401a-947c-e14134558b4a
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 486b867456bff282801302293ec715d595924ba0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="count-dimension-mdx"></a>Count (Dimension) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el número de jerarquías de un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Comentarios  
 Devuelve el número de jerarquías de un cubo, incluida la jerarquía `[Measures].[Measures]`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el número de jerarquías del cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Recuento de &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Recuento de &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Número de & #40; Conjunto de & #41; & #40; MDX & #41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
