---
title: SetToArray (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e545cb4b41f1a0d60e471c15753a82079978ee5
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743314"
---
# <a name="settoarray-mdx"></a>SetToArray (MDX)


  Convierte uno o más conjuntos en una matriz, para usarla en funciones definidas por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Notas  
 El **SetToArray** función convierte uno o más conjuntos en una matriz para su uso en una función definida por el usuario. El número de dimensiones de la matriz resultante es el mismo que el número de conjuntos especificados.  
  
 La expresión numérica opcional puede proporcionar los valores en las celdas de la matriz. Si no se especifica una expresión numérica, la combinación cruzada de los conjuntos se evalúa en el contexto actual.  
  
 Las coordenadas de celda de la matriz resultante corresponden a la posición de los conjuntos en la lista. Por ejemplo, hay tres conjuntos, `SA`, `SB` y `SC`. Cada uno de ellos tiene dos elementos. La instrucción de MDX, `SetToArray(SA, SB, SC)`, crea la siguiente matriz de tres dimensiones:  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  El tipo de valor devuelto de la **SetToArray** función es el tipo VARIANT, VT_ARRAY. Por lo tanto, el resultado de la **SetToArray** función debe usarse únicamente como entrada para una función definida por el usuario.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo devuelve una matriz.  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
