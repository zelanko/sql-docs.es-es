---
description: Count (Dimension) (MDX)
title: Count (dimensión) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: afa58c330210e4fdb34d13892101e210f54cd3bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429967"
---
# <a name="count-dimension-mdx"></a>Count (Dimension) (MDX)


  Devuelve el número de jerarquías de un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Observaciones  
 Devuelve el número de jerarquías de un cubo, incluida la jerarquía `[Measures].[Measures]`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el número de jerarquías del cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Count &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Recuento &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;establecer&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
