---
title: Comentario (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a38b7c7ed805afbcdfd3b5426141358bfde742c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577447"
---
# <a name="comment-mdx"></a>Comentario (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica texto de comentario proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Notas  
 El servidor no evalúa el texto entre los caracteres de comentario / * y \*/. Los comentarios pueden insertarse en una línea distinta o como parte de una instrucción de Expresiones multidimensionales (MDX).  Comentarios de varias líneas deben indicarse con /\* y \*/.  
  
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
 [&#40;Comentario&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [-- &#40;Comentario&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
