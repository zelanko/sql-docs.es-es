---
title: "Editor de transformaci&#243;n Agrupaci&#243;n aproximada (pesta&#241;a Avanzadas) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzygroupingtransformation.advanced.f1"
helpviewer_keywords: 
  - "Agrupación aproximada, editor de transformación"
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Editor de transformaci&#243;n Agrupaci&#243;n aproximada (pesta&#241;a Avanzadas)
  Use la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Agrupación aproximada** para especificar las columnas de entrada y salida, configurar umbrales de similitud y definir delimitadores.  
  
> [!NOTE]  
>  Las propiedades **Exhaustive** y **MaxMemoryUsage** de la transformación Agrupación aproximada no están disponibles en el **Editor de transformación Agrupación aproximada**, pero se pueden establecer con el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre la transformación Agrupación aproximada en [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Para obtener más información acerca de la transformación Agrupación aproximada, vea [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## Opciones  
 **Nombre de la columna de clave de entrada**  
 Especifique el nombre de una columna de salida que contenga el identificador único para cada fila de entrada. La columna **_key_in** tiene un valor que identifica de forma exclusiva cada fila.  
  
 **Nombre de la columna de clave de salida**  
 Especifique el nombre de una columna de salida que contenga el identificador único para la fila canónica de un grupo de filas duplicadas. La columna **_key_out** se corresponde con el valor **_key_in** de la fila de datos canónica.  
  
 **Nombre de la columna de resultados de similitud**  
 Especifique un nombre para la columna que contiene los resultados de similitud. Los resultados de similitud tienen un valor entre 0 y 1 que indica la similitud de la fila de entrada con la fila canónica. Cuanto más se acerque el resultado a 1, mayor será la coincidencia entre la fila y la fila canónica.  
  
 **Umbral de similitud**  
 Defina el umbral de similitud utilizando el control deslizante. Cuanto más se acerque el umbral a 1, más deberán parecerse las filas entre sí para ser consideradas duplicados. Aumentar el umbral puede mejorar la velocidad de coincidencia, ya que tendrán que tenerse en cuenta menos registros candidatos.  
  
 **Delimitadores de token**  
 La transformación proporciona un conjunto predeterminado de delimitadores para dividir los datos en tokens, pero se pueden agregar o quitar los delimitadores que sea necesario editando la lista.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Identificar filas de datos similares mediante la transformación Agrupación aproximada](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  