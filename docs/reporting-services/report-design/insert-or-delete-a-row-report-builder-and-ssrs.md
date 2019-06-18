---
title: Insertar o eliminar una fila (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b20b95586e387484d536ad8005c6f57c1de4698
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580171"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>Insertar o eliminar una fila (Generador de informes y SSRS)
Puede agregar o eliminar filas de una región de datos Tablix en un informe paginado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La región de datos Tablix puede ser una tabla, una matriz o una lista. Los procedimientos siguientes no se aplican a las regiones de datos Gráfico y Medidor.  
  
 En una región de datos Tablix, puede agregar filas que están asociadas a un grupo (dentro de un grupo) o que no están asociadas a un grupo (fuera de un grupo). Una fila que está dentro de un grupo se repite una vez para cada valor de grupo único. Por ejemplo, una fila dentro de un grupo que está basada en el valor de una columna de datos que contiene nombres de colores se repite una vez para cada nombre de color. Para los grupos anidados, una fila puede estar fuera del grupo secundario, pero dentro del grupo primario. En este caso, la fila se repite una vez para cada valor único del grupo primario.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>Para seleccionar una región de datos con objeto de que aparezcan los identificadores de columna y de fila  
  
-   En la vista Diseño, haga clic en la esquina superior izquierda de la región de datos Tablix para que los identificadores de columna y de fila aparezcan por encima y junto a ella.  
  
     Para más información sobre las áreas de regiones de datos, vea [Tables, Matrices, and Lists &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="to-insert-a-row-in-a-selected-data-region"></a>Para insertar una fila en una región de datos seleccionada  
  
-   Haga clic con el botón derecho en el identificador de fila donde quiera insertar una fila, haga clic en **Insertar fila**y, después, haga clic en **Por encima** o **Por debajo**.  
  
     \- O bien  
  
-   Haga clic con el botón derecho en una celda de la región de datos donde quiera insertar una fila, haga clic en **Insertar fila**y, después, haga clic en **Por encima** o **Por debajo**.  
  
## <a name="to-delete-a-row-from-a-selected-data-region"></a>Para eliminar una fila de una región de datos seleccionada  
  
-   Seleccione las filas que quiere eliminar, haga clic con el botón derecho en el identificador de una de las filas seleccionadas y, después, haga clic en **Eliminar filas**.  
  
     \- O bien  
  
-   Haga clic con el botón derecho en una celda de la región de datos de la que quiere eliminar una fila y, después, haga clic en **Eliminar filas**.  
  
## <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>Para insertar una fila en un grupo de una región de datos seleccionada  
  
-   Haga clic con el botón derecho en una celda de grupo de filas en el área de grupo de filas de una región de datos Tablix donde quiera insertar una fila, haga clic en **Insertar fila**y, después, haga clic en **Por encima - Fuera del grupo**, **Por encima - Dentro del grupo**, **Por debajo - Dentro del grupo**o **Por debajo - Fuera del grupo**.  
  
     Una vez hecho esto, se agrega una fila dentro o fuera del grupo representado por la celda de grupo de filas sobre la que ha hecho clic.  
  
## <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>Para eliminar una fila de un grupo en una región de datos seleccionada  
  
-   Haga clic con el botón derecho en una celda de grupo de filas del área de grupo de filas de una región de datos Tablix de la que quiere eliminar una fila y, después, haga clic en **Eliminar filas**.  
  
## <a name="see-also"></a>Consulte también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)     
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
