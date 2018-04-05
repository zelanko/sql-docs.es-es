---
title: SetToArray (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SETTOARRAY
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToArray function
ms.assetid: e408c626-3a2a-4ce9-aeb4-247301334893
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7cf8bdfdb22175a59207f14792abcf7f27aede0a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="settoarray-mdx"></a>SetToArray (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Comentarios  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
