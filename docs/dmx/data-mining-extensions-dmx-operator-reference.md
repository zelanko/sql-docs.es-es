---
title: "Referencia de operadores (DMX) de extensiones de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: a6d747c0-9ff0-475f-86cd-34bebd79c21a
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b750c1ba7fb7f0557b69aa70e768fd323e2de2c5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Referencia de operadores de Extensiones de minería de datos (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El lenguaje de extensiones de minería de datos (DMX) en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] es compatible con operadores aritméticos, asignación, comparación, lógicos y unarios. En la tabla siguiente se muestran los operadores que admite DMX.  
  
|Operador|Description|  
|--------------|-----------------|  
|[+ &#40; Agregar &#41; &#40; DMX &#41;](../dmx/add-dmx.md)|Operador aritmético que suma dos números.|  
|[-&#40; Restar &#41; &#40; DMX &#41;](../dmx/subtract-dmx.md)|Operador aritmético que resta un número de otro número.|  
|[&#42; &#40; Multiplicar &#41; &#40; DMX &#41;](../dmx/multiply-dmx.md)|Operador aritmético que multiplica un número por otro número.|  
|[&#40; división &#41; &#40; DMX &#41;](../dmx/divide-dmx.md)|Operador aritmético que divide un número entre otro número.|  
|[&#60; &#40; Menor &#41; &#40; DMX &#41;](../dmx/less-than-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es menor que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#62; &#40; Mayor &#41; &#40; DMX &#41;](../dmx/greater-than-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es mayor que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[= &#40; Igual a &#41; &#40; DMX &#41;](../dmx/equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#60; &#62; &#40; No igual a &#41; &#40; DMX &#41;](../dmx/not-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es distinto del valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#60; = &#40; Menor o igual a &#41; &#40; DMX &#41;](../dmx/less-than-or-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es menor o igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[&#62; = &#40; Mayor que o igual a &#41; &#40; DMX &#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operador de comparación. En el caso de argumentos que se evalúan como valores no NULL, devuelve TRUE si el valor del argumento de la izquierda es mayor o igual que el valor del argumento de la derecha; de lo contrario, devuelve FALSE. Si un argumento o ambos argumentos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[Y &#40; DMX &#41;](../dmx/and-dmx.md)|Operador lógico que realiza una conjunción de dos expresiones numéricas.|  
|[NO &#40; DMX &#41;](../dmx/not-dmx.md)|Operador lógico que realiza una negación de una expresión numérica.|  
|[O &#40; DMX &#41;](../dmx/or-dmx.md)|Operador lógico que realiza una disyunción de dos expresiones numéricas.|  
|[+ &#40; Positivo &#41; &#40; DMX &#41;](../dmx/positive-dmx.md)|Operador unario que devuelve el valor positivo de una expresión numérica.|  
|[-&#40; Negativo &#41; &#40; DMX &#41;](../dmx/negative-dmx.md)|Operador unario que devuelve el valor negativo de una expresión numérica.|  
|[Doble barra diagonal &#40; Comentario &#41; &#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
|[--&#40; Comentario &#41; &#40; DMX &#41; Resumen](../dmx/comment-dmx-summary.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
|[Estrella de barra diagonal &#40; Comentario &#41; &#40; DMX &#41;](../dmx/slash-star-comment-dmx.md)|Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX, incluirlos al final de una línea de código o insertarlos en una línea independiente.|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  
