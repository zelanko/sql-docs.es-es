---
title: NonEmpty (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- NonEmpty function
ms.assetid: dfbfa747-3175-405c-aa5b-15c187b06338
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 334b54968c8603928850d2ce195f7c1be50ad161
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
>  Use esta función en lugar de las regiones [NonEmptyCrossjoin &#40; MDX &#41; ](../mdx/nonemptycrossjoin-mdx.md) (función).  
  
> [!IMPORTANT]  
>  No vacías es una característica de las celdas a las que hacen referencia las tuplas y no de las propias tuplas.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra un ejemplo sencillo de **NonEmpty**, devolver todos los clientes que tenían un valor distinto de null para Internet Sales Amount en el 1 de julio de 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 En el ejemplo siguiente se devuelve el conjunto de tuplas que contiene clientes y fechas de compra mediante el **filtro** función y la **NonEmpty** funciones para encontrar la última fecha en que cada cliente realizó una compra:  
  
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
 [DefaultMember &#40; MDX &#41;](../mdx/defaultmember-mdx.md)   
 [Filtro &#40; MDX &#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40; MDX &#41;](../mdx/isempty-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40; MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  

