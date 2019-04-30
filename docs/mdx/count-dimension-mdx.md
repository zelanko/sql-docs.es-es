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
manager: kfile
ms.openlocfilehash: 6ee8fe09f7a840d32511d3a208a4621612ee9939
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63285050"
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
  
  
