---
title: Usar funciones de dimensión, jerarquía y nivel | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 96315c01133f3a25e5853ba076d2b28e5ba81a35
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581497"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Usar funciones de dimensión, jerarquía y nivel
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [Dimensión &#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [Funciones &#40;sintaxis MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Jerarquía &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Nivel &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
