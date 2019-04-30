---
title: Comentarios (sintaxis de MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17693d0dc76dd6cb8b3a4d0c3ead9f95c0599580
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181562"
---
# <a name="comments-mdx-syntax"></a>Comentarios (sintaxis de MDX)


  Los comentarios son cadenas de texto no ejecutables en código de programa. (Los comentarios también se denominan observaciones). Los comentarios permiten documentar el código o deshabilitar temporalmente partes de las instrucciones de expresiones multidimensionales (MDX) o los scripts que se estén diagnosticando. La utilización de comentarios para documentar código facilita el mantenimiento futuro del código del programa. Con frecuencia, los comentarios se usan para registrar el nombre de un programa, el nombre del autor y las fechas de los cambios importantes del código. También se pueden usar para describir cálculos complicados o explicar un método de programación.  
  
 Los comentarios MDX deben seguir las siguientes directrices:  
  
-   En los comentarios se pueden usar todos los caracteres o símbolos alfanuméricos.  Se omiten todos los caracteres dentro de un comentario.  
  
-   No hay longitud máxima para un comentario dentro de una instrucción o script. Un comentario puede estar formado por una o varias líneas.  
  
 MDX admite tres tipos de caracteres para indicar comentarios:  
  
 // (barras diagonales dobles)  
 Estos caracteres de comentarios se pueden usar en la misma línea que el código que se va a ejecutar o en una línea aparte. Todo lo que se encuentre entre las barras diagonales dobles y el final de la línea es parte del comentario. En el caso de que un comentario ocupe varias líneas, las barras diagonales dobles deben aparecer al inicio de cada línea de comentarios. Para obtener más información, consulte [ &#40;comentario&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md).  
  
 -- (guiones dobles)  
 Estos caracteres de comentarios se pueden usar en la misma línea que el código que se va a ejecutar o en una línea aparte. Todo lo que se encuentre entre los dos guiones y el final de la línea es parte del comentario. En el caso de que un comentario ocupe varias líneas, los guiones dobles deben aparecer al principio de cada línea de comentarios. Para obtener más información, consulte [-- &#40;comentario&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md).  
  
 /* ... \*/ (barra diagonal y asterisco pares de caracteres)  
 Estos caracteres de comentarios se pueden usar en la misma línea que el código que se va a ejecutar, en líneas separadas o, incluso, en el código ejecutable. Todo, desde el par de comentario de apertura (/\*) para el par de comentario de cierre (\*/) se considera parte del comentario. Para un comentario de varias líneas, el par de caracteres de apertura de comentario (/\*) debe iniciar el comentario y el par de caracteres de cierre de comentario (\*/) debe finalizarlo. Ningún otro carácter de comentario puede aparecer en las líneas de comentario. Para obtener más información, consulte [/ *... \*/ (Comentario)](../mdx/comment-mdx.md).  
  
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
 [Los elementos de sintaxis MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
