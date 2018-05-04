---
title: AllMembers (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALLMEMBERS
dev_langs:
- kbMDX
helpviewer_keywords:
- AllMembers function
ms.assetid: 202e81d4-d2ee-4ec1-a019-4835eb19f446
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: f20f6af260ff5f37aa2665d6229c2096360e05fa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Comentarios  
 El **AllMembers** función devuelve un conjunto que contiene todos los miembros, incluidos los miembros calculados, en el nivel o jerarquía especificada. El **AllMembers** función devuelve los miembros calculados incluso si la jerarquía o nivel especificados no contiene miembros visibles.  
  
> [!IMPORTANT]  
>  Cuando una dimensión contiene solo una única jerarquía visible, se puede hacer referencia a la jerarquía por el nombre de la dimensión o por el nombre de la jerarquía, dado que el nombre de la dimensión en este caso se resuelve en su única jerarquía visible. Por ejemplo, `Measures.AllMembers` es una expresión MDX válida debido a que se resuelve en la única jerarquía de la dimensión Measures.  
  
> [!NOTE]  
>  El **AllMembers** función es semánticamente similar a la [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md) (función).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los miembros en el [`Date].[Calendar Year]` jerarquía de atributo en el eje de columna, esto incluye los miembros calculados y el conjunto de todos los elementos secundarios de la `[Product].[Model Name]` jerarquía del eje de fila de atributo el **Adventure Works** cubo.  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve todos los miembros de la **medidas** dimensión en el eje de columna, esto incluye todos los miembros calculados y el conjunto de todos los elementos secundarios de la `[Product].[Model Name]` atributo la jerarquía del eje de fila de la **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [AddCalculatedMembers & #40; MDX & #41;](../mdx/addcalculatedmembers-mdx.md)   
 [Elementos secundarios &#40;MDX&#41;](../mdx/children-mdx.md)   
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
