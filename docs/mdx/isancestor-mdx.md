---
title: IsAncestor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8aacd6825a81ff172d8fdf79373f5b251d6e18b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653475"
---
# <a name="isancestor-mdx"></a>IsAncestor (MDX)


  Informa de si un miembro especificado es un antecesor de otro miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsAncestor(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression1*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Member_Expression2*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **IsAncestor** función devuelve **true** si el primer miembro especificado es un antecesor del segundo miembro especificado. En caso contrario, devuelve la función **false**.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve **true** si [Date]. [ Fiscal]. CurrentMember es un antecesor de January de 2003:  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Antecesor &#40;MDX&#41;](../mdx/ancestor-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
