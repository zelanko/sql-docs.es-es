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
ms.openlocfilehash: 5cc8352b0d087b54a623cce892a05dfed29258b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105260"
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
  
## <a name="remarks"></a>Observaciones  
 La función **IsAncestor** devuelve **true** si el primer miembro especificado es un antecesor del segundo miembro especificado. De lo contrario, la función devuelve **false**.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve **true** si [Date]. [Fiscal]. CurrentMember es un antecesor del 2003 de enero:  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [&#41;&#40;de MDX](../mdx/ancestor-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
