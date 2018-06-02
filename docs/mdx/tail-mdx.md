---
title: Tail (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5192deedcb6085767fc00f68bb17f6adddb38679
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581247"
---
# <a name="tail-mdx"></a>Tail (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un subconjunto del final de un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recuento*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
## <a name="remarks"></a>Notas  
 El **final** función devuelve el número especificado de tuplas desde el final del conjunto especificado. Se conserva el orden de los elementos. El valor predeterminado de *recuento* es 1. Si el número especificado de tuplas es menor que 1, la función devuelve un conjunto vacío. Si el número especificado de tuplas supera al número de tuplas del conjunto, la función devuelve el conjunto original.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la medida Reseller Sales de las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. El **final** función se utiliza para devolver solo los últimos cinco conjuntos del resultado después de que el resultado se ha ordenado inversamente mediante la **orden** función.  
  
```  
SELECT Tail  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BASC  
      )  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
