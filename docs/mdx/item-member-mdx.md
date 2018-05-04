---
title: Elemento (miembro) (MDX) | Documentos de Microsoft
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
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 71cca249-910b-4ecd-9097-1a17b224e219
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 76603e70d7bd4779f8d76a69a872d9ee39d2323f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="item-member-mdx"></a>Item (Member) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un miembro de una tupla especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
 *Index*  
 Expresión numérica válida que especifica el miembro concreto mediante la posición en la tupla que se devolverá.  
  
## <a name="remarks"></a>Comentarios  
 El **elemento** función devuelve un miembro de la tupla especificada. La función devuelve el miembro que se encuentra en la posición de base cero especificada por *índice*.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se devuelve el miembro `[2003]` (el primer elemento de la tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).`) en columnas:  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
