---
title: IIf (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ff85ddef47099462a8c38031141120d02bfd1019
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740684"
---
# <a name="iif-mdx"></a>IIf (MDX)


  Evalúa diferentes expresiones de bifurcación en función de si una condición booleana es true o false.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argumentos  
 La función IIf toma tres argumentos: iif (\<condición >, \<, a continuación, crear una bifurcación >, \<rama #else >).  
  
 *Filter*  
 Una condición que se evalúa como **true** (1) o **false** (0). Debe ser expresión lógica MDX (Expresiones multidimensionales) válida.  
  
 *Sugerencia de expression1 [diligente | Strict | Diferida]]*  
 Utilizar cuando la expresión lógica se evalúa como **true**. Expression1 debe ser una expresión MDX (Expresiones multidimensionales) válida.  
  
 *Sugerencia de expression2 [diligente | Strict | Diferida]]*  
 Utilizar cuando la expresión lógica se evalúa como **false**. Expression2 debe ser una expresión MDX (Expresiones multidimensionales) válida.  
  
## <a name="remarks"></a>Notas  
 La condición especificada por la expresión lógica se evalúa como **false** cuando el valor de esta expresión es cero. Cualquier otro valor se evalúa como **true**.  
  
 Cuando la condición es **true**, **IIf** función devuelve la primera expresión. De lo contrario, la función devuelve la segunda expresión.  
  
 Las expresiones especificadas pueden devolver valores u objetos MDX. Además, no es necesario que coincida el tipo de las expresiones especificadas.  
  
 El **IIf** función no se recomienda para crear un conjunto de miembros basado en criterios de búsqueda. En su lugar, use la [filtro](../mdx/filter-mdx.md) función para evaluar cada miembro de un conjunto especificado con una expresión lógica y devolver un subconjunto de miembros.  
  
> [!NOTE]  
>  Si una de las expresiones se evalúa en NULL, el conjunto de resultados será NULL cuando se cumpla esa condición.  
  
 Hint es un modificador opcional que determina cómo y cuándo se evalúa la expresión. Permite invalidar el plan de consulta predeterminado si se especifica cómo se evalúa la expresión.  
  
-   EAGER evalúa la expresión sobre el subespacio IIF original.  
  
-   STRICT evalúa la expresión solo en el subespacio restringido creado por la expresión de condición lógica.  
  
-   LAZY evalúa la expresión en modo celda por celda.  
  
 Mientras que EAGER y STRICT solo se aplican a las bifurcaciones then-else de IIF, LAZY se aplica a todas las expresiones MDX. Cualquier expresión MDX puede ir seguida de HINT LAZY, que evaluará esa expresión en modo celda por celda.  
  
 EAGER y STRICT son mutuamente exclusivos en la sugerencia; se pueden utilizar en el mismo IIF(,,) a través de expresiones diferentes.  
  
 Para obtener más información, consulte [sugerencias de consulta de función IIF en SQL Server Analysis Services 2008](http://go.microsoft.com/fwlink/?LinkId=269540) y [planes de ejecución y sugerencias de Plan para la función IIF de MDX y la instrucción CASE](http://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra un uso simple de **IIF** dentro de una medida calculada para devolver uno de dos valores de cadena diferentes cuando la medida Internet Sales Amount es superior o inferior a 10.000 dólares:  
  
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
  
 El siguiente es un ejemplo de **IIF** devuelve uno de los dos conjuntos existentes dentro de la función Generate para crear un conjunto complejo de tuplas en filas:  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
