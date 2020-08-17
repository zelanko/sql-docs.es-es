---
description: Members (Set) (MDX)
title: Members (Set) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0358f20d0aeba0e4d455fabadb6dc1e4361081e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341401"
---
# <a name="members-set-mdx"></a>Members (Set) (MDX)


  Devuelve el conjunto de miembros en una dimensión, nivel o jerarquía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión de jerarquía, la función **Members (Set)** devuelve el conjunto de todos los miembros de la jerarquía especificada, sin incluir los miembros calculados. Para obtener el conjunto de todos los miembros, calculados o en cualquier otro caso, en una jerarquía, utilice la función [AllMembers &#40;MDX&#41;](../mdx/allmembers-mdx.md)  
  
 Si se especifica una expresión de nivel, la función **Members (Set)** devuelve el conjunto de todos los miembros en el nivel especificado.  
  
> [!IMPORTANT]  
>  Cuando una dimensión contiene solo una única jerarquía visible, se puede hacer referencia a la jerarquía por el nombre de la dimensión o por el nombre de la jerarquía, dado que el nombre de la dimensión en este escenario se resuelve en su única jerarquía visible. Por ejemplo, Measures.Members es una expresión MDX válida debido a que se resuelve en la única jerarquía de la dimensión Measures.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el conjunto de todos los miembros de la jerarquía Calendar Year del cubo Adventure Works.  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 El siguiente ejemplo devuelve las cantidades de pedido de 2003 para cada miembro del nivel `[Product].[Products].[Product Line]`. La función **Members** devuelve un conjunto que representa todos los miembros del nivel.  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
