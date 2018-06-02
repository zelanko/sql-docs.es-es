---
title: UniqueName (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ab132fbadaf1fedb8493c93bcdec863ad52f401e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582397"
---
# <a name="uniquename-mdx"></a>UniqueName (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el nombre único de una dimensión, jerarquía, nivel o miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Dimension expression syntax  
Dimension_Expression.UniqueName  
  
Hierarchy expression syntax  
Hierarchy_Expression.UniqueName  
  
Level expression syntax  
Level_Expression.UniqueName  
  
Member expression syntax  
Member_Expression.UniqueName  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que se resuelve en una dimensión.  
  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 El **UniqueName** función devuelve el nombre único del objeto, no el nombre devuelto por la [nombre](../mdx/name-mdx.md) función. El nombre devuelto no incluye el nombre del cubo. Los resultados devueltos dependen de la configuración del servidor o de la propiedad de cadena de conexión MDX Unique Name Style.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor de nombre único de la dimensión Product, la jerarquía Product Categories, el nivel Subcategory y el miembro Bike Racks del cubo Adventure Works.  
  
```  
WITH MEMBER DimensionUniqueName   
   AS [Product].UniqueName  
MEMBER HierarchyUniqueName   
   AS [Product].[Product Categories].UniqueName  
MEMBER LevelUniqueName   
   AS [Product].[Product Categories].[Subcategory].UniqueName  
MEMBER MemberUniqueName   
   AS [Product].[Product Categories].[Subcategory].[Bike Racks]  
SELECT   
   {DimensionUniqueName  
   , HierarchyUniqueName  
   , LevelUniqueName  
   , MemberUniqueName }  
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
