---
title: Max (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e805801fef4151ad6349fdeaca6e6dc62c687f3
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741934"
---
# <a name="max-mdx"></a>Max (MDX)


  Devuelve el valor máximo de una expresión numérica evaluada sobre un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Max( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Notas  
 Si se especifica una expresión numérica, dicha expresión numérica especificada se evalúa en todo el conjunto y devuelve el valor máximo de esa evaluación. Si no se especifica una expresión numérica, el conjunto especificado se evalúa en el contexto actual de los miembros del conjunto y devuelve el valor máximo de esa evaluación.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] omite los valores NULL al calcular el valor máximo de un conjunto de números.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve las ventas mensuales máximas de cada trimestre, subcategoría y país del cubo de Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Max   
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
