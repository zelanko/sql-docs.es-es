---
title: No vacío (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45daf970f69322cad36bbe5419bf1dc8cc8009b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088343"
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
  
## <a name="remarks"></a>Observaciones  
 Esta función devuelve las tuplas del primer conjunto especificado que no están vacías cuando se evalúan todas las tuplas del segundo conjunto. La función **NonEmpty** tiene en cuenta los cálculos y conserva las tuplas duplicadas. Si no se proporciona un segundo conjunto, la expresión se evalúa en el contexto de las coordenadas actuales de los miembros de las jerarquías de atributo y las medidas del cubo.  
  
> [!NOTE]  
>  Use esta función en lugar de la función de [&#41;de MDX &#40;da NonEmptyCrossjoin](../mdx/nonemptycrossjoin-mdx.md) en desuso.  
  
> [!IMPORTANT]  
>  No vacías es una característica de las celdas a las que hacen referencia las tuplas y no de las propias tuplas.  
  
## <a name="examples"></a>Ejemplos  
 En la consulta siguiente se muestra un ejemplo simple de **NonEmpty**, que devuelve todos los clientes que tenían un valor distinto de null para Internet sales amount el 1 de julio de 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 En el ejemplo siguiente se devuelve el conjunto de tuplas que contienen clientes y fechas de compra, mediante la función **Filter** y las funciones no **vacías** para buscar la última fecha en la que cada cliente realizó una compra:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [Filtrar &#40;&#41;MDX](../mdx/filter-mdx.md)   
 [IsEmpty &#40;&#41;MDX](../mdx/isempty-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;&#41;MDX](../mdx/nonemptycrossjoin-mdx.md)  
  
  
