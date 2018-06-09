---
title: Valor (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6eb91bb43407311a58e495b5f9391186821d3a67
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743844"
---
# <a name="value-mdx"></a>Value (MDX)


  Devuelve el valor del miembro actual de la dimensión de medidas que forma intersección con el miembro actual de las jerarquías de atributo en el contexto de la consulta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 El **valor** función devuelve el valor del miembro especificado como una cadena. El **valor** argumento es opcional porque el valor de un miembro es la propiedad predeterminada de un miembro y es el valor devuelto para un miembro si no se especifica ningún otro valor. Para obtener más información acerca de las propiedades de miembros, vea [propiedades de miembro intrínsecas &#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) y [propiedades de miembro definidas por el usuario &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el valor de un miembro además de devolver explícitamente el nombre del miembro.  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve el valor de un miembro como el valor predeterminado devuelto para un miembro en un eje.  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [Propiedades &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Nombre &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
