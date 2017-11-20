---
title: Comentarios (DMX) | Documentos de Microsoft
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
dev_langs:
- DMX
helpviewer_keywords:
- comments [DMX]
- Data Mining Extensions [Analysis Services], comments
- double forward slashes
- commenting characters
- text strings [SQL Server]
- remarks [DMX]
- forward slash-asterisk character pairs
- DMX [Analysis Services], comments
- /*...*/ (comment)
- double hyphens
- // (comment)
- -- (comment character)
ms.assetid: 64d10eb5-4fe8-42c6-b387-eff336315e56
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 012feb6b830b18151708a85259a0d52ba195788f
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="comments-dmx"></a>Comentarios (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Comentarios en las extensiones de minería de datos (DMX) son cadenas de texto en el programa de código que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no se ejecuta. Los comentarios también se denominan observaciones. Los comentarios se pueden usar para documentar el código o para deshabilitar temporalmente partes de una instrucción o script DMX cuando se diagnostican problemas de código.  
  
 La utilización de comentarios para documentar el código de programación facilita el mantenimiento futuro del código. Los comentarios sirven para registrar detalles como el nombre del programa, el nombre del programador que escribió el código y las fechas de implementación de cambios importantes en el código. También puede usar los comentarios para describir cálculos complicados o un método de programación.  
  
 A continuación, figuran instrucciones básicas para escribir comentarios:  
  
-   Puede usar cualquier carácter alfanumérico o símbolo en un comentario. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pasa por alto todos los caracteres del comentario.  
  
-   No hay longitud máxima para un comentario dentro de una instrucción o script. Un comentario puede estar formado por una o varias líneas.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite los siguientes tipos de caracteres en comentarios:  
  
-   **(barras diagonales dobles).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar o en una línea independiente. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]evalúa todos los elementos de la barra diagonal doble hasta el final de la línea como parte del comentario. Para crear un comentario de varias líneas, use la barra diagonal doble al principio de cada línea de comentario. Para obtener más información sobre este carácter de comentario, vea [barra diagonal doble &#40; Comentario &#41; &#40; DMX &#41; ](../dmx/double-slash-comment-dmx.md).  
  
-   **--(guiones dobles).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar o en una línea independiente. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera como comentario todo lo que figura desde el guión doble hasta el final de la línea. Para crear un comentario de varias líneas, use el guión doble al principio de cada línea de comentario. Para obtener más información sobre este carácter de comentario, vea [--&#40; Comentario &#41; &#40; DMX &#41; Resumen de](../dmx/comment-dmx-summary.md).  
  
-   **/\*... \*/ (barra diagonal y asterisco pares de caracteres).** Estos caracteres de comentario sirven para escribir un comentario en la misma línea que el código que se va a ejecutar, en una línea independiente o en medio de código ejecutable. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]se evalúa como todo, desde el par de apertura de comentario (/ *) para el par de cierre de comentario (\*/) como parte del comentario. Para crear un comentario ocupe varias líneas, inicie el comentario con el par de caracteres de apertura de comentario (/\*) y finalice el comentario con el par de caracteres de cierre de comentario (\*/). Ningún otro carácter de comentario debe aparecer en ninguna línea del comentario. Para obtener más información sobre este carácter de comentario, vea [estrella barra diagonal &#40; Comentario &#41; &#40; DMX &#41; ](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

