---
title: Qtd (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: QTD
dev_langs: kbMDX
helpviewer_keywords: Qtd function
ms.assetid: c1fe47e0-9c2b-466f-8d6d-e2b1c16a69cb
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: cabe908f3d78082d6af113a60f105ba4f4e4f5c0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="qtd-mdx"></a>Qtd (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y terminando con el miembro en cuestión, como restringida por la *trimestre* nivel en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Si expressionis de miembro que no se especifica, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo *trimestres* en la primera dimensión de tipo *tiempo* en el grupo de medida.  
  
 El **Qtd** función es una función abreviada para la [PeriodsToDate &#40; MDX &#41; ](../mdx/periodstodate-mdx.md) función cuyo argumento de expresión de nivel se establece en *trimestre*. Es decir, `Qtd(Member_Expression)` es funcionalmente equivalente a `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve la suma de la `Measures.[Order Quantity]` miembro, que se agrega en los dos primeros meses del tercer trimestre del año 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
