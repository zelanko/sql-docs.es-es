---
title: "Usar funciones de dimensión, jerarquía y nivel | Documentos de Microsoft"
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
- dimensions [Analysis Services], functions
- level functions [MDX]
- hierarchy functions [MDX]
ms.assetid: e730f65a-1798-4094-9acf-2739e2505d52
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 10996fe3bec61356308a59ef78e52ecfeacca95a
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Usar funciones de dimensión, jerarquía y nivel
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las funciones de dimensión, jerarquía y nivel resultan útiles para recorrer las estructuras multidimensionales de Analysis Services. Por lo general, estas funciones se suelen utilizar junto con otras para obtener información acerca de los miembros de una dimensión, jerarquía o nivel.  
  
 En el ejemplo siguiente se muestra cómo utilizar el **. Dimensión**, **. Jerarquía**, y **. Nivel** funciones:  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Dimensión &#40; MDX &#41;](../mdx/dimension-mdx.md)   
 [Funciones &#40; La sintaxis de MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Jerarquía de &#40; MDX &#41;](../mdx/hierarchy-mdx.md)   
 [Nivel &#40; MDX &#41;](../mdx/level-mdx.md)  
  
  

