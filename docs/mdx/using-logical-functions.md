---
title: Usar funciones lógicas | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6bd427ebfca1fbf2f546603853b2352d6dcf4c90
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582467"
---
# <a name="using-logical-functions"></a>Usar funciones lógicas
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
