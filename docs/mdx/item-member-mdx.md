---
title: Elemento (miembro) (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92745085a408503a2b435eb160daf431c7fdaa32
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740344"
---
# <a name="item-member-mdx"></a>Item (Member) (MDX)


  Devuelve un miembro de una tupla especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
 *Index*  
 Expresión numérica válida que especifica el miembro concreto mediante la posición en la tupla que se devolverá.  
  
## <a name="remarks"></a>Notas  
 El **elemento** función devuelve un miembro de la tupla especificada. La función devuelve el miembro que se encuentra en la posición de base cero especificada por *índice*.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se devuelve el miembro `[2003]` (el primer elemento de la tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).`) en columnas:  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
