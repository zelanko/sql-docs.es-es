---
title: Valor (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Value
dev_langs:
- kbMDX
helpviewer_keywords:
- Value function
ms.assetid: ff76628e-2d49-49f6-a6cb-f6da07d83d65
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63e24e0f701332747e3129a57768bfe1b6fbb45d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="value-mdx"></a>Value (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el valor del miembro actual de la dimensión de medidas que forma intersección con el miembro actual de las jerarquías de atributo en el contexto de la consulta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **valor** función devuelve el valor del miembro especificado como una cadena. El **valor** argumento es opcional porque el valor de un miembro es la propiedad predeterminada de un miembro y es el valor devuelto para un miembro si no se especifica ningún otro valor. Para obtener más información acerca de las propiedades de miembros, vea [propiedades de miembro intrínsecas &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) y [propiedades de miembro definidas por el usuario &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
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
 [MemberValue &#40; MDX &#41;](../mdx/membervalue-mdx.md)   
 [Propiedades &#40; MDX &#41;](../mdx/properties-mdx.md)   
 [Nombre de &#40; MDX &#41;](../mdx/name-mdx.md)   
 [UniqueName &#40; MDX &#41;](../mdx/uniquename-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

