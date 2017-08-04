---
title: TopSum (MDX) | Documentos de Microsoft
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
- TOPSUM
dev_langs:
- kbMDX
helpviewer_keywords:
- TopSum function
ms.assetid: e32496fd-4897-43c9-a388-4028609f4ffb
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 58a7bffc672af75c52eacca28f2e83d36a56af0c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="topsum-mdx"></a>TopSum (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX (Expresiones multidimensionales) que devuelve una medida.  
  
## <a name="remarks"></a>Comentarios  
 El **TopSum** función calcula la suma de una medida especificada evaluada sobre un conjunto especificado, ordenando el conjunto en orden descendente. A continuación, la función devuelve los elementos con los valores más altos cuyo total de la expresión numérica especificada sea al menos el valor especificado. Esta función devuelve el subconjunto más pequeño de un conjunto cuyo total acumulado es al menos el valor especificado. Los elementos devueltos se ordenan de mayor a menor.  
  
> [!IMPORTANT]  
>  Al igual que el [BottomSum](../mdx/bottomsum-mdx.md) función, el **TopSum** función siempre rompe la jerarquía.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

