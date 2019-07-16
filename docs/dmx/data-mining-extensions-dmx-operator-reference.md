---
title: Referencia de operadores (DMX) de las extensiones de minería de datos | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e0dfafb74e6e86185872ea8e736b95dce7d4058
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070912"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Referencia de operadores de Extensiones de minería de datos (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El lenguaje de extensiones de minería de datos (DMX) en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite operadores aritméticos, de asignación, comparación, lógicos y unarios. En la tabla siguiente se muestran los operadores que admite DMX.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|[+ &#40;Agregar&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Operador aritmético que suma dos números.|  
|[- &#40;Subtract&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Operador aritmético que resta un número de otro número.|  
|[&#42; &#40;Multiply&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Operador aritmético que multiplica un número por otro número.|  
|[&#40;Divide&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Operador aritmético que divide un número entre otro número.|  
|[&#60;&#40;Menor&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es menor que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#62;&#40;Mayor&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es mayor que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[= &#40;Igual a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#60;&#62;&#40;No es igual a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es distinto del valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#60;= &#40;Menor o igual a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es menor o igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#62;= &#40;Mayor o igual que&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es mayor o igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[AND &#40;DMX&#41;](../dmx/and-dmx.md)|Operador lógico que realiza una conjunción de dos expresiones numéricas.|  
|[NOT &#40;DMX&#41;](../dmx/not-dmx.md)|Operador lógico que realiza una negación de una expresión numérica.|  
|[OR &#40;DMX&#41;](../dmx/or-dmx.md)|Operador lógico que realiza una disyunción de dos expresiones numéricas.|  
|[+ &#40;Positivo&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|Operador unario que devuelve el valor positivo de una expresión numérica.|  
|[- &#40;Negativo&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|Operador unario que devuelve el valor negativo de una expresión numérica.|  
|[Doble barra diagonal &#40;comentario&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
|[-- &#40;Comentario&#41; &#40;DMX&#41; resumen](../dmx/comment-dmx-summary.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
|[Barra diagonal y asterisco &#40;comentario&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
