---
title: Dimensión (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cee82f3baa95df1d8636e314bfbb0798efe9527a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741674"
---
# <a name="dimension-mdx"></a>Dimension (MDX)


  Devuelve la jerarquía que contiene un miembro, nivel o jerarquía especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
### <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el **dimensión** función, junto con el **nombre** función para devolver el nombre de la jerarquía del miembro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente utiliza la función Dimension junto con las funciones Levels y Count para devolver el número de niveles de la jerarquía que contiene el miembro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se usa el **dimensión** función, junto con el **miembros** y **recuento** funciones, para devolver el número de miembros en la jerarquía que contiene el miembro especificado.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Recuento de &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Recuento de &#40;establecer&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Niveles &#40;MDX&#41;](../mdx/levels-mdx.md)   
 [Los miembros &#40;establecer&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
