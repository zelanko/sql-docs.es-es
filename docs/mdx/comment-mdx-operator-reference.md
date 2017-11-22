---
title: --(Comentario) (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: --
dev_langs: kbMDX
helpviewer_keywords:
- commenting characters
- -- (comment character)
ms.assetid: 02aec133-6809-4829-b9a2-102c376e21da
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8ec94e2553e55d7d4f3806a3ca548e7379f3bdd3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="comment---mdx-operator-reference"></a>Comentario - referencia de operadores MDX
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica texto de comentario proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Comentarios  
 Los comentarios pueden insertarse en una línea distinta, anidados al final de una línea en un script de Expresiones multidimensionales (MDX), o anidados en una instrucción MDX. El servidor no evalúa el comentario.  
  
 Use este operador para comentarios de una línea o anidados. Los comentarios que se insertan con dos guiones (--) se delimitan con un carácter de nueva línea.  
  
 No hay límite de longitud para los comentarios.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Vea también  
 [Comentario &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [&#40; Comentario &#41; &#40; MDX &#41;](../mdx/comment-mdx-double-slash.md)   
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
