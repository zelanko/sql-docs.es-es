---
title: Comentarios (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 834e31fcc9d8e0887929dae356c7b2068aeeff2d
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669342"
---
# <a name="comments-dmx"></a>Comentarios (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Los comentarios de las extensiones de minería de datos (DMX) son cadenas de texto en el código del programa que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no se ejecuta. Los comentarios también se denominan observaciones. Los comentarios se pueden usar para documentar el código o para deshabilitar temporalmente partes de una instrucción o script DMX cuando se diagnostican problemas de código.  
  
 La utilización de comentarios para documentar el código de programación facilita el mantenimiento futuro del código. Los comentarios sirven para registrar detalles como el nombre del programa, el nombre del programador que escribió el código y las fechas de implementación de cambios importantes en el código. También puede usar los comentarios para describir cálculos complicados o un método de programación.  
  
 A continuación, figuran instrucciones básicas para escribir comentarios:  
  
-   Puede usar cualquier carácter alfanumérico o símbolo en un comentario. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pasa por alto todos los caracteres del comentario.  
  
-   No hay longitud máxima para un comentario dentro de una instrucción o script. Un comentario puede estar formado por una o varias líneas.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite los siguientes tipos de caracteres en comentarios:  
  
-   **(barras diagonales dobles).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar o en una línea independiente. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]evalúa todo desde las barras diagonales dobles hasta el final de la línea como parte del comentario. Para crear un comentario de varias líneas, use la barra diagonal doble al principio de cada línea de comentario. Para obtener más información sobre este carácter de comentario, vea [barra diagonal doble &#40;comment&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **--(guiones dobles).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar o en una línea independiente. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera como comentario todo lo que figura desde el guión doble hasta el final de la línea. Para crear un comentario de varias líneas, use el guión doble al principio de cada línea de comentario. Para obtener más información sobre este carácter de comentario, consulte [--&#40;comment&#41; &#40;DMX&#41; Summary](../dmx/comment-dmx-summary.md).  
  
-   **/\*... \* /(pares de caracteres de barra diagonal y asterisco).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar, en una línea independiente o en medio de código ejecutable. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]evalúa todo el elemento desde el par de comentario de apertura (/*) hasta el par \* de comentario de cierre (/) como parte del comentario. Para crear un Comentario de varias líneas, inicie el comentario con el par de caracteres de apertura de comentario (/ \* ) y finalice el comentario con el par de caracteres de cierre de comentario ( \* /). Ningún otro carácter de comentario debe aparecer en ninguna línea del comentario. Para obtener más información sobre este carácter de comentario, vea [barra diagonal de &#40;de comentario&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
