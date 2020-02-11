---
title: Ordenación interactiva (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 02735bafde927ba110de6465c5380987ddb6b5f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105615"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>Ordenación interactiva (Generador de informes y SSRS)
  Puede agregar botones de ordenación interactiva para permitir a los usuarios alternar entre el orden ascendente y descendente para las filas de una tabla o para las filas y columnas de una matriz. El uso más común de la ordenación interactiva es agregar un botón de ordenación a cada encabezado de columna. De esta forma, el usuario podrá elegir la columna por la que desea realizar la ordenación.  
  
 Sin embargo, puede agregar un botón de ordenación interactiva a cualquier cuadro de texto, no solo a los encabezados de columna. Por ejemplo, para un cuadro de texto de una fila situada fuera de un grupo de filas, puede especificar una ordenación para las filas o columnas del grupo primario, para las filas o columnas del grupo secundario o para las filas o columnas de detalles. También puede combinar campos en una única expresión de grupo y, a continuación, realizar la ordenación por varios campos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Al agregar una ordenación interactiva, es necesario especificar los elementos siguientes:  
  
-   **Qué ordenar:** ¿filas o columnas?  
  
-   **Los datos por los que se debe realizar la ordenación:** ¿un campo que se muestra en una columna de una tabla? ¿Un campo que no se muestra?  
  
-   **El contexto en el que se va a realizar la ordenación:** por ejemplo, se puede ordenar por las filas asociadas a grupos de filas; por las columnas asociadas a grupos de columnas; por filas de detalles; por grupos secundarios dentro de un grupo primario; o por un grupo primario y un grupo secundario al mismo tiempo.  
  
-   **El cuadro de texto al que se va a agregar el botón de ordenación:** ¿en el encabezado de columna o en el encabezado de fila de grupo?  
  
-   **Si se debe sincronizar la ordenación para varias regiones de datos:** puede diseñar un informe de forma que, cuando el usuario alterne el criterio de ordenación, también se ordenen otras regiones de datos con el mismo antecesor.  
  
 Para obtener instrucciones paso a paso, vea [Agregar una ordenación interactiva a una tabla o una matriz &#40;Generador de informes y SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 En la tabla siguiente se resumen los efectos que se pueden conseguir usando los botones de ordenación interactiva.  
  
|Acción|Qué ordenar|Dónde agregar el botón de ordenación|Los datos por los que ordenar|Ámbito de la ordenación|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|Ordenar filas de detalles para una tabla sin grupos|Detalles|Encabezado de columna|Campo del conjunto de datos enlazado a esta columna|Región de datos|  
|Ordenar las instancias de grupo de nivel superior para una matriz|Grupos|Encabezado de columna|Expresión de grupo para el grupo primario|Región de datos|  
|Ordenar las filas de detalles para un grupo secundario de una tabla|Detalles|Fila de encabezado del grupo secundario|Campo del conjunto de datos por el que ordenar|Grupo secundario|  
|Ordenar filas para varios grupos de filas y filas de detalles de una tabla|Grupos, pero debe volver a definir la expresión de grupo|Encabezado de columna|El agregado del campo del conjunto de datos por el que se va ordenar|Región de datos|  
|Sincronizar el criterio de ordenación para varias regiones de datos|Grupos|Normalmente, el encabezado de columna|Expresión de grupo|Dataset|  
  
 El procesador de informes aplica la ordenación interactiva después de que se han aplicado todas las expresiones de ordenación de grupo y de región de datos. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>Agregar una ordenación interactiva para varios grupos  
 En una tabla con grupos de filas anidados y basados en un único campo de conjunto de datos, puede agregar un botón de ordenación interactiva que ordene los valores del grupo primario, los valores del grupo secundario o las filas de detalles. Sin embargo, quizás desee ofrecer al usuario la posibilidad de ordenar la tabla por los valores del grupo primario y los del grupo secundario sin tener que hacer clic varias veces.  
  
 Para ello, debe volver a diseñar la tabla para realizar la agrupación por una expresión que combine varios campos. Por ejemplo, para un conjunto de datos con recuentos del inventario, si la tabla original está agrupada por tamaño y, a continuación, por color, puede especificar un único grupo con una expresión de grupo que sea una combinación de tamaño y color. Para obtener más información, vea [Agregar una ordenación interactiva a una tabla o una matriz &#40;Generador de informes y SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Agregar una ordenación interactiva a una tabla o una matriz &#40;Generador de informes y SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
