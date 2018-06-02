---
title: YTD (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33deba1261ad6c2afcf44854b0590c978683f08b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581897"
---
# <a name="ytd-mdx"></a>Ytd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y terminando con el miembro en cuestión, como restringida por la *año* nivel en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 Si no se especifica una expresión de miembro, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo *años* en la primera dimensión de tipo *tiempo* en el grupo de medida.  
  
 El **Ytd** función es una función abreviada para la [PeriodsToDate](../mdx/periodstodate-mdx.md) función donde se establece la propiedad Type de la jerarquía de atributo en el que se basa el nivel en *años*. Es decir, `Ytd(Member_Expression)` es equivalente a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Tenga en cuenta que esta función no funcionará cuando la propiedad Type se establece en *FiscalYears*.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve la suma de la `Measures.[Order Quantity]` miembro, que se agrega en los primeros ocho meses del año 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo.  
  
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
  
 **YTD** se suele usar en combinación con ningún parámetro especificado, lo que significa que la [CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md) función mostrará un total acumulado del año hasta la fecha en un informe, como se muestra en el consulta siguiente:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
