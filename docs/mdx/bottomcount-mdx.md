---
title: BottomCount (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 424c928f64b784070520f4cebe450dd5465fea41
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739784"
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)


  Ordena un conjunto de forma ascendente y devuelve el número especificado de tuplas del conjunto especificado con los valores más bajos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recuento*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Notas  
 Si se especifica una expresión numérica, esta función ordena las tuplas del conjunto especificado de acuerdo con el valor de la expresión numérica especificada según se ha evaluado sobre un conjunto, en orden ascendente. El **BottomCount** función, a continuación, devuelve el número especificado de tuplas con el valor más bajo.  
  
> [!IMPORTANT]  
>  El **BottomCount** funcione, al igual que el [TopCount](../mdx/topcount-mdx.md) , siempre rompe la jerarquía.  
  
 Si no se especifica una expresión numérica, la función devuelve el conjunto de miembros en orden natural, sin ordenamiento, comportándose como la [Tail (MDX)](../mdx/tail-mdx.md) (función).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la medida Reseller Order Quantity por cada año para las cinco ventas inferiores Product SubCategory, ordenadas de acuerdo con la medida Reseller Sales Amount.  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
