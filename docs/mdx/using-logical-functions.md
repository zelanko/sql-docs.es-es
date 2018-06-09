---
title: Usar funciones lógicas | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a63d8cb22a8533cf352acb690f87916e2e9d568d
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743524"
---
# <a name="using-logical-functions"></a>Usar funciones lógicas


  Una función lógica realiza operaciones o comparaciones lógicas de objetos y expresiones y devuelve un valor booleano. Las funciones lógicas son esenciales en las expresiones multidimensionales (MDX) para determinar la posición de un miembro.  
  
 La función lógica utilizada con más frecuencia es la **IsEmpty** función. Para obtener más información sobre cómo usar el **IsEmpty** función, vea [trabajar con valores vacíos](../mdx/working-with-empty-values.md).  
  
 La consulta siguiente muestra cómo utilizar el **IsLeaf** y **IsAncestor** funciones:  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;sintaxis MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
  
