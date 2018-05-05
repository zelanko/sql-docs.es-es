---
title: Referencia de operadores MDX (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1cdb8c31-a5f6-4430-b509-f81344f4622a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 05351149c5c4b7e5b639a1d3c6cb16e9894f181e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-operator-reference-mdx"></a>Referencia de operadores de MDX (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El lenguaje de Expresiones multidimensionales (MDX) admite operadores aritméticos, lógicos, de comparación, de conjunto, de cadena y unarios. En la tabla siguiente se enumeran los operadores admitidos y sus descripciones.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[--& #40; Comentario & #41; & #40; MDX & #41;](../mdx/comment-mdx-operator-reference.md)|Indica texto de comentario proporcionado por el usuario.|  
|[- &#40;Excepto&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)|Realiza una operación de conjunto que devuelve la diferencia entre dos conjuntos y quita los miembros duplicados.|  
|[- &#40;Negativo&#41; &#40;MDX&#41;](../mdx/negative-mdx.md)|Realiza una operación unaria que devuelve el valor negativo de una expresión numérica.|  
|[- &#40;Restar&#41; &#40;MDX&#41;](../mdx/subtract-mdx.md)|Realiza una operación aritmética que resta un número de otro.|  
|[&#42;&#40;Crossjoin&#41; &#40;MDX&#41;](../mdx/crossjoin-mdx-operator-reference.md)|Realiza una operación de conjunto que devuelve el producto cruzado de dos conjuntos.|  
|[&#42;&#40;Multiplicar&#41; &#40;MDX&#41;](../mdx/multiply-mdx.md)|Realiza una operación aritmética que multiplica dos números.|  
|[&#40;Dividir&#41; &#40;MDX&#41;](../mdx/divide-mdx-operator-reference.md)|Realiza una operación aritmética que divide un número por otro número.|  
|[^ &#40;Power&#41; &#40;MDX&#41;](../mdx/power-mdx.md)|Lleva a cabo una operación aritmética que eleva un número a otro número.|  
|[Comentario & #40; MDX & #41;](../mdx/comment-mdx.md)|Indica texto de comentario proporcionado por el usuario.|  
|[& #40; Comentario & #41; & #40; MDX & #41;](../mdx/comment-mdx-double-slash.md)|Indica texto proporcionado por el usuario.|  
|[: &#40;Intervalo&#41; &#40;MDX&#41;](../mdx/range-mdx.md)|Realiza una operación de conjunto que devuelve un conjunto en su orden natural, con los dos miembros especificados como extremos y todos los miembros entre ellos incluidos como miembros del conjunto.|  
|[+ &#40;Agregar&#41; &#40;MDX&#41;](../mdx/add-mdx.md)|Realiza una operación aritmética que suma dos números.|  
|[+ &#40;Positivo&#41; &#40;MDX&#41;](../mdx/positive-mdx.md)|Realiza una operación unaria que devuelve el valor positivo de una expresión numérica.|  
|[+ &#40;Concatenación de cadenas&#41; &#40;MDX&#41;](../mdx/string-concatenation-mdx.md)|Realiza una operación de cadena que concatena dos o más cadenas de caracteres, tuplas o una combinación de cadenas y tuplas.|  
|[+ &#40;Unión&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)|Realiza una operación de conjunto que devuelve la unión entre dos conjuntos y quita los duplicados.|  
|[&#60;&#40;Inferior a&#41; &#40;MDX&#41;](../mdx/less-than-mdx.md)|Realiza una operación de comparación que determina si el valor de una expresión MDX es menor que el valor de otra expresión MDX.|  
|[&#60;= &#40;Menor o igual a&#41; &#40;MDX&#41;](../mdx/less-than-or-equal-to-mdx.md)|Realiza una operación de comparación que determina si el valor de una expresión MDX es menor o igual que el valor de otra expresión MDX.|  
|[&#60;&#62;&#40;No es igual a&#41; &#40;MDX&#41;](../mdx/not-equal-to-mdx.md)|Realiza una operación de comparación que determina si el valor de una expresión MDX no es igual que el valor de otra expresión MDX.|  
|[= &#40;Igual a&#41; &#40;MDX&#41;](../mdx/equal-to-mdx.md)|Realiza una operación de comparación que determina si el valor de una expresión MDX es igual que el valor de otra expresión MDX.|  
|[&#62;&#40;Mayor&#41; &#40;MDX&#41;](../mdx/greater-than-mdx.md)|Realiza una operación de comparación que determina si el valor de una expresión MDX es mayor que el valor de otra expresión MDX.|  
|[&#62;= &#40;Mayor o igual que&#41; &#40;MDX&#41;](../mdx/greater-than-or-equal-to-mdx.md)|Realiza una operación de comparación que determina si el valor de una expresión MDX es mayor o igual que el valor de otra expresión MDX.|  
|[Y &AMP;#40;MDX&AMP;#41;](../mdx/and-mdx.md)|Realiza una conjunción lógica de dos expresiones numéricas.|  
|[ES &AMP;#40;MDX&AMP;#41;](../mdx/is-mdx.md)|Realiza una comparación lógica entre dos expresiones de objeto.|  
|[NO &AMP;#40;MDX&AMP;#41;](../mdx/not-mdx.md)|Realiza una negación lógica de una expresión numérica.|  
|[O &AMP;#40;MDX&AMP;#41;](../mdx/or-mdx.md)|Realiza una disyunción lógica de dos expresiones numéricas.|  
|[XOR &AMP;#40;MDX&AMP;#41;](../mdx/xor-mdx.md)|Realiza una exclusión lógica de dos expresiones numéricas.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje MDX & #40; MDX & #41;](../mdx/mdx-language-reference-mdx.md)  
  
  
