---
title: Insertar o eliminar una fila (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bd9f92b0128bd6280654885f79f8231570f721de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105629"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>Insertar o eliminar una fila (Generador de informes y SSRS)
  Puede agregar o eliminar filas de una región de datos Tablix. La región de datos Tablix puede ser una tabla, una matriz o una lista. Los procedimientos siguientes no se aplican a las regiones de datos Gráfico y Medidor.  
  
 En una región de datos Tablix, puede agregar filas que están asociadas a un grupo (dentro de un grupo) o que no están asociadas a un grupo (fuera de un grupo). Una fila que está dentro de un grupo se repite una vez para cada valor de grupo único. Por ejemplo, una fila dentro de un grupo que está basada en el valor de una columna de datos que contiene nombres de colores se repite una vez para cada nombre de color. Para los grupos anidados, una fila puede estar fuera del grupo secundario, pero dentro del grupo primario. En este caso, la fila se repite una vez para cada valor único del grupo primario.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>Para seleccionar una región de datos con objeto de que aparezcan los identificadores de columna y de fila  
  
-   En la vista Diseño, haga clic en la esquina superior izquierda de la región de datos Tablix para que los identificadores de columna y de fila aparezcan por encima y junto a ella.  
  
     Para obtener más información sobre las áreas de la región de datos, vea [listas &#40;generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="to-insert-a-row-in-a-selected-data-region"></a>Para insertar una fila en una región de datos seleccionada  
  
-   Haga clic con el botón derecho en el identificador de fila donde quiera insertar una fila, haga clic en **Insertar fila**y, después, haga clic en **Por encima** o **Por debajo**.  
  
     \- O bien  
  
-   Haga clic con el botón derecho en una celda de la región de datos donde quiera insertar una fila, haga clic en **Insertar fila**y, después, haga clic en **Por encima** o **Por debajo**.  
  
### <a name="to-delete-a-row-from-a-selected-data-region"></a>Para eliminar una fila de una región de datos seleccionada  
  
-   Seleccione las filas que quiere eliminar, haga clic con el botón derecho en el identificador de una de las filas seleccionadas y, después, haga clic en **Eliminar filas**.  
  
     \- O bien  
  
-   Haga clic con el botón derecho en una celda de la región de datos de la que quiere eliminar una fila y, después, haga clic en **Eliminar filas**.  
  
### <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>Para insertar una fila en un grupo de una región de datos seleccionada  
  
-   Haga clic con el botón derecho en una celda de grupo de filas en el área de grupo de filas de una región de datos Tablix donde quiera insertar una fila, haga clic en **Insertar fila**y, después, haga clic en **Por encima - Fuera del grupo**, **Por encima - Dentro del grupo**, **Por debajo - Dentro del grupo**o **Por debajo - Fuera del grupo**.  
  
     Una vez hecho esto, se agrega una fila dentro o fuera del grupo representado por la celda de grupo de filas sobre la que ha hecho clic.  
  
### <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>Para eliminar una fila de un grupo en una región de datos seleccionada  
  
-   Haga clic con el botón derecho en una celda de grupo de filas del área de grupo de filas de una región de datos Tablix de la que quiere eliminar una fila y, después, haga clic en **Eliminar filas**.  
  
## <a name="see-also"></a>Consulte también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
