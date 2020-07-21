---
title: Topcount (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0f607f3111c150bff3d5dc562c77901a381bedc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036601"
---
# <a name="topcount-mdx"></a>TopCount (MDX)


  Ordena un conjunto de forma descendente y devuelve el número de elementos especificado con los valores más altos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recuento*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión numérica, la función **topcount** ordena, en orden descendente, las tuplas del conjunto especificado por el conjunto especificado de acuerdo con el valor especificado por la expresión numérica, según se ha evaluado en el conjunto especificado. Después de ordenar el conjunto, la función **topcount** devuelve el número de tuplas especificado con el valor más alto.  
  
> [!IMPORTANT]  
>  Al igual que la función [BottomCount](../mdx/bottomcount-mdx.md) , la función **topcount** siempre rompe la jerarquía.  
  
 Si no se especifica una expresión numérica, la función devuelve el conjunto de miembros en orden natural, sin ninguna ordenación, como la función de [encabezado (MDX)](../mdx/head-mdx.md) .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelven las 10 fechas superiores según Internet Sales Amount:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 El ejemplo siguiente devuelve, para la categoría Bike, los primeros cinco miembros del conjunto que contiene todas las combinaciones de miembros del nivel City de la jerarquía Geography de la dimensión Geography y los años fiscales de la jerarquía Fiscal de la dimensión Date, ordenados por la medida Reseller Sales Amount (comenzando por los miembros de este conjunto con la mayor cifra de ventas).  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
