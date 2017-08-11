---
title: Cambiar un elemento dentro de una celda (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91a54778-8929-41f9-bb4c-826cec636be4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f4a345f97fc3b414f6d804b127b625faa8e1204
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="change-an-item-within-a-cell-report-builder-and-ssrs"></a>Cambiar un elemento de una celda (Diseñador de informes y SSRS)
En informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , solo un elemento no contenedor, como un cuadro de texto, una línea o una imagen, se puede reemplazar por un elemento de informe nuevo. Por ejemplo, puede arrastrar una tabla hasta un cuadro de texto para reemplazar éste por la tabla.  
  
 Si la celda contiene un elemento contenedor, por ejemplo un rectángulo, una lista, una tabla o una matriz, el nuevo elemento se agrega al elemento contenedor en lugar de reemplazarlo. Para reemplazar un elemento contenedor por un nuevo elemento, elimine el contenedor. De este modo, el elemento contenedor se reemplaza por un cuadro de texto que, a su vez, se puede reemplazar por otro elemento.  
  
 De forma predeterminada, todas las celdas de una tabla, matriz o región de datos de lista contienen un cuadro de texto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-an-item-within-a-cell"></a>Para cambiar un elemento de una celda  
  
-   En la pestaña **Insertar** , en el grupo **Regiones de datos** o **Elementos de informe** , haga clic en el elemento que desee agregar al informe y, a continuación, haga clic en este último. El elemento se agregará al informe.  
  
> [!NOTE]  
>  El cuadro de diálogo **Propiedades de la imagen** se abre al arrastrar un elemento de informe de imagen a una celda; en él puede establecer propiedades como el origen de la imagen antes de agregarla a la celda.  
  
## <a name="see-also"></a>Vea también  
 [Imágenes, cuadros de texto, rectángulos y líneas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)   
 [Tablas, Matrices y listas de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
