---
title: BottomCount (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BOTTOMCOUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomCount function
ms.assetid: 1441dab3-7885-4e92-9d48-21d832286677
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4109e8241babdb49a53a233360092308b11c616b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ordena un conjunto de forma ascendente y devuelve el número especificado de tuplas del conjunto especificado con los valores más bajos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Count*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, esta función ordena las tuplas del conjunto especificado de acuerdo con el valor de la expresión numérica especificada según se ha evaluado sobre un conjunto, en orden ascendente. El **BottomCount** función, a continuación, devuelve el número especificado de tuplas con el valor más bajo.  
  
> [!IMPORTANT]  
>  El **BottomCount** funcione, al igual que el [TopCount](../mdx/topcount-mdx.md) , siempre rompe la jerarquía.  
  
 Si no se especifica una expresión numérica, la función devuelve el conjunto de miembros en orden natural, sin ordenamiento, comportándose como la [Tail (MDX)](../mdx/tail-mdx.md) (función).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la medida Reseller Order Quantity por cada año para las cinco ventas inferiores Product SubCategory, ordenadas de acuerdo con la medida Reseller Sales Amount.  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
