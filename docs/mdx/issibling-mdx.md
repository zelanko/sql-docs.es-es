---
title: IsSibling (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0db66d425acbcf24636e5db78a3a825b62a4fbef
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578817"
---
# <a name="issibling-mdx"></a>IsSibling (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Informa de si un miembro especificado está en el mismo nivel que otro miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression1*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Member_Expression2*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 El **IsSibling** función devuelve **true** si el primer miembro especificado está en un elemento relacionado del segundo miembro especificado. En caso contrario, la función devuelve **false**.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo devuelve TRUE si el miembro actual en la jerarquía Fiscal de la dimensión Date es un elemento relacionado de julio 2002:  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
