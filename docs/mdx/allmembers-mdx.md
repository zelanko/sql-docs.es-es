---
title: AllMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 770d66941af9b42be3c7b26f7e04a60d2a95cac2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017152"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)


  Evalúa una expresión de jerarquía o de nivel y devuelve un conjunto que contiene todos los miembros de la jerarquía o el nivel especificados, lo que incluye todos los miembros calculados de la jerarquía o nivel.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Observaciones  
 La función **AllMembers** devuelve un conjunto que contiene todos los miembros, incluidos los miembros calculados, en la jerarquía o el nivel especificados. La función **AllMembers** devuelve los miembros calculados incluso si la jerarquía o el nivel especificados no contienen miembros visibles.  
  
> [!IMPORTANT]  
>  Cuando una dimensión contiene solo una única jerarquía visible, se puede hacer referencia a la jerarquía por el nombre de la dimensión o por el nombre de la jerarquía, dado que el nombre de la dimensión en este caso se resuelve en su única jerarquía visible. Por ejemplo, `Measures.AllMembers` es una expresión MDX válida debido a que se resuelve en la única jerarquía de la dimensión Measures.  
  
> [!NOTE]  
>  La función **AllMembers** es semánticamente similar a la función [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelven todos`Date].[Calendar Year]` los miembros de la jerarquía de atributo [en el eje de columna; esto incluye los miembros calculados `[Product].[Model Name]` y el conjunto de todos los elementos secundarios de la jerarquía de atributo en el eje de filas del cubo **Adventure Works** .  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 En el ejemplo siguiente se devuelven todos los miembros de la dimensión **Measures** en el eje de columna, lo que incluye todos los miembros calculados y el conjunto de todos los elementos secundarios de la `[Product].[Model Name]` jerarquía de atributo en el eje de filas del cubo **Adventure Works** .  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [&#41;AddCalculatedMembers &#40;MDX](../mdx/addcalculatedmembers-mdx.md)   
 [Secundarios &#40;&#41;MDX](../mdx/children-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
