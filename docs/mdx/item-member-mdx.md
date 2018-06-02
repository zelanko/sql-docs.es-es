---
title: Elemento (miembro) (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7cb7c3825f2a319282788c222a7ebb46cec2b532
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578837"
---
# <a name="item-member-mdx"></a>Item (Member) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
