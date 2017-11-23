---
title: HEAD (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: HEAD
dev_langs: kbMDX
helpviewer_keywords: Head function
ms.assetid: 2a909bda-1366-4537-93b0-c089554fc11f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fa23c17ba90453c735c41782c208f388d706f434
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="head-mdx"></a>Head (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el primer número de elementos especificado en un conjunto y retiene los duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recuento*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
## <a name="remarks"></a>Comentarios  
 El **Head** función devuelve el número especificado de tuplas desde el principio del conjunto especificado. Se conserva el orden de los elementos. El valor predeterminado de Count es 1. Si el número especificado de tuplas es menor que 1, el **Head** función devuelve un conjunto vacío. Si el número especificado de tuplas supera al número de tuplas del conjunto, la función devuelve el conjunto original.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. El **Head** función se utiliza para devolver sólo los 5 primeros conjuntos del resultado después de que el resultado se ordena mediante la **orden** función.  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Final &#40; MDX &#41;](../mdx/tail-mdx.md)   
 [Elemento &#40; Tupla &#41; &#40; MDX &#41;](../mdx/item-tuple-mdx.md)   
 [Elemento &#40; Miembro &#41; &#40; MDX &#41;](../mdx/item-member-mdx.md)   
 [Rango &#40; MDX &#41;](../mdx/rank-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
