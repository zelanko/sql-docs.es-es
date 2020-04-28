---
title: Count (tupla) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 486c68e1947bfad67bc0288751d03c6042cd7f3e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68047267"
---
# <a name="count-tuple-mdx"></a>Count (Tuple) (MDX)


  Devuelve el número de dimensiones de una tupla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
## <a name="remarks"></a>Observaciones  
 Devuelve el número de dimensiones de una tupla.  
  
## <a name="example"></a>Ejemplo  
 La medida calculada en la siguiente consulta devuelve el valor 2, que es el número de jerarquías presente en la tupla `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])`:  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Recuento &#40;dimensión&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Recuento &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;establecer&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
