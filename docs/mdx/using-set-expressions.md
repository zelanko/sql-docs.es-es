---
title: Usar expresiones de conjuntos | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1588d955e728830da4417160591a5c2b6c231473
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893502"
---
# <a name="using-set-expressions"></a>Usar expresiones de conjunto


  Un conjunto está formado por una lista ordenada de cero o más tuplas. Los conjuntos que no contienen tuplas se denominan conjuntos vacíos.  
  
 La expresión completa de un conjunto consta de cero o más tuplas especificadas explícitamente entre corchetes:  
  
 {[{ *Tuple_expression* | *Member_expression* } [, { *Tuple_expression* | *Member_expression* }]...]}  
  
 Las expresiones de miembro especificadas en expresiones de conjunto se convierten en expresiones de tupla de un miembro.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestran dos expresiones de conjunto que se utilizan en los ejes de columnas y de filas de una consulta:  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]} ON COLUMNS,`  
  
 `{([Product].[Product Categories].[Category].&[4], [Date].[Calendar].[Calendar Year].&[2004]),`  
  
 `([Product].[Product Categories].[Category].&[1], [Date].[Calendar].[Calendar Year].&[2003]),`  
  
 `([Product].[Product Categories].[Category].&[3], [Date].[Calendar].[Calendar Year].&[2004])}`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 En el eje de columnas, el conjunto  
  
 {[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}  
  
 está compuesto de dos miembros de dimensión Measures. En el eje de filas, el conjunto  
  
 {([Product]. [Categorías de producto]. [Category]. & [4], [Date]. [Calendar]. [Año natural]. & [2004]),  
  
 ([Product]. [Categorías de producto]. [Category]. & [1], [Date]. [Calendar]. [Año natural]. & [2003]),  
  
 ([Product]. [Categorías de producto]. [Category]. & [3], [Date]. [Calendar]. [Año natural]. & [2004])}  
  
 está compuesto de tres tuplas, cada una de las cuales contiene dos referencias explícitas a miembros de la jerarquía Product Categories de la dimensión Product y de la jerarquía Calendar de la dimensión Date.  
  
 Para obtener ejemplos de funciones que devuelven conjuntos, vea [trabajar con miembros, tuplas y conjuntos &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx).  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;&#41;MDX](../mdx/expressions-mdx.md)  
  
  
