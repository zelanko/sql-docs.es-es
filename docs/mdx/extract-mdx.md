---
title: Extraer (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3c58799cc3e95efd7d49b3aff0bf31a1fce22b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155204"
---
# <a name="extract-mdx"></a>Extract (MDX)


  Devuelve un conjunto de tuplas de los elementos de jerarquía extraídos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Hierarchy_Expression1*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Hierarchy_Expression2*  
 Expresión MDX válida que devuelve una jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 El **extraer** función devuelve un conjunto que consta de tuplas de los elementos de jerarquía extraídos. En cada tupla del conjunto especificado, se extraen los miembros de las jerarquías especificadas en nuevas tuplas en el conjunto de resultados. Esta función quita siempre las tuplas duplicadas.  
  
 El **extraer** función realiza la acción opuesta el [Crossjoin](../mdx/crossjoin-mdx.md) función.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra cómo usar el **extraer** función en un conjunto de tuplas devueltas por la **NonEmpty** función:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
