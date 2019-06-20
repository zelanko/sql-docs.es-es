---
title: Comentarios (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f319457da85378000ef974c3ace1ddbba87d18e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62709084"
---
# <a name="comments-dmx"></a>Comentarios (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Comentarios en las extensiones de minería de datos (DMX) son cadenas de texto en el programa de código que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no se ejecuta. Los comentarios también se denominan observaciones. Los comentarios se pueden usar para documentar el código o para deshabilitar temporalmente partes de una instrucción o script DMX cuando se diagnostican problemas de código.  
  
 La utilización de comentarios para documentar el código de programación facilita el mantenimiento futuro del código. Los comentarios sirven para registrar detalles como el nombre del programa, el nombre del programador que escribió el código y las fechas de implementación de cambios importantes en el código. También puede usar los comentarios para describir cálculos complicados o un método de programación.  
  
 A continuación, figuran instrucciones básicas para escribir comentarios:  
  
-   Puede usar cualquier carácter alfanumérico o símbolo en un comentario. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pasa por alto todos los caracteres del comentario.  
  
-   No hay longitud máxima para un comentario dentro de una instrucción o script. Un comentario puede estar formado por una o varias líneas.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite los siguientes tipos de caracteres en comentarios:  
  
-   **(barras diagonales dobles).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar o en una línea independiente. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se evalúa como todo, desde la barra diagonal doble hasta el final de la línea como parte del comentario. Para crear un comentario de varias líneas, use la barra diagonal doble al principio de cada línea de comentario. Para obtener más información acerca de este carácter de comentario, vea [barra diagonal doble &#40;comentario&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **--(guiones dobles).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar o en una línea independiente. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera como comentario todo lo que figura desde el guión doble hasta el final de la línea. Para crear un comentario de varias líneas, use el guión doble al principio de cada línea de comentario. Para obtener más información acerca de este carácter de comentario, vea [-- &#40;comentario&#41; &#40;DMX&#41; resumen](../dmx/comment-dmx-summary.md).  
  
-   **/\* ... \*/ (barra diagonal y asterisco pares de caracteres).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar, en una línea independiente o en medio de código ejecutable. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se evalúa como todo, desde el par de comentario de apertura (/ *) para el par de comentario de cierre (\*/) como parte del comentario. Para crear un comentario de varias líneas, inicie el comentario con el par de caracteres de apertura de comentario (/\*) y terminar el comentario con el par de caracteres de cierre de comentario (\*/). Ningún otro carácter de comentario debe aparecer en ninguna línea del comentario. Para obtener más información acerca de este carácter de comentario, vea [Slash Star &#40;comentario&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
