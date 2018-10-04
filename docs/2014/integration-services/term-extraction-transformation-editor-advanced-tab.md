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
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce44e2709013a6d56d47ad30c90ecf5d92825503
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185335"
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
 Mediante esta opción se indica que la puntuación está determinada por el valor TFIDF del término. La puntuación TFIDF es el producto de la frecuencia del término y la frecuencia inversa del documento, definida de esta forma: TFIDF de un término T = (frecuencia de T) * log( (n.º de filas de entrada) / (n.º de filas con T) )  
  
 **Umbral de frecuencia**  
 Permite especificar el número de veces que una palabra o frase debe aparecer antes de extraerla. El valor predeterminado es 2.  
  
 **Longitud máxima del término**  
 Permite especificar la longitud máxima de una frase en palabras. Esta opción afecta únicamente a frases. El valor predeterminado es 12.  
  
 **Utilizar extracción de términos con distinción de mayúsculas y minúsculas**  
 Permite especificar si la extracción distinguirá mayúsculas de minúsculas. De manera predeterminada, es `False`.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación extracción de términos &#40;pestaña extracción de términos&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformación extracción de términos &#40;pestaña exclusión&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [Transformación Búsqueda de términos](data-flow/transformations/lookup-transformation.md)  
  
  
