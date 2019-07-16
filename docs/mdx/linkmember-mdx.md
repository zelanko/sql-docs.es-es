---
title: LinkMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a00388e067878d9c2165cbae6844f8020b7c63e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905602"
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)


  Devuelve el miembro equivalente a un miembro especificado de una jerarquía especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 El **LinkMember** función devuelve el miembro de la jerarquía especificada que coincide con los valores de clave en cada nivel del miembro especificado en la jerarquía relacionada. Los atributos de cada nivel deben tener la misma cardinalidad de clave y tipo de datos. En las jerarquías no naturales, si existe más de una coincidencia para el valor clave de un atributo, el resultado será un error o indeterminado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el **LinkMember** función para devolver la medida predeterminada del cubo Adventure Works para los antecesores del miembro 1 de July de 2002 de la jerarquía de atributo Date.Date de la jerarquía Calendar.  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [Ascendants &#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
