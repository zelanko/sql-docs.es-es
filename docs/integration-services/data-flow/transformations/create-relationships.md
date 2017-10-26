---
title: Crear relaciones | Documentos de Microsoft
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
- sql13.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9f511b91e0e085c07dcf4dfb7742514ddad6070
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="create-relationships"></a>Crear relaciones
  Utilice el cuadro de diálogo **Crear relaciones** para editar asignaciones entre las columnas de origen y las columnas de la tabla de búsqueda configuradas en el Editor de transformación Búsqueda aproximada, el Editor de transformación Búsqueda y el Editor de transformación Búsqueda de términos.  
  
> [!NOTE]  
>  En el cuadro de diálogo **Crear relaciones** se muestran únicamente las listas **Columna de entrada** y **Columna de búsqueda** cuando se invoca desde el Editor de transformación Búsqueda de términos.  
  
 Para obtener más información acerca de las transformaciones que utilizan en el cuadro de diálogo **Crear relaciones** , vea [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md), [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)y [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columna de entrada**  
 Seleccione las columnas de entrada disponibles de la lista.  
  
 **Columna de búsqueda**  
 Seleccione columnas de la lista de columnas de búsqueda disponibles.  
  
 **Tipo de asignación**  
 Seleccione coincidencia exacta o aproximada.  
  
 Cuando se utiliza la coincidencia aproximada, las filas se consideran duplicadas si son lo suficientemente similares en todas las columnas que tienen un tipo de coincidencia aproximada. Para obtener mejores resultados en la coincidencia aproximada, puede especificar que algunas columnas deben utilizar la coincidencia exacta en lugar de la coincidencia aproximada. Por ejemplo, si sabe que una determinada columna no tiene errores ni incoherencias, puede especificar una coincidencia exacta en esa columna, de tal modo que solo las filas que contengan valores idénticos en esta columna se consideren como posibles duplicados. Esto aumenta la precisión de la coincidencia aproximada en otras columnas.  
  
 **Marcas de comparación**  
 Para obtener más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Similitud mínima**  
 Establezca el umbral de similitud del nivel de columna con el control deslizante. Cuanto más se acerque el valor a 1, mayor deberá ser el parecido entre el valor de búsqueda y el valor de origen para que pueda calificarse como coincidencia. Aumentar el umbral puede mejorar la velocidad de coincidencia, ya que tendrán que tenerse en cuenta menos registros candidatos.  
  
 **Alias de salida de similitud**  
 Especifique el nombre de una nueva columna de salida que contendrá los resultados de similitud de la columna seleccionada. Si este valor se deja vacío, la columna de salida no se crea.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Búsqueda aproximada &#40; Pestaña columnas &#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor de transformación Búsqueda &#40; Página columnas &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de transformación Búsqueda de términos &#40; Término de búsqueda pestaña &#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
  

