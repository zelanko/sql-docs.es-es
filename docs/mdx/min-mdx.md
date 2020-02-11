---
title: Min (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 83061ff3e9923e65f231675c1bc5b1913a5156fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114382"
---
# <a name="min-mdx"></a>Min (MDX)


  Devuelve el valor mínimo de una expresión numérica evaluada sobre un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión numérica, dicha expresión numérica se evalúa en todo el conjunto y devuelve el valor mínimo de esa evaluación. Si no se especifica una expresión numérica, el conjunto especificado se evalúa en el contexto actual de los miembros del conjunto y devuelve el valor mínimo de esa evaluación.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] omite los valores NULL al calcular el valor mínimo de un conjunto de números.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve las ventas trimestrales mínimas de cada subcategoría y cada país del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Min   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
