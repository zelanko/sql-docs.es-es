---
description: Subset (MDX)
title: Subconjunto (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0b7e79ebf0415011665ae63e7b9699200e374b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386731"
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
  
 *Recuento*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
## <a name="remarks"></a>Observaciones  
 En el conjunto especificado, la función **subset** devuelve un subconjunto que contiene el número especificado de tuplas, comenzando en la posición inicial especificada. La posición inicial está basada en un índice basado en cero; es decir que cero (0) corresponde a la primera tupla del conjunto especificado, 1 corresponde a la segunda y así sucesivamente.  
  
 Si no se especifica *Count* , la función devuelve todas las tuplas desde el *principio* hasta el final del conjunto.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la medida Reseller Sales de las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. La función **subset** se utiliza para devolver solo los cinco primeros conjuntos del resultado después de que el resultado se ordene mediante la función **Order** .  
  
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
  
  
