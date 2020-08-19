---
description: LinkMember (MDX)
title: LinkMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 81d8d87caa0c844bd2754ba2d044936d43f8d48a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429867"
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
  
## <a name="remarks"></a>Observaciones  
 La función **LinkMember** devuelve el miembro de la jerarquía especificada que coincide con los valores de clave en cada nivel del miembro especificado en una jerarquía relacionada. Los atributos de cada nivel deben tener la misma cardinalidad de clave y tipo de datos. En las jerarquías no naturales, si existe más de una coincidencia para el valor clave de un atributo, el resultado será un error o indeterminado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa la función **LinkMember** para devolver la medida predeterminada del cubo Adventure Works para los antecesores del miembro 1 de julio de 2002 de la jerarquía de atributo Date. Date de la jerarquía Calendar.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Jerarquía &#40;&#41;MDX ](../mdx/hierarchize-mdx.md)   
 [Antecesores &#40;&#41;MDX ](../mdx/ascendants-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
