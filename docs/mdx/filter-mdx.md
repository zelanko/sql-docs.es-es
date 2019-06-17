---
title: Filtro (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d740148052712a69a39e0de314496733b3b26a8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63154632"
---
# <a name="filter-mdx"></a>Filter (MDX)


  Devuelve el conjunto resultante de filtrar un determinado conjunto con una condición de búsqueda.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Logical_Expression*  
 Expresión lógica MDX (Expresiones multidimensionales) válida que se evalúa en true o false.  
  
## <a name="remarks"></a>Comentarios  
 El **filtro** función evalúa la expresión lógica especificada con cada tupla del conjunto especificado. La función devuelve un conjunto que consta de cada tupla del conjunto especificado donde la expresión lógica se evalúa como **true**. Si no hay tuplas se evalúan como **true**, se devuelve un conjunto vacío.  
  
 El **filtro** función funciona de manera similar de la [IIf](../mdx/iif-mdx.md) función. El **IIf** función devuelve solo una de dos opciones en función de la evaluación de una expresión lógica MDX, mientras el **filtro** función devuelve un conjunto de tuplas que cumplen la condición de búsqueda especificado. De hecho, el **filtro** función ejecuta `IIf(Logical_Expression, Set_Expression.Current, NULL)` en cada tupla del conjunto y devuelve el conjunto resultante.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra el uso de la función Filter en el eje de filas de una consulta para devolver únicamente las fechas en las que Internet Sales Amount es mayor que 10000 dólares:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 La función Filter también puede usarse dentro de definiciones de miembros calculados. El ejemplo siguiente devuelve la suma de los `Measures.[Order Quantity]` miembro, se agregan durante los primeros nueve meses de 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo. El **PeriodsToDate** función define las tuplas del conjunto sobre el que el **agregado** funciona de la función. El **filtro** función limita las tuplas devueltas a aquéllas con valores más bajos para la medida Reseller Sales Amount para el período de tiempo anterior.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
