---
description: 'Comentario: referencia de operadores MDX'
title: --(Comentario) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2ef1ba2fda9cd5eb6a82ea3d437c8e663c442cf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487608"
---
# <a name="comment---mdx-operator-reference"></a>Comentario: referencia de operadores MDX


  Indica texto de comentario proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Observaciones  
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
  
## <a name="see-also"></a>Consulte también  
 [Comentario &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [&#40;comentario&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
