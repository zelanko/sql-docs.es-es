---
title: Usar las funciones de dimensión, jerarquía y nivel | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa374ef93f56f8cddaed81bc9e3872d1eb206c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097185"
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>Usar funciones de dimensión, jerarquía y nivel


  Las funciones de dimensión, jerarquía y nivel resultan útiles para recorrer las estructuras multidimensionales de Analysis Services. Por lo general, estas funciones se suelen utilizar junto con otras para obtener información acerca de los miembros de una dimensión, jerarquía o nivel.  
  
 En el ejemplo siguiente se muestra cómo utilizar **. Dimensión**, **. Jerarquía**y **. **Funciones de nivel:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Dimension &#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [Funciones &#40;sintaxis de MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Jerarquía &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [Nivel &#40;&#41;MDX](../mdx/level-mdx.md)  
  
  
