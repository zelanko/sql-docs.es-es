---
title: SUM (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb4e9d55ef2228404dd9113170066e4a3612a0a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036675"
---
# <a name="sum-mdx"></a>Sum (MDX)


  Devuelve la suma de una expresión numérica evaluada sobre un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Una expresión de conjunto de MDX (Expresiones multidimensionales) válida.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, ésta se evalúa en el conjunto y, a continuación, se suma. Si no se especifica una expresión numérica, el conjunto especificado se evalúa en el contexto actual de los miembros del conjunto y, a continuación, se suma. Si la función SUM se aplica a una expresión no numérica, los resultados quedarán sin definir.  
  
> [!NOTE]  
>  Analysis Services omite los valores nulos al calcular la suma de un conjunto de números.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la suma de Reseller Sales Amounts para todos los miembros de la jerarquía de atributo Product.Category para los años 2001 y 2002.  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve la suma de los costos de flete correspondientes a las ventas por Internet del mes de julio de 2002 hasta el día 20 de julio.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se usa la palabra clave WITH MEMBER y **suma** función para definir un miembro calculado en la dimensión Measures que contiene la suma de la medida Reseller Sales Amount para los miembros Canada y United States de la Jerarquía de atributo Country de la dimensión Geography.  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 A menudo, el **suma** función se utiliza con el **CURRENTMEMBER** función o funciones como **YTD** que devuelve un conjunto que varía según el miembro actual de una jerarquía. Por ejemplo, la siguiente consulta devuelve la suma de la medida Internet Sales Amount para todas las fechas desde principio del año natural hasta la fecha mostrada en el eje de filas:  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
