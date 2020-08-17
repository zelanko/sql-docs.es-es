---
description: Extract (MDX)
title: Extraer (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0b168794a38a515d4ace97d576710041eac86195
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387521"
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
  
## <a name="remarks"></a>Observaciones  
 La función **Extract** devuelve un conjunto que consta de tuplas de los elementos de jerarquía extraídos. En cada tupla del conjunto especificado, se extraen los miembros de las jerarquías especificadas en nuevas tuplas en el conjunto de resultados. Esta función quita siempre las tuplas duplicadas.  
  
 La función **Extract** realiza la acción opuesta a la función [Crossjoin](../mdx/crossjoin-mdx.md) .  
  
## <a name="examples"></a>Ejemplos  
 En la consulta siguiente se muestra cómo usar la función **Extract** en un conjunto de tuplas devueltas por la función **NonEmpty** :  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
