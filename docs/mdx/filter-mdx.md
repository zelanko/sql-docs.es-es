---
title: Filtrar (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132692"
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
  
## <a name="remarks"></a>Observaciones  
 La función **Filter** evalúa la expresión lógica especificada en cada tupla del conjunto especificado. La función devuelve un conjunto que consta de cada tupla del conjunto especificado, donde la expresión lógica se evalúa como **true**. Si ninguna tupla se evalúa como **true**, se devuelve un conjunto vacío.  
  
 La función **Filter** funciona de manera similar a la de la función [IIf](../mdx/iif-mdx.md) . La función **IIf** devuelve solo una de las dos opciones en función de la evaluación de una expresión lógica de MDX, mientras que la función de **filtro** devuelve un conjunto de tuplas que cumplen la condición de búsqueda especificada. En efecto, la función de **filtro** se `IIf(Logical_Expression, Set_Expression.Current, NULL)` ejecuta en cada tupla del conjunto y devuelve el conjunto resultante.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra el uso de la función Filter en el eje de filas de una consulta para devolver únicamente las fechas en las que Internet Sales Amount es mayor que 10000 dólares:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 La función Filter también puede usarse dentro de definiciones de miembros calculados. En el ejemplo siguiente se devuelve la suma `Measures.[Order Quantity]` del miembro, agregada durante los primeros nueve meses de 2003 contenidos en `Date` la dimensión, del cubo **Adventure Works** . La función **PeriodsToDate** define las tuplas en el conjunto sobre el que funciona la función de **agregado** . La función de **filtro** limita las tuplas que se devuelven a aquellas con valores inferiores para la medida reseller sales amount para el período de tiempo anterior.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
