---
description: TopSum (MDX)
title: TopS (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 665a1ace9df98303da19b861cdd3ce6340ec8368
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412920"
---
# <a name="topsum-mdx"></a>TopSum (MDX)


  Ordena un conjunto y devuelve los elementos de nivel superior cuyo total acumulado sea igual o superior a un valor especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopSum(Set_Expression, Value, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Valor*  
 Expresión numérica válida que especifica el valor con el que se compara cada tupla.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX (Expresiones multidimensionales) que devuelve una medida.  
  
## <a name="remarks"></a>Observaciones  
 La función **topse** calcula la suma de una medida especificada evaluada sobre un conjunto especificado, ordenando el conjunto en orden descendente. A continuación, la función devuelve los elementos con los valores más altos cuyo total de la expresión numérica especificada sea al menos el valor especificado. Esta función devuelve el subconjunto más pequeño de un conjunto cuyo total acumulado es al menos el valor especificado. Los elementos devueltos se ordenan de mayor a menor.  
  
> [!IMPORTANT]  
>  Al igual que la función [BottomSum](../mdx/bottomsum-mdx.md) , la función de **topsing** siempre rompe la jerarquía.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve, para la categoría Bike, el conjunto más pequeño de miembros del nivel City de la jerarquía Geography de la dimensión Geography cuyo total acumulado mediante la medida Reseller Sales Amount sea al menos la suma de 6.000.000 (empezando con los miembros de este conjunto que tengan la cifra de ventas más alta).  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopSum  
   ({[Geography].[Geography].[City].Members}  
   , 6000000  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
