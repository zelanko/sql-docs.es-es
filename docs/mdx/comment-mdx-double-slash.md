---
title: / / (Comentario) (MDX) | Documentos de Microsoft
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
- //
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- // (comment)
ms.assetid: 9a3ee822-4689-41a8-9997-8b307850cd68
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 35d02bc4e809048f80b90c2b11f0cf278c2f0c71
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="comment-mdx-double-slash"></a>Barra diagonal doble de comentario MDX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica texto proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Notas  
 Los comentarios pueden insertarse en una línea distinta, anidados al final de una línea en un script de Expresiones multidimensionales (MDX), o anidados en una instrucción MDX. El servidor no evalúa el comentario.  
  
 Utilice // solamente para comentarios de una línea. Los comentarios que se insertan con dos barras inclinadas (//) se delimitan con un carácter de nueva línea.  
  
 No hay límite de longitud para los comentarios.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
// This member returns the gross profit margin for product types  
// and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM // Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Ver también  
 [Comentario &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [--&#40; Comentario &#41; &#40; MDX &#41;](../mdx/comment-mdx-operator-reference.md)   
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
