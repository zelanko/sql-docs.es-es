---
title: Recuento (tupla) (MDX) | Documentos de Microsoft
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
ms.assetid: c8f4a570-54a8-4c00-ac4b-eef0ebdb353c
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2df1e6b6c68f584b2dc2a28cda03caf766ad456b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="count-tuple-mdx"></a>Count (Tuple) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [Recuento de &#40;dimensión&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Recuento de &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Número de & #40; Conjunto de & #41; & #40; MDX & #41;](../mdx/count-set-mdx.md)   
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
