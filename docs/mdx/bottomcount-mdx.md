---
title: BottomCount (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd09c823e09270ebf7c9851b3c6760baf720db39
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016950"
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
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión numérica, esta función ordena las tuplas del conjunto especificado de acuerdo con el valor de la expresión numérica especificada según se ha evaluado sobre un conjunto, en orden ascendente. A continuación, la función **BottomCount** devuelve el número especificado de tuplas con el valor más bajo.  
  
> [!IMPORTANT]  
>  La función **BottomCount** , al igual que la función [topcount](../mdx/topcount-mdx.md) , siempre rompe la jerarquía.  
  
 Si no se especifica una expresión numérica, la función devuelve el conjunto de miembros en orden natural, sin ninguna ordenación, de forma similar a la función [tail (MDX)](../mdx/tail-mdx.md) .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
