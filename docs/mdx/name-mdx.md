---
description: Name (MDX)
title: Nombre (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f7598d8ee25b3ffa50d8b4ab7638640d0c5e4ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483768"
---
# <a name="name-mdx"></a>Name (MDX)


  Devuelve el nombre de una dimensión, jerarquía, nivel o miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Dimension expression syntax  
Dimension_Expression.Name  
  
Hierarchy expression syntax  
Hierarchy_Expression.Name  
  
Level_expression syntax  
Level_Expression.Name  
  
Member expression syntax  
Member_Expression.Name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Expresión MDX válida que devuelve una dimensión.  
  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **Name** devuelve el nombre del objeto, no el nombre único.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="dimension-hierarchy-and-level-expression-example"></a>Ejemplo de expresión de dimensión, jerarquía y nivel  
 El ejemplo siguiente devuelve el nombre de dimensión para la dimensión Date y los nombres de jerarquía y nivel para el miembro July 2001.  
  
```  
WITH MEMBER Measures.DimensionName AS [Date].Name  
MEMBER Measures.HierarchyName AS [Date].[Calendar].[July 2001].Hierarchy.Name  
MEMBER Measures.LevelName as [Date].[Calendar].[July 2001].Level.Name  
  
SELECT {Measures.DimensionName, Measures.HierarchyName, Measures.LevelName} ON 0  
from [Adventure Works]  
```  
  
### <a name="member-expression-example"></a>Ejemplo de expresión de miembro  
 El ejemplo siguiente devuelve el nombre de miembro, junto con el valor, la clave y el título de miembro.  
  
```  
WITH MEMBER MemberName AS [Date].[Calendar].[July 1, 2001].Name  
MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.MemberName, Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
