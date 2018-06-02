---
title: Los miembros (Set) (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3bc1cb1f1d6836bcedbad533beeed48266e774a3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580487"
---
# <a name="members-set-mdx"></a>Members (Set) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Notas  
 Si se especifica una expresión de jerarquía, el **Members (conjunto)** función devuelve el conjunto de todos los miembros de la jerarquía especificada, sin incluir los miembros calculados. Para obtener el conjunto de todos los miembros, calculado o en caso contrario, en una jerarquía, utilice la [AllMembers &#40;MDX&#41; ](../mdx/allmembers-mdx.md) (función)  
  
 Si se especifica una expresión de nivel, la **Members (conjunto)** función devuelve el conjunto de todos los miembros del nivel especificado.  
  
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
  
 El siguiente ejemplo devuelve las cantidades de pedido de 2003 para cada miembro del nivel `[Product].[Products].[Product Line]`. El **miembros** función devuelve un conjunto que representa todos los miembros del nivel.  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
