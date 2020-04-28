---
title: IIf (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b7b030776c1c18bb13307bf97db721fe472bd3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105333"
---
# <a name="iif-mdx"></a>IIf (MDX)


  Evalúa diferentes expresiones de bifurcación en función de si una condición booleana es true o false.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argumentos  
 La función IIf toma tres argumentos: IIF (\<condición>, \<después rama>, \<o rama>).  
  
 *Logical_Expression*  
 Una condición que se evalúa como **true** (1) o **false** (0). Debe ser expresión lógica MDX (Expresiones multidimensionales) válida.  
  
 *Sugerencia expression1 [diligente | STRICT | Lazy]]*  
 Se usa cuando la expresión lógica se evalúa como **true**. Expression1 debe ser una expresión MDX (Expresiones multidimensionales) válida.  
  
 *Sugerencia expression2 [diligente | STRICT | Lazy]]*  
 Se usa cuando la expresión lógica se evalúa como **false**. Expression2 debe ser una expresión MDX (Expresiones multidimensionales) válida.  
  
## <a name="remarks"></a>Observaciones  
 La condición especificada por la expresión lógica se evalúa como **false** cuando el valor de esta expresión es cero. Cualquier otro valor se evalúa como **true**.  
  
 Cuando la condición es **true**, la función **IIf** devuelve la primera expresión. De lo contrario, la función devuelve la segunda expresión.  
  
 Las expresiones especificadas pueden devolver valores u objetos MDX. Además, no es necesario que coincida el tipo de las expresiones especificadas.  
  
 La función **IIf** no se recomienda para crear un conjunto de miembros basado en criterios de búsqueda. En su lugar, use la función [Filter](../mdx/filter-mdx.md) para evaluar cada miembro de un conjunto especificado en una expresión lógica y devolver un subconjunto de miembros.  
  
> [!NOTE]  
>  Si una de las expresiones se evalúa en NULL, el conjunto de resultados será NULL cuando se cumpla esa condición.  
  
 Hint es un modificador opcional que determina cómo y cuándo se evalúa la expresión. Permite invalidar el plan de consulta predeterminado si se especifica cómo se evalúa la expresión.  
  
-   EAGER evalúa la expresión sobre el subespacio IIF original.  
  
-   STRICT evalúa la expresión solo en el subespacio restringido creado por la expresión de condición lógica.  
  
-   LAZY evalúa la expresión en modo celda por celda.  
  
 Mientras que EAGER y STRICT solo se aplican a las bifurcaciones then-else de IIF, LAZY se aplica a todas las expresiones MDX. Cualquier expresión MDX puede ir seguida de HINT LAZY, que evaluará esa expresión en modo celda por celda.  
  
 EAGER y STRICT son mutuamente exclusivos en la sugerencia; se pueden utilizar en el mismo IIF(,,) a través de expresiones diferentes.  
  
 Para obtener más información, vea [sugerencias de consulta de función IIf en SQL Server Analysis Services 2008](https://go.microsoft.com/fwlink/?LinkId=269540) y [planes de ejecución y sugerencias de plan para la función IIf de MDX y la instrucción Case](https://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Ejemplos  
 En la consulta siguiente se muestra un uso simple de **IIf** dentro de una medida calculada para devolver uno de dos valores de cadena diferentes cuando la medida Internet sales amount es mayor o menor que $10000:  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Un uso muy común de IIF es controlar errores de división por cero dentro de las medidas calculadas, como en el ejemplo siguiente:  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 El siguiente es un ejemplo de **IIf** que devuelve uno de dos conjuntos dentro de la función Generate para crear un conjunto complejo de tuplas en filas:  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 Por último, este ejemplo muestra cómo utilizar sugerencias de plan:  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
