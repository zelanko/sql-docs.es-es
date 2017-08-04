---
title: "Editor de transformación extracción de términos (pestaña Avanzadas) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 605085b59357a98011c801f8aa4675e89c3cd8a9
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>Editor de transformación Extracción de términos (pestaña Avanzadas)
  Use la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Extracción de términos** para especificar las propiedades de la extracción, tales como la frecuencia, la longitud y si deben extraerse palabras o frases.  
  
 Para obtener más información acerca de la transformación Extracción de términos, vea [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
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
 Permite especificar si la extracción distinguirá mayúsculas de minúsculas. El valor predeterminado es **False**.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación extracción de términos &#40; Término pestaña extracción &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformación extracción de términos &#40; Pestaña exclusión &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-exclusion-tab.md)   
 [Transformación Búsqueda de términos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  
