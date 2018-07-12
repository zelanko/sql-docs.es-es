---
title: Editor de transformación Agrupación aproximada (pestaña columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
caps.latest.revision: 29
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b393e0a2807a002f1805b5c2664f9ae2b3e527a6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172996"
---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Editor de transformación Agrupación aproximada (pestaña Columnas)
  Use la pestaña **Columnas** del cuadro de diálogo **Editor de transformación Agrupación aproximada** para especificar las columnas utilizadas para agrupar filas con valores duplicados.  
  
 Para obtener más información acerca de la transformación Agrupación aproximada, vea [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Seleccione en esta lista las columnas de entrada utilizadas para agrupar filas con valores duplicados.  
  
 **Nombre**  
 Muestra los nombres de las columnas de entrada disponibles.  
  
 **Paso a través**  
 Seleccione si la columna de entrada debe incluirse en la salida de transformación. Todas las columnas utilizadas para la agrupación se copian automáticamente en la salida. Si activa esta columna, puede incluir columnas adicionales.  
  
 **Columna de entrada**  
 Seleccione una de las columnas de entrada seleccionadas anteriormente en la lista **Columnas de entrada disponibles** .  
  
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
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Neither**|Los números iniciales y finales no son significativos.|  
|**Leading**|Solo son significativos los números iniciales.|  
|**Trailing**|Solo son significativos los números finales.|  
|**LeadingAndTrailing**|Tanto los números iniciales como los finales son significativos.|  
  
 **Marcas de comparación**  
 Para obtener más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](data-flow/comparing-string-data.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificación de filas de datos similares con la transformación Agrupación aproximada](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
