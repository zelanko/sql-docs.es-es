---
title: NonEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 91e6d478397cf9fa77a6ca33748b5a4515034471
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278516"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  Devuelve un conjunto de tuplas que no están vacías de un conjunto especificado, según el producto cruzado del conjunto especificado con un segundo conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>Argumentos  
 *set_expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *set_expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 Esta función devuelve las tuplas del primer conjunto especificado que no están vacías cuando se evalúan todas las tuplas del segundo conjunto. El **NonEmpty** función toma en cuenta los cálculos y conserva las tuplas duplicadas. Si no se proporciona un segundo conjunto, la expresión se evalúa en el contexto de las coordenadas actuales de los miembros de las jerarquías de atributo y las medidas del cubo.  
  
> [!NOTE]  
>  Utilice esta función en lugar de en desuso [NonEmptyCrossjoin &#40;MDX&#41; ](../mdx/nonemptycrossjoin-mdx.md) función.  
  
> [!IMPORTANT]  
>  No vacías es una característica de las celdas a las que hacen referencia las tuplas y no de las propias tuplas.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra un ejemplo sencillo de **NonEmpty**, devuelve todos los clientes que tenían un valor distinto de null para Internet Sales Amount del 1 de julio de 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 El ejemplo siguiente devuelve el conjunto de tuplas que contiene clientes y fechas de compra mediante el **filtro** función y el **NonEmpty** funciones para buscar la última fecha en que cada cliente realizó una compra:  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
