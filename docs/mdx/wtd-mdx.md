---
description: Wtd (MDX)
title: WTD (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b45e583da6f7fc18712e432a0c504c3bc813141e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421889"
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
  
## <a name="remarks"></a>Observaciones  
 Si no se especifica una expresión de miembro, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo weeks en la primera dimensión de tipo Time (**Time. CurrentMember**) del grupo de medida.  
  
 La función **WTD** es una función de acceso directo para la función [PeriodsToDate](../mdx/periodstodate-mdx.md) en la que el nivel se establece en *weeks*. Es decir, `Wtd(Member_Expression)` es equivalente a `PeriodsToDate(Week_Level_Expression,Member_Expression)`.  
  
## <a name="see-also"></a>Consulte también  
 [&#41;hasta &#40;MDX ](../mdx/qtd-mdx.md)   
 [MTD &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [&#41;MDX &#40;](../mdx/ytd-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
