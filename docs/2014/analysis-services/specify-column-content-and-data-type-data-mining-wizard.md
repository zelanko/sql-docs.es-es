---
title: Especificar el contenido y el tipo de datos de la columna (Asistente para minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0634be64-4c38-4381-9b19-fe9a5889306c
author: minewiskan
ms.author: owend
ms.openlocfilehash: f23bc2e0f21f15c0af1a26d64e528c65632d75a2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940426"
---
# <a name="specify-column-content-and-data-type-data-mining-wizard"></a>Especificar contenido y el tipo de datos de las columnas (Asistente para minería de datos)
  Utilice la página **Especificar el contenido y el tipo de datos de las columnas** para especificar el uso y el tipo de datos para cada columna seleccionada en la página anterior del asistente. Si desea omitir la columna, haga clic en **Atrás** para volver a la página **Especificar los datos de aprendizaje**y desactive todas las casillas.  
  
 El uso de una columna indica cómo se utilizarán los datos en el modelo. Una columna se puede utilizar como una clave para identificar una serie, como un valor de entrada que se va a utilizar en el análisis o como el valor que desea predecir. Las columnas se pueden utilizar para tareas de predicción y de entrada de datos.  
  
 El tipo de datos especifica información adicional sobre el tipo de datos que contiene la columna y cómo se utilizarán esos datos durante la fase de aprendizaje. Algunos tipos de contenido requieren un tipo de datos concreto y viceversa. Puede que también necesite especificar un tipo de datos determinado dependiendo del algoritmo que utilice al crear un modelo de minería. Para obtener información sobre los tipos de contenido y los tipos de datos en estructuras y modelos de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](data-mining/content-types-data-mining.md).  
  
 **Para más información:** [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining/mining-structures-analysis-services-data-mining.md), [Columnas del modelo de minería de datos](data-mining/mining-model-columns.md), [Asistente para minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [Crear una estructura de minería de datos relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opciones  
 **Estructura del modelo de minería de datos**  
 Muestra las columnas de las vistas y las tablas anidadas que seleccionó en la página anterior del asistente.  
  
 **Columnas**  
 Enumera las columnas.  
  
 **Tipo de contenido**  
 Especifica el tipo de contenido para la columna. Si especificó que la columna es una clave en la página anterior del asistente, los valores siguientes estarán disponibles:  
  
|Opción|Descripción|  
|------------|-----------------|  
|Clave|Especifica que la columna contiene un identificador único para la serie de casos.|  
|Key Sequence|Especifica que la columna contiene un identificador de secuencia.|  
|Key Time|Especifica que la columna contiene una fecha u otro número continuo único que se utiliza para identificar una fecha o una serie temporal.|  
  
 Si seleccionó la columna como una columna que no es de clave, los valores siguientes están disponibles, dependiendo del tipo de datos:  
  
|Opción|Descripción|  
|------------|-----------------|  
|Continuo|Especifica que la columna contiene los valores numéricos continuos.|  
|Discretized|Especifica que la columna contiene valores numéricos que se han discretizado o se pueden tratar como valores discretos.|  
|Discrete|Especifica que la columna contiene texto u otros valores no numéricos.|  
  
 **Tipo de datos**  
 Especifica el tipo de datos para la columna.  
  
 Puede disponer de los siguientes valores:  
  
-   `Boolean`  
  
-   `Date`  
  
-   `Double`  
  
-   `Long`  
  
-   `Text`  
  
 **Detectar**  
 Analiza un ejemplo de datos en todas las columnas numéricas. Reemplaza los valores **Tipo de contenido** especificados con un tipo de contenido recomendado.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para minería de datos (ayuda F1) &#40;Analysis Services: minería de datos&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir columnas relacionadas &#40;Asistente para minería de datos&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tablas &#40;Asistente para minería de datos&#41;](specify-table-types-data-mining-wizard.md)   
 [Especifique el contenido y el tipo de datos de la columna &#40;Asistente para minería de datos&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
