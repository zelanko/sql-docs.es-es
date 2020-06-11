---
title: Referencia del operador de extensiones de minería de datos (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf2887fb779fbe66556c4b45098cba41b8128b44
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669404"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Referencia de operadores de Extensiones de minería de datos (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El lenguaje DMX (extensiones de minería de datos) de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite operadores aritméticos, de asignación, de comparación, lógicos y unarios. En la tabla siguiente se muestran los operadores que admite DMX.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|[+ &#40;agregar&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Operador aritmético que suma dos números.|  
|[-&#40;resta&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Operador aritmético que resta un número de otro número.|  
|[&#42; &#40;multiplicar&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Operador aritmético que multiplica un número por otro número.|  
|[&#40;dividir&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Operador aritmético que divide un número entre otro número.|  
|[&#60; &#40;menor que&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es menor que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#62; &#40;mayor que&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es mayor que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[= &#40;igual que&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#60;&#62; &#40;no es igual a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es distinto del valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#60;= &#40;menor o igual que&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es menor o igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#62;= &#40;mayor o igual que&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es mayor o igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[Y &#40;DMX&#41;](../dmx/and-dmx.md)|Operador lógico que realiza una conjunción de dos expresiones numéricas.|  
|[NO &#40;DMX&#41;](../dmx/not-dmx.md)|Operador lógico que realiza una negación de una expresión numérica.|  
|[O &#40;DMX&#41;](../dmx/or-dmx.md)|Operador lógico que realiza una disyunción de dos expresiones numéricas.|  
|[+ &#40;positivo&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|Operador unario que devuelve el valor positivo de una expresión numérica.|  
|[-&#40;negativo&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|Operador unario que devuelve el valor negativo de una expresión numérica.|  
|[Barra diagonal doble &#40;comentario&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
|[--&#40;comment&#41; &#40;Resumen de&#41; DMX](../dmx/comment-dmx-summary.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
|[Barra diagonal de &#40;comentario&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
