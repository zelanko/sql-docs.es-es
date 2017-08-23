---
title: Comentarios (sintaxis de MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- remarks [MDX]
- MDX [Analysis Services], comments
- commenting characters
- nonexecuting text strings [MDX]
- Multidimensional Expressions [Analysis Services], comments
- comments [MDX]
ms.assetid: 9c00b30c-28f6-4f23-b812-ccc0e900daa5
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 372ef0470c32b4bb7fc6f6b2094a1e3b4d1a7013
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="comments-mdx-syntax"></a>Comentarios (sintaxis de MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Los comentarios son cadenas de texto no ejecutables en código de programa. (Los comentarios también se denominan observaciones). Los comentarios permiten documentar el código o deshabilitar temporalmente partes de las instrucciones de expresiones multidimensionales (MDX) o los scripts que se estén diagnosticando. La utilización de comentarios para documentar código facilita el mantenimiento futuro del código del programa. Con frecuencia, los comentarios se usan para registrar el nombre de un programa, el nombre del autor y las fechas de los cambios importantes del código. También se pueden usar para describir cálculos complicados o explicar un método de programación.  
  
 Los comentarios MDX deben seguir las siguientes directrices:  
  
-   En los comentarios se pueden usar todos los caracteres o símbolos alfanuméricos. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] omite todos los caracteres dentro de un comentario.  
  
-   No hay longitud máxima para un comentario dentro de una instrucción o script. Un comentario puede estar formado por una o varias líneas.  
  
 MDX admite tres tipos de caracteres para indicar comentarios:  
  
 // (barras diagonales dobles)  
 Estos caracteres de comentarios se pueden usar en la misma línea que el código que se va a ejecutar o en una línea aparte. Todo lo que se encuentre entre las barras diagonales dobles y el final de la línea es parte del comentario. En el caso de que un comentario ocupe varias líneas, las barras diagonales dobles deben aparecer al inicio de cada línea de comentarios. Para obtener más información, vea [&#40; Comentario &#41; &#40; MDX &#41; ](../mdx/comment-mdx-double-slash.md).  
  
 -- (guiones dobles)  
 Estos caracteres de comentarios se pueden usar en la misma línea que el código que se va a ejecutar o en una línea aparte. Todo lo que se encuentre entre los dos guiones y el final de la línea es parte del comentario. En el caso de que un comentario ocupe varias líneas, los guiones dobles deben aparecer al principio de cada línea de comentarios. Para obtener más información, vea [--&#40; Comentario &#41; &#40; MDX &#41; ](../mdx/comment-mdx-operator-reference.md).  
  
 /* ... \*/ (barra diagonal y asterisco pares de caracteres)  
 Estos caracteres de comentarios se pueden usar en la misma línea que el código que se va a ejecutar, en líneas separadas o, incluso, en el código ejecutable. Todo, desde el par de apertura de comentario (/\*) para el par de cierre de comentario (\*/) se considera parte del comentario. Para un comentario de varias líneas, el par de caracteres de apertura de comentario (/\*) debe iniciar el comentario y el par de caracteres de cierre de comentario (\*/) debe finalizarlo. Ningún otro carácter de comentario puede aparecer en ninguna línea del comentario. Para obtener más información, vea [/ *... \*/ (Comment)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente muestra ejemplos de los tres tipos de comentario:  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Elementos de sintaxis MDX &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

