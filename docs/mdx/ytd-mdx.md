---
title: Año (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125760"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer elemento del mismo nivel y finalizando con el miembro dado, restringido por el nivel de *año* de la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Si no se especifica una expresión de miembro, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo *years* en la primera dimensión de tipo *Time* en el grupo de medida.  
  
 La función de **año actual** es una función abreviada para la función [PeriodsToDate](../mdx/periodstodate-mdx.md) en la que la propiedad Type de la jerarquía de atributo en la que se basa el nivel está establecida en *years*. Es decir, `Ytd(Member_Expression)` es equivalente a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Tenga en cuenta que esta función no funcionará cuando la propiedad Type esté establecida en *FiscalYears*.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve la suma `Measures.[Order Quantity]` del miembro, agregada durante los primeros ocho meses del año 2003 que se encuentran en la `Date` dimensión, del cubo **Adventure Works** .  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 El **año actual** se usa con frecuencia en combinación sin parámetros especificados, lo que significa que la función [CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md) mostrará un total acumulado de un año hasta la fecha en un informe, como se muestra en la consulta siguiente:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
