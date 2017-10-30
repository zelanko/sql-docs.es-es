---
title: Mediante las funciones miembro | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- member functions [MDX]
ms.assetid: 094c443f-0daa-4af7-801c-d2e1d686d755
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9354c2e6a83918742f1c2de1dea943be4b21e844
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="using-member-functions"></a>Usar funciones de miembro
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Una función miembro es una función MDX (Expresiones multidimensionales) que devuelve un miembro. Las funciones de  miembro, al igual que las funciones de tupla y de conjunto, son esenciales para negociar las estructuras multidimensionales de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 De las muchas funciones de miembro en MDX, el más importante es la **CurrentMember** función, que se usa para determinar el miembro actual en una jerarquía. La consulta siguiente muestra cómo se usa, junto con el **primario**, **antecesor**, y **Prevmember** funciones:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40; La sintaxis de MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Usar funciones de tupla](../mdx/using-tuple-functions.md)   
 [Uso de funciones de conjunto](../mdx/using-set-functions.md)  
  
  

