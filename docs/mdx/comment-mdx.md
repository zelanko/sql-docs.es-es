---
title: Comentario (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6469921572b8a1809e228fff0d25061475399ae7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181570"
---
# <a name="comment-mdx"></a>Comentario (MDX)


  Indica texto de comentario proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Comentarios  
 El servidor no evalúa el texto situado entre los caracteres de comentario / * y \*/. Los comentarios pueden insertarse en una línea distinta o como parte de una instrucción de Expresiones multidimensionales (MDX).  Los comentarios de varias líneas deben indicarse con /\* y \*/.  
  
 No hay límite de longitud para los comentarios. Los comentarios pueden anidarse; por ejemplo, `/* Test /*Comment*/ Text*/` es un ejemplo de un comentario anidado.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Vea también  
 [&#40;Comment&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [-- &#40;Comentario&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
