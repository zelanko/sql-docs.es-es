---
title: Uso de funciones de conjunto | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a042092cfcddb985b29e7b0c98612f07c68ac2d0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582287"
---
# <a name="using-set-functions"></a>Usar funciones de conjuntos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Una función de conjuntos recupera un conjunto a partir de una dimensión, jerarquía o nivel, o bien recorriendo las ubicaciones absolutas y relativas de los miembros de dichos objetos, para generar luego conjuntos de varias maneras.  
  
 Las funciones de conjunto, al igual que las funciones de tupla y de conjunto, son esenciales para negociar las estructuras multidimensionales de Analysis Services. Las funciones de conjuntos son vitales para obtener resultados de las consultas MDX (Expresiones multidimensionales) porque las expresiones de conjuntos definen los ejes de una consulta MDX.  
  
 Una de las funciones de conjunto más común es el [miembros &#40;establecer&#41; &#40;MDX&#41; ](../mdx/members-set-mdx.md) función, que recupera un conjunto que contiene todos los miembros de una dimensión, jerarquía o nivel. A continuación se muestra un ejemplo de su uso dentro de una consulta:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Es otra función que se utiliza la [Crossjoin &#40;MDX&#41; ](../mdx/crossjoin-mdx.md) (función). Devuelve un conjunto de tuplas que representan el producto cartesiano de los conjuntos pasados en el mismo como parámetros. En términos prácticos, esta función permite crear ejes 'anidados' o 'de referencias cruzadas' en las consultas:  
  
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
  
 El [descendientes &#40;MDX&#41; ](../mdx/descendants-mdx.md) función es similar el **elementos secundarios** funcionar, pero es más eficaz. Devuelve los descendientes de cualquier miembro en uno o varios niveles de una jerarquía:  
  
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
  
 El [orden &#40;MDX&#41; ](../mdx/order-mdx.md) función le permite ordenar el contenido de un conjunto en orden ascendente o descendente según una expresión numérica determinada. La consulta siguiente devuelve los mismos miembros en filas que la consulta anterior, pero ahora los ordena por la medida Internet Sales Amount:  
  
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
  
 Filtrar un conjunto según ciertos criterios resulta muy útil al escribir consultas, y para ello puede usar el [filtro &#40;MDX&#41; ](../mdx/filter-mdx.md) funcione, tal como se muestra en el ejemplo siguiente:  
  
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
  
 Existen otras funciones más sofisticadas que permiten filtrar un conjunto de otras maneras. Por ejemplo, la consulta siguiente muestra el [TopCount &#40;MDX&#41; ](../mdx/topcount-mdx.md) función devuelve los n elementos superiores de un conjunto:  
  
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
  
 Por último, es posible realizar una serie de operaciones de conjunto lógico mediante funciones como [Intersect &#40;MDX&#41;](../mdx/intersect-mdx.md), [unión &#40;MDX&#41; ](../mdx/union-mdx.md) y [excepto &#40;MDX&#41; ](../mdx/except-mdx-function.md) funciones. En la consulta siguiente se muestran ejemplos de las dos últimas funciones:  
  
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
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;sintaxis MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Usar funciones de miembro](../mdx/using-member-functions.md)   
 [Uso de funciones de tupla](../mdx/using-tuple-functions.md)  
  
  
