---
title: WTD (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Wtd function
ms.assetid: 41066e1b-e802-4582-be4b-3ed7807b033e
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1010b6d7aef59c5bb4eb18e93ba63bc972e8b7fa
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="wtd-mdx"></a>Wtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de semana en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Si no se especifica una expresión de miembro, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo semanas en la primera dimensión de tipo Time (**Time.CurrentMember**) en el grupo de medida.  
  
 El **Wtd** función es una función abreviada para la [PeriodsToDate](../mdx/periodstodate-mdx.md) función donde se establece el nivel en *semanas*. Es decir, `Wtd(Member_Expression)` es equivalente a `PeriodsToDate(Week_Level_Expression,Member_Expression)`.  
  
## <a name="see-also"></a>Vea también  
 [QTD &#40; MDX &#41;](../mdx/qtd-mdx.md)   
 [MTd &#40; MDX &#41;](../mdx/mtd-mdx.md)   
 [YTD &#40; MDX &#41;](../mdx/ytd-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

