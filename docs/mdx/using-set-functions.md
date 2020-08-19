---
description: Usar funciones de conjuntos
title: Usar funciones set | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1325055017eeee392cd098d9168dd247a2664aa4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476987"
---
# <a name="using-set-functions"></a>Usar funciones de conjuntos


  Una función de conjuntos recupera un conjunto a partir de una dimensión, jerarquía o nivel, o bien recorriendo las ubicaciones absolutas y relativas de los miembros de dichos objetos, para generar luego conjuntos de varias maneras.  
  
 Las funciones de conjunto, al igual que las funciones de tupla y de conjunto, son esenciales para negociar las estructuras multidimensionales de Analysis Services. Las funciones de conjuntos son vitales para obtener resultados de las consultas MDX (Expresiones multidimensionales) porque las expresiones de conjuntos definen los ejes de una consulta MDX.  
  
 Una de las funciones de conjunto más comunes son los [miembros &#40;establecer&#41; &#40;función&#41;de MDX ](../mdx/members-set-mdx.md) , que recupera un conjunto que contiene todos los miembros de una dimensión, jerarquía o nivel. A continuación se muestra un ejemplo de su uso dentro de una consulta:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Otra función que se usa con frecuencia es la función de [&#41;de &#40;MDX ](../mdx/crossjoin-mdx.md) . Devuelve un conjunto de tuplas que representan el producto cartesiano de los conjuntos pasados en el mismo como parámetros. En términos prácticos, esta función permite crear ejes 'anidados' o 'de referencias cruzadas' en las consultas:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Los [descendientes &#40;función MDX&#41;](../mdx/descendants-mdx.md) es similar a la función **Children** , pero es más eficaz. Devuelve los descendientes de cualquier miembro en uno o varios niveles de una jerarquía:  
  
 SELECT  
  
 [Measures].[Internet Sales Amount]  
  
 ON Columns,  
  
 //Devuelve un conjunto que incluye todas las fechas (Date) debajo del año natural (Calendar Year)  
  
 //2004 en la jerarquía Calendar de la dimensión Date  
  
 DESCENDANTS(  
  
 [Date]. [Calendar]. [Año natural]. & [2004]  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 FROM [Adventure Works]  
  
 La función [order &#40;MDX&#41;](../mdx/order-mdx.md) permite ordenar el contenido de un conjunto en orden ascendente o descendente según una expresión numérica determinada. La consulta siguiente devuelve los mismos miembros en filas que la consulta anterior, pero ahora los ordena por la medida Internet Sales Amount:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Esta consulta también muestra la forma en que el conjunto devuelto por una función de conjunto, Descendants, puede pasarse como parámetro a otra función de conjunto, Order.  
  
 Filtrar un conjunto según ciertos criterios resulta muy útil al escribir consultas y, para este propósito, puede utilizar el [filtro &#40;función&#41;MDX ](../mdx/filter-mdx.md) , como se muestra en el ejemplo siguiente:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Existen otras funciones más sofisticadas que permiten filtrar un conjunto de otras maneras. Por ejemplo, en la consulta siguiente se muestra la función [&#40;&#41;MDX de ](../mdx/topcount-mdx.md) devuelve los n elementos superiores de un conjunto:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Por último, es posible realizar una serie de operaciones de conjuntos lógicos mediante funciones como [Intersect &#40;mdx&#41;](../mdx/intersect-mdx.md), [Union &#40;MDX&#41;](../mdx/union-mdx.md) y [except &#40;funciones MDX&#41;](../mdx/except-mdx-function.md) . En la consulta siguiente se muestran ejemplos de las dos últimas funciones:  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;sintaxis de MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Usar funciones miembro](../mdx/using-member-functions.md)   
 [Usar funciones de tupla](../mdx/using-tuple-functions.md)  
  
  
