---
description: Aggregate (MDX)
title: Agregado (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d1e3f00ffbf662422f162d493a585d3972518431
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461706"
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
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un conjunto de tuplas vacías o un conjunto vacío, esta función devuelve un valor vacío.  
  
 En la tabla siguiente se describe cómo se comporta la función de **agregado** con distintas funciones de agregación.  
  
|Operador de agregación|Resultado|  
|--------------------------|------------|  
|Sum|Devuelve la suma de valores del conjunto.|  
|Recuento|Devuelve el recuento de valores del conjunto.|  
|Max|Devuelve el valor máximo del conjunto.|  
|Min|Devuelve el valor mínimo del conjunto.|  
|Funciones de agregación de suma parcial|Devuelve el cálculo de comportamiento de suma parcial del conjunto después de proyectar la forma al eje de tiempo.|  
|Distinct Count|Agrega todos los datos de hechos que contribuyen al subcubo cuando el eje segmentador incluye un conjunto.<br /><br /> Devuelve el recuento distintivo de cada miembro del conjunto. El resultado depende de la seguridad de las celdas que se agregan y no de la seguridad de las celdas necesarias para el cálculo. La seguridad de celda del conjunto genera un error; la seguridad de celda por debajo de la granularidad del conjunto especificado se omite. Los cálculos en el conjunto generan un error. Los cálculos por debajo de la granularidad del conjunto se omiten. El recuento distintivo en un conjunto que incluye un miembro y uno o más de sus elementos secundarios devuelve el recuento distintivo de todos los hechos que contribuyen al miembro secundario.|  
|Atributos que no pueden agregarse.|Devuelve la suma de los valores.|  
|Funciones de agregación combinada|No es compatible y genera un error.|  
|Operadores unarios|No se respetan; los valores se agregan mediante la suma.|  
|Medidas calculadas|Conjunto de orden de resolución para garantizar la aplicación de la medida calculada.|  
|Miembros calculados|Se aplican las reglas normales, es decir, la última orden de resolución tiene prioridad.|  
|Assignments|Las asignaciones se agregan de acuerdo con la función de agregación de medida. Si la función de agregación de medida es un recuento distintivo, se suma la asignación.|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve la suma del `Measures.[Order Quantity]` miembro, agregada durante los primeros ocho meses del año 2003 que se encuentran en la `Date` dimensión, del cubo **Adventure Works** .  
  
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
  
 El ejemplo siguiente devuelve el recuento de los distribuidores cuyas ventas han disminuido en el período de tiempo anterior, de acuerdo con los valores de los miembros State-Province seleccionados por el usuario evaluados mediante la función Aggregate. Las funciones **Hierarchy** y **DrillDownLevel** se utilizan para devolver valores para las ventas que se rechazan para las categorías de producto de la dimensión product.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [&#40;&#41;MDX de PeriodsToDate ](../mdx/periodstodate-mdx.md)   
 [Secundarios &#40;&#41;MDX ](../mdx/children-mdx.md)   
 [Jerarquía &#40;&#41;MDX ](../mdx/hierarchize-mdx.md)   
 [Count &#40;establecer&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Filtrar &#40;&#41;MDX ](../mdx/filter-mdx.md)   
 [&#41;AddCalculatedMembers &#40;MDX ](../mdx/addcalculatedmembers-mdx.md)   
 [&#41;DrilldownLevel &#40;MDX ](../mdx/drilldownlevel-mdx.md)   
 [Propiedades &#40;&#41;MDX ](../mdx/properties-mdx.md)   
 [&#41;PrevMember &#40;MDX ](../mdx/prevmember-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
