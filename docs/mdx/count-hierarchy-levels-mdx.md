---
title: "Count (niveles de jerarquía) (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 3de6a824-2ff3-47ac-9ceb-e3369a04f35d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ca18ec4161db5405055a3732007170167afc123c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="count-hierarchy-levels-mdx"></a>Count (niveles de jerarquía) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de niveles de una jerarquía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 Devuelve el número de niveles de una jerarquía, incluido, si procede, el nivel `[All]`.  
  
> [!IMPORTANT]  
>  Cuando una dimensión contiene solo una única jerarquía visible, se puede hacer referencia a la jerarquía por el nombre de la dimensión o por el nombre de la jerarquía, dado que el nombre de la dimensión se resuelve en su única jerarquía visible. Por ejemplo, `Measures.Levels.Count` es una expresión MDX válida debido a que se resuelve en la única jerarquía de la dimensión Measures.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve un recuento del número de niveles de la jerarquía definida por el usuario Product Categories del cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Número de &#40; dimensión &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)   
 [Número de &#40; Tupla &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)   
 [Número de &#40; Conjunto de &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
