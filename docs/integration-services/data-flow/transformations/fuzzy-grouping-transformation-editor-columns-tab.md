---
title: "Editor de transformaci&#243;n Agrupaci&#243;n aproximada (pesta&#241;a Columnas) | Microsoft Docs"
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
  - "sql13.dts.designer.fuzzygroupingtransformation.columns.f1"
helpviewer_keywords: 
  - "Agrupación aproximada, editor de transformación"
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor de transformaci&#243;n Agrupaci&#243;n aproximada (pesta&#241;a Columnas)
  Use la pestaña **Columnas** del cuadro de diálogo **Editor de transformación Agrupación aproximada** para especificar las columnas utilizadas para agrupar filas con valores duplicados.  
  
 Para obtener más información acerca de la transformación Agrupación aproximada, vea [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## Opciones  
 **Columnas de entrada disponibles**  
 Seleccione en esta lista las columnas de entrada utilizadas para agrupar filas con valores duplicados.  
  
 **Nombre**  
 Muestra los nombres de las columnas de entrada disponibles.  
  
 **Paso a través**  
 Seleccione si la columna de entrada debe incluirse en la salida de transformación. Todas las columnas utilizadas para la agrupación se copian automáticamente en la salida. Si activa esta columna, puede incluir columnas adicionales.  
  
 **Columna de entrada**  
 Seleccione una de las columnas de entrada seleccionadas anteriormente en la lista **Columnas de entrada disponibles**.  
  
 **Alias de salida**  
 Escriba un nombre descriptivo para la columna de salida correspondiente. De forma predeterminada, el nombre de la columna de salida es el mismo que el nombre de la columna de entrada.  
  
 **Alias de salida de grupo**  
 Escriba un nombre descriptivo para la columna que contendrá el valor canónico de los valores duplicados agrupados. El nombre predeterminado de esta columna de salida es el nombre de la columna de entrada con _clean anexado.  
  
 **Tipo de coincidencia**  
 Seleccione coincidencia exacta o aproximada. Las filas se consideran duplicadas si existe un parecido suficiente entre todas las columnas con un tipo de coincidencia aproximada. Si también especifica coincidencia exacta en determinadas columnas, solamente se consideran como posibles duplicados las filas que contienen valores idénticos en las columnas de coincidencia exacta. Por tanto, si sabe que una determinada columna no tiene errores o incoherencias, puede especificar coincidencia exacta en esa columna para aumentar la exactitud de la coincidencia aproximada en otras columnas.  
  
 **Similitud mínima**  
 Establezca el umbral de similitud del nivel de combinación con el control deslizante. Cuanto más se acerque el valor a 1, más deberá parecerse el valor de búsqueda al valor de origen para que pueda calificarse como coincidencia. Al aumentar el umbral se puede mejorar la velocidad de la coincidencia ya que se tendrán en cuanta menos registros candidatos.  
  
 **Alias de salida de similitud**  
 Especifique el nombre de una nueva columna de salida que contendrá los resultados de similitud de la combinación seleccionada. Si este valor se deja vacío, la columna de salida no se crea.  
  
 **Números**  
 Especifique la importancia de los números iniciales y finales en la comparación de los datos de la columna. Por ejemplo, si los números iniciales son significativos, "123 Main Street" no se agrupará con "456 Main Street."  
  
|Value|Description|  
|-----------|-----------------|  
|**Neither**|Los números iniciales y finales no son significativos.|  
|**Leading**|Solo son significativos los números iniciales.|  
|**Trailing**|Solo son significativos los números finales.|  
|**LeadingAndTrailing**|Tanto los números iniciales como los finales son significativos.|  
  
 **Marcas de comparación**  
 Para más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](../../../integration-services/data-flow/comparing-string-data.md).  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Identificar filas de datos similares mediante la transformación Agrupación aproximada](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  