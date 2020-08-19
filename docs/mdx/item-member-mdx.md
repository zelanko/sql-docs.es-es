---
description: Item (Member) (MDX)
title: Elemento (miembro) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a374d1fcc7f972828832c2f82375acf640d45fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483968"
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
  
## <a name="remarks"></a>Observaciones  
 La función **Item** devuelve un miembro de la tupla especificada. La función devuelve el miembro que se encuentra en la posición basada en cero especificada por *index*.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se devuelve el miembro `[2003]` (el primer elemento de la tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).`) en columnas:  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
