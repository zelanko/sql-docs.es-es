---
title: Editor de transformación extracción de términos (pestaña Avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea6582aacefc7c17450e59689bec29c260a38d07
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385043"
---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>Editor de transformación Extracción de términos (pestaña Avanzadas)
  Use la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Extracción de términos** para especificar las propiedades de la extracción, tales como la frecuencia, la longitud y si deben extraerse palabras o frases.  
  
 Para obtener más información acerca de la transformación Extracción de términos, vea [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifica que la transformación extrae únicamente nombres individuales.  
  
 **Frase**  
 Especifica que la transformación extrae únicamente frases.  
  
 **Nombre y frase**  
 Especifica que la transformación extrae nombres y frases.  
  
 **Frecuencia**  
 Especifica que la puntuación está determinada por la frecuencia del término.  
  
 **TFIDF**  
 Mediante esta opción se indica que la puntuación está determinada por el valor TFIDF del término. La puntuación TFIDF es el producto de término y frecuencia inversa de documento, definido como: TFIDF de un término T = (frecuencia de T) * log ((#rows de entrada) / (#rows con T))  
  
 **Umbral de frecuencia**  
 Permite especificar el número de veces que una palabra o frase debe aparecer antes de extraerla. El valor predeterminado es 2.  
  
 **Longitud máxima del término**  
 Permite especificar la longitud máxima de una frase en palabras. Esta opción afecta únicamente a frases. El valor predeterminado es 12.  
  
 **Utilizar extracción de términos con distinción de mayúsculas y minúsculas**  
 Permite especificar si la extracción distinguirá mayúsculas de minúsculas. De manera predeterminada, es `False`.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Extracción de términos &#40;pestaña Extracción de términos&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformación Extracción de términos &#40;pestaña Exclusión&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [Transformación Búsqueda de términos](data-flow/transformations/lookup-transformation.md)  
  
  
