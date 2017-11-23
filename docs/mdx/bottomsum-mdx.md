---
title: BottomSum (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: BOTTOMSUM
dev_langs: kbMDX
helpviewer_keywords: BottomSum function
ms.assetid: b3b10e68-2a36-4c38-85f4-3bb7917d5ae8
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e7175a655406dd27f11c2594ad53dfc233a6c1a9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ordena un conjunto especificado de forma ascendente y devuelve un conjunto de tuplas con los valores más bajos cuya suma es igual o inferior a un valor especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BottomSum(Set_Expression, Value, Numeric_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Valor*  
 Expresión numérica válida que especifica el valor con el que se compara cada tupla.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 El **BottomSum** función calcula la suma de una medida especificada evaluada sobre un conjunto especificado, ordenando el conjunto en orden ascendente. A continuación, la función devuelve los elementos con los valores más bajos cuyo total de la expresión numérica especificada es al menos el valor especificado (suma). Esta función devuelve el subconjunto más pequeño de un conjunto cuyo total acumulado es al menos el valor especificado. Los elementos devueltos se ordenan de menor a mayor.  
  
> [!IMPORTANT]  
>  El **BottomSum** funcione, al igual que el [TopSum](../mdx/topsum-mdx.md) , siempre rompe la jerarquía.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve, para la categoría Bike, el conjunto más pequeño de miembros del nivel City de la jerarquía Geography de la dimensión Geography para el año fiscal 2003, cuyo total acumulado mediante la medida Reseller Sales Amount es al menos la suma de 50.000 (empezando por los miembros de este conjunto que tengan la cifra de ventas más baja):  
  
 `SELECT`  
  
 `[Product].[Product Categories].Bikes ON 0,`  
  
 `BottomSum`  
  
 `({[Geography].[Geography].[City].Members}`  
  
 `, 50000`  
  
 `, ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)`  
  
 `) ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
