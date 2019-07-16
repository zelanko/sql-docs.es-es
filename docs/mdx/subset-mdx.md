---
title: Subconjunto (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b1f9a79c0e0ba6d578b82d7b1d072f3543888a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036701"
---
# <a name="subset-mdx"></a>Subset (MDX)


  Devuelve un subconjunto de tuplas a partir de un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Iniciar*  
 Expresión numérica válida que especifica la posición de la primera tupla que será devuelta.  
  
 *Count*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
## <a name="remarks"></a>Comentarios  
 Desde el conjunto especificado, el **subconjunto** función devuelve un subconjunto que contiene el número especificado de tuplas, comenzando por la posición de inicio especificada. La posición inicial está basada en un índice basado en cero; es decir que cero (0) corresponde a la primera tupla del conjunto especificado, 1 corresponde a la segunda y así sucesivamente.  
  
 Si *recuento* no se especifica, la función devuelve todas las tuplas desde *iniciar* hasta el final del conjunto.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la medida Reseller Sales de las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. El **subconjunto** función se utiliza para devolver solo los cinco primeros conjuntos del resultado después de que el resultado se ordena mediante la **orden** función.  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
