---
title: Recuento (tupla) (MDX) | Documentos de Microsoft
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
ms.assetid: c8f4a570-54a8-4c00-ac4b-eef0ebdb353c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 99f6bd3cb046f49d27b019fb6f0e5128d47d55db
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="count-tuple-mdx"></a>Count (Tuple) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de dimensiones de una tupla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
## <a name="remarks"></a>Comentarios  
 Devuelve el número de dimensiones de una tupla.  
  
## <a name="example"></a>Ejemplo  
 La medida calculada en la siguiente consulta devuelve el valor 2, que es el número de jerarquías presente en la tupla `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])`:  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Número de &#40; dimensión &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)   
 [Número de &#40; Niveles de jerarquía &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Número de &#40; Conjunto de &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
