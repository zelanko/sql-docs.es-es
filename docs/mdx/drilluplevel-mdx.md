---
title: DrillupLevel (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLUPLEVEL
dev_langs: kbMDX
helpviewer_keywords: DrillupLevel function
ms.assetid: 63431f79-f3a1-40c4-bf57-2b6bd8991cc3
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5b17f352e31fe3cb08a2ca2af629cf9cde1bc08f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reduce el detalle de los miembros de un conjunto por debajo de un nivel especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Comentarios  
 El **DrillupLevel** función devuelve un conjunto de miembros se organiza jerárquicamente según los miembros incluidos en el conjunto especificado. Se mantiene el orden entre los miembros del conjunto especificado.  
  
 Si se especifica una expresión de nivel, la **DrillupLevel** función crea el conjunto mediante la recuperación solo aquellos miembros que están por encima del nivel especificado. Si se especifica una expresión de nivel y no hay un miembro del nivel especificado representado en el conjunto especificado, se devuelve el conjunto especificado.  
  
 Si no se especifica una expresión de nivel, la función crea el conjunto mediante la recuperación de solo aquellos miembros que se encuentran un nivel por encima del nivel más bajo de la primera dimensión a la que se hace referencia en el conjunto especificado.  
  
## <a name="example"></a>Ejemplo  
 EL ejemplo siguiente devuelve el conjunto de miembros del primer conjunto que están por encima del nivel Subcategory.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
