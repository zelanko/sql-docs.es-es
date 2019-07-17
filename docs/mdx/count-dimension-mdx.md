---
title: Count (dimensión) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b84c5a1902e80f8abe3828f4be1b5d570ec026ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104811"
---
# <a name="count-dimension-mdx"></a>Count (Dimension) (MDX)


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
 [Recuento &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Recuento &#40;los niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
