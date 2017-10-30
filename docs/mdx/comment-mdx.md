---
title: Comentario (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '*/'
- /*
dev_langs:
- kbMDX
helpviewer_keywords:
- commenting characters
- /*...*/ (comment)
ms.assetid: 64434ae4-80ce-4634-86b8-4125dfaa7f61
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fca15a526cbd5329c8116e751bda4959a46e1713
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="comment-mdx"></a>Comentario (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica texto de comentario proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Comentarios  
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
 [&#40; Comentario &#41; &#40; MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [--&#40; Comentario &#41; &#40; MDX &#41;](../mdx/comment-mdx-operator-reference.md)   
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

