---
title: Valor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f373f626d778c4d77ec5843dca5bb11da728451d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68887442"
---
# <a name="value-mdx"></a>Value (MDX)


  Devuelve el valor del miembro actual de la dimensión de medidas que forma intersección con el miembro actual de las jerarquías de atributo en el contexto de la consulta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **Value** devuelve el valor del miembro especificado como una cadena. El argumento de **valor** es opcional porque el valor de un miembro es la propiedad predeterminada de un miembro y es el valor que se devuelve para un miembro si no se especifica ningún otro valor. Para obtener más información acerca de las propiedades de los miembros, vea [propiedades de miembro intrínsecas &#40;&#41;MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) y [propiedades de miembro definidas por el usuario &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties).  
  
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
  
## <a name="see-also"></a>Consulte también  
 [&#41;MemberValue &#40;MDX](../mdx/membervalue-mdx.md)   
 [Propiedades &#40;&#41;MDX](../mdx/properties-mdx.md)   
 [Nombre &#40;&#41;MDX](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
