---
description: PeriodsToDate (MDX)
title: PeriodsToDate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8b18fe4d90a8a0c56424c5e0a7f3607ceea0eae4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471707"
---
# <a name="periodstodate-mdx"></a>PeriodsToDate (MDX)


  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel especificado en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PeriodsToDate( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Dentro del ámbito del nivel especificado, la función **PeriodsToDate** devuelve el conjunto de períodos del mismo nivel que el miembro especificado, empezando por el primer período y finalizando con el miembro especificado.  
  
-   Si se especifica un nivel, el miembro actual de la jerarquía es una *jerarquía*inferido. **CurrentMember**, donde *Hierarchy*es la jerarquía del nivel especificado.  
  
-   Si no se especifican ni un nivel ni un miembro, el nivel es el nivel primario del miembro actual de la primera jerarquía de la primera dimensión de tipo Time del grupo de medida.  
  
 `PeriodsToDate( Level_Expression, Member_Expression )` es funcionalmente equivalente a la siguiente expresión MDX:  
  
 `TopCount(Descendants(Ancestor(Member_Expression, Level_Expression), Member_Expression.Level), 1):Member_Expression`  
  
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
  
## <a name="see-also"></a>Consulte también  
 [&#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
