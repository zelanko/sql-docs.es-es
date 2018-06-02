---
title: Mediana (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ba13f8803e0baa10a11f8766fb6a02e2ed3ad3c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580717"
---
# <a name="median-mdx"></a>Median (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor medio de una expresión numérica evaluada sobre un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Notas  
 Si se especifica una expresión numérica, dicha expresión numérica especificada se evalúa en todo el conjunto y devuelve el valor medio de esa evaluación. Si no se especifica una expresión numérica, el conjunto especificado se evalúa en el contexto actual de los miembros del conjunto y devuelve el valor medio de esa evaluación.  
  
 El valor medio es el valor central de un conjunto de números ordenados. (El valor medio no es lo mismo que el valor promedio, que es la suma de un conjunto de números dividido por el total de números de un conjunto.) El valor medio se determina al elegir el valor más pequeño de forma que al menos la mitad de los valores del conjunto no sean mayores que el valor elegido. Si el número de valores del conjunto es impar, el valor medio corresponde a un solo valor. Si el número de valores del conjunto es par, el valor medio corresponde a la suma de los dos valores centrales dividida por dos.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] omite los valores NULL al calcular el valor medio de un conjunto de números ordenados.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve las ventas mensuales medias de cada trimestre, cada subcategoría y cada país del cubo de Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Median   
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
  
  
