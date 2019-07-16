---
title: Wtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eee40829c72394bf95a1bc06540a434a1c74e166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125808"
---
# <a name="wtd-mdx"></a>Wtd (MDX)


  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de semana en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Si no se especifica una expresión de miembro, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo semanas en la primera dimensión de tipo Time (**Time.CurrentMember**) en el grupo de medida.  
  
 El **Wtd** función es una función abreviada para la [PeriodsToDate](../mdx/periodstodate-mdx.md) función donde el nivel está establecido en *semanas*. Es decir, `Wtd(Member_Expression)` es equivalente a `PeriodsToDate(Week_Level_Expression,Member_Expression)`.  
  
## <a name="see-also"></a>Vea también  
 [QTD &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [MTd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [YTD &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
