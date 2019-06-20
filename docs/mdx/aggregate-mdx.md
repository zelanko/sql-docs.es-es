---
title: Agregado (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11e10d5a03702329a5ed59ed42acee0abc2d27c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200626"
---
# <a name="aggregate-mdx"></a>Aggregate (MDX)


  Devuelve un número que se calcula al agregar las celdas devueltas por la expresión establecida. Si no se proporciona una expresión numérica, esta función agrega cada medida del contexto de consulta actual mediante el operador de agregación predeterminado especificado para cada medida. Si se proporciona una expresión numérica, esta función primero evalúa y después suma la expresión numérica de cada celda del conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Aggregate(Set_Expression [ ,Numeric_Expression ])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica un conjunto de tuplas vacías o un conjunto vacío, esta función devuelve un valor vacío.  
  
 La tabla siguiente describe cómo el **agregado** función se comporta con distintas funciones de agregación.  
  
|Operador de agregación|Resultado|  
|--------------------------|------------|  
|Sum|Devuelve la suma de valores del conjunto.|  
|Count|Devuelve el recuento de valores del conjunto.|  
|Max|Devuelve el valor máximo del conjunto.|  
|Min|Devuelve el valor mínimo del conjunto.|  
|Funciones de agregación de suma parcial|Devuelve el cálculo de comportamiento de suma parcial del conjunto después de proyectar la forma al eje de tiempo.|  
|Distinct Count|Agrega todos los datos de hechos que contribuyen al subcubo cuando el eje segmentador incluye un conjunto.<br /><br /> Devuelve el recuento distintivo de cada miembro del conjunto. El resultado depende de la seguridad de las celdas que se agregan y no de la seguridad de las celdas necesarias para el cálculo. La seguridad de celda del conjunto genera un error; la seguridad de celda por debajo de la granularidad del conjunto especificado se omite. Los cálculos en el conjunto generan un error. Los cálculos por debajo de la granularidad del conjunto se omiten. El recuento distintivo en un conjunto que incluye un miembro y uno o más de sus elementos secundarios devuelve el recuento distintivo de todos los hechos que contribuyen al miembro secundario.|  
|Atributos que no pueden agregarse.|Devuelve la suma de los valores.|  
|Funciones de agregación combinada|No es compatible y genera un error.|  
|Operadores unarios|No se respetan; los valores se agregan mediante la suma.|  
|Medidas calculadas|Conjunto de orden de resolución para garantizar la aplicación de la medida calculada.|  
|Miembros calculados|Se aplican las reglas normales, es decir, la última orden de resolución tiene prioridad.|  
|Asignaciones|Las asignaciones se agregan de acuerdo con la función de agregación de medida. Si la función de agregación de medida es un recuento distintivo, se suma la asignación.|  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la suma de los `Measures.[Order Quantity]` miembro, se agregan durante los primeros ocho meses del año 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 El ejemplo siguiente agrega en los primeros dos meses del segundo semestre de 2003.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 El ejemplo siguiente devuelve el recuento de los distribuidores cuyas ventas han disminuido en el período de tiempo anterior, de acuerdo con los valores de los miembros State-Province seleccionados por el usuario evaluados mediante la función Aggregate. El **Hierarchize** y **DrillDownLevel** las funciones se usan para devolver valores para las ventas de categorías de producto de la dimensión Product que han disminuido.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)   
 [Children &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
