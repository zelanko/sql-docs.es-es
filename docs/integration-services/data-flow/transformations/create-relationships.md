---
title: Crear relaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fce60dd2a2663e23001805621e622b4334126a1e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71291540"
---
# <a name="create-relationships"></a>Crear relaciones

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilice el cuadro de diálogo **Crear relaciones** para editar asignaciones entre las columnas de origen y las columnas de la tabla de búsqueda configuradas en el Editor de transformación Búsqueda aproximada, el Editor de transformación Búsqueda y el Editor de transformación Búsqueda de términos.  
  
> [!NOTE]  
>  En el cuadro de diálogo **Crear relaciones** se muestran únicamente las listas **Columna de entrada** y **Columna de búsqueda** cuando se invoca desde el Editor de transformación Búsqueda de términos.  
  
 Para obtener más información acerca de las transformaciones que utilizan en el cuadro de diálogo **Crear relaciones** , vea [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md), [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)y [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columna de entrada**  
 Seleccione las columnas de entrada disponibles de la lista.  
  
 **columna de búsqueda**  
 Seleccione columnas de la lista de columnas de búsqueda disponibles.  
  
 **Tipo de asignación**  
 Seleccione coincidencia exacta o aproximada.  
  
 Cuando se utiliza la coincidencia aproximada, las filas se consideran duplicadas si son lo suficientemente similares en todas las columnas que tienen un tipo de coincidencia aproximada. Para obtener mejores resultados en la coincidencia aproximada, puede especificar que algunas columnas deben utilizar la coincidencia exacta en lugar de la coincidencia aproximada. Por ejemplo, si sabe que una determinada columna no tiene errores ni incoherencias, puede especificar una coincidencia exacta en esa columna, de tal modo que solo las filas que contengan valores idénticos en esta columna se consideren como posibles duplicados. Esto aumenta la precisión de la coincidencia aproximada en otras columnas.  
  
 **Marcas de comparación**  
 Para más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Similitud mínima**  
 Establezca el umbral de similitud del nivel de columna con el control deslizante. Cuanto más se acerque el valor a 1, mayor deberá ser el parecido entre el valor de búsqueda y el valor de origen para que pueda calificarse como coincidencia. Aumentar el umbral puede mejorar la velocidad de coincidencia, ya que tendrán que tenerse en cuenta menos registros candidatos.  
  
 **Alias de salida de similitud**  
 Especifique el nombre de una nueva columna de salida que contendrá los resultados de similitud de la columna seleccionada. Si este valor se deja vacío, la columna de salida no se crea.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Búsqueda aproximada &#40;pestaña Columnas&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor de transformación Búsqueda &#40;página Columnas&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de transformación Búsqueda de términos &#40;pestaña Búsqueda de términos&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
