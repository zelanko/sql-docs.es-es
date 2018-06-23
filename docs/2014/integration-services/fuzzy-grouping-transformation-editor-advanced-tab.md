---
title: Editor de transformación Agrupación aproximada (pestaña Avanzadas) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b1696734810b1b3fd4ceccb624139358cea0dcaa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202129"
---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Editor de transformación Agrupación aproximada (pestaña Avanzadas)
  Use la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Agrupación aproximada** para especificar las columnas de entrada y salida, configurar umbrales de similitud y definir delimitadores.  
  
> [!NOTE]  
>  El `Exhaustive` y `MaxMemoryUsage` propiedades de la transformación Agrupación aproximada no están disponibles en la **Editor de transformación Agrupación aproximada**, pero se puede establecer mediante el uso de la **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre la transformación Agrupación aproximada en [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para obtener más información acerca de la transformación Agrupación aproximada, vea [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de la columna de clave de entrada**  
 Especifique el nombre de una columna de salida que contenga el identificador único para cada fila de entrada. La `_key_in` columna tiene un valor que identifica de forma única cada fila.  
  
 **Nombre de la columna de clave de salida**  
 Especifique el nombre de una columna de salida que contenga el identificador único para la fila canónica de un grupo de filas duplicadas. La columna `_key_out` se corresponde con el valor `_key_in` de la fila de datos canónica.  
  
 **Nombre de la columna de resultados de similitud**  
 Especifique un nombre para la columna que contiene los resultados de similitud. Los resultados de similitud tienen un valor entre 0 y 1 que indica la similitud de la fila de entrada con la fila canónica. Cuanto más se acerque el resultado a 1, mayor será la coincidencia entre la fila y la fila canónica.  
  
 **Umbral de similitud**  
 Defina el umbral de similitud utilizando el control deslizante. Cuanto más se acerque el umbral a 1, más deberán parecerse las filas entre sí para ser consideradas duplicados. Aumentar el umbral puede mejorar la velocidad de coincidencia, ya que tendrán que tenerse en cuenta menos registros candidatos.  
  
 **Delimitadores de token**  
 La transformación proporciona un conjunto predeterminado de delimitadores para dividir los datos en tokens, pero se pueden agregar o quitar los delimitadores que sea necesario editando la lista.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificación de filas de datos similares con la transformación Agrupación aproximada](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  